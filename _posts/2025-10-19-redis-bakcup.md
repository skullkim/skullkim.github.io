---
layout:       post
title:        "레디스 데이터 백업 방법"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
  - redis
---

- 레디스는 데이터를 메모리로 관리해서 인스턴스 재시작 시 데이터가 손실될 수 있다.
    - 복제는 인스턴스 재시작에 따른 손실은 막을 수 있으나 의도치 않은 데이터 삭제 등은 막지 못한다.
- 레디스는 RDB, AOF 두 가지 백업 방식을 지원한다.
    - RDB(Redis DataBase): 일정 시점에 메모리에 저장된 데이터 전체를 저장하는 스냅숏 방식. 바이너리 형태로 저장.
        - 장점
            - 시점 단위 백업본 저장 가능
            - AOF에 비해 복원이 빠르다
        - 단점:
            - 특정에 대한 백업본이 없다면, 해당 시점으로 백업 불가
    - AOF(Append Only File): 레디스 인스턴스가 처리한 쓰기 작업을 차례대로 기록, 복원 시 파일을 읽어서 데이터 세트 구성. 레디스 프로토콜(RESP) 형태로 저장.
        - 장점
            - 원하는 시점으로 복구 가능
        - 단점
            - 크기가 커서 주기적으로 압축해 저장해야 한다.
    - 프로덕션에서는 두 방식을 같이 사용하는 것을 권장한다. 인스턴스 하나에서 두 방식을 모두 사용할 수 있다.
        - AOF로 데이터 내구성 확보
        - RDB로 빠른 복구가 필요할 때 대응.
    - 레디스 데이터 복원은 서버 재시작 시점에만 가능하다. 이 때 AOF, RDB 파일잉 모두 존재하면 AOF 파일을 사용한다. AOF가 내구성 보장이 더 뛰어나기 때문이다.

# 1. RDB 방식 데이터 백업

## 1.1 백업 설정 방법

- RBD 백업 방식은 세 가지이다
    - 설정 파일에서 특정 조건 파일이 자동으로 저장되게 지정
    - 커맨드 수동 실행
    - 복제 기능을 이용한 자동 생성

### 1.2 특정 조건에 자동으로 RDB 파일 생성

commend:

```sql
# 일정 기간 동안 정한 키 개수 만큼 데이터 변경 시 RDB 파일 생성
# save "" 같이 빈 문자열로 RDB 백업 비활성화 가능
save <기간<초>> <기간 내 변경된 키 개수>
# 새성할 파일 이름 지정, 기본값은 dump.rdb
dbfilename <RDB 파일 이름>
dir <RDB 파일이 저장될 경로>
```

- 레디스 인스턴스는 실행 중 설정이 변경되어도 즉시 반영되지 않는다. CONFIG SET 커맨드로 설정 변경 후, CONFIG REWRITE 커맨드로 설정 파일을 재작성해야한다.

### 1.3 수종으로 RDB 파일 생성

- SAVE, BGSAVE 커맨드를 이용해 원하는 시점에 파일 생성
    - SAVE: 동기 방식
    - BGSAVE: fork를 호출해 자식 프로세스를 생성해서 백그라운드 실행. 이미 해당 방식으로 데이터 백업 중이라면 에러 반환. SCHEDULE 옵션을 사용한다면 에러 대신 진행중이면 백업 완료 후 다시 BGSAVE 실행.
- 정상 저장 여부는 LASTSAVE로 확인. 파일이 저장된 마지막 시점을 UNIX timestamp로 반환.

### 1.4 복제를 사용해 자도으로 RDB 파일 생성

- 레플리카가 REPLICAOF 커맨드로 마스터에 요청. 마스터 노드에서 RDB 파일 생성 후 복제본을 레플리카로 전달.
- 복제 연결이 되어 있을 때 이슈로 일정 시간 이상 복제가 끊어졌었다면, 재연결 후 마스터가 레플리카에게 전달.

# 2. AOF 방식 데이터 백업

commend:

```sql
# AOF 파일에 주기적으로 데이터 저장
appendonly yes
# 파일 이름 지정, 기본값: appendonly.aof
appendfilename "appendonly.aof"
# 파일 경로 지정, 경로가 아닌 디렉터리 이름만 지정 가능. dir 옵션 하위에 생성된다.
appenddirname "appendonlydir"
```

- 저장되거나 변경되어 저장되는 커맨드
    - 존재하지 않는 키에 대한 조작 커맨드 등은 저장되지 않는다.
    - AOF 파일에는 메모리에 영향을 끼치는 커맨드만 저장된다.
    - 블로킹 기능을 지원하는 list의 BRPOP 커맨드는 RPOP으로 저장된다.
    - string에 사용자가 입력한 부동소수점 값을 더하는 INCRBYFLOAT 커맨드는 증분 후 값을 직접 SET하는 커맨드로 남는다.
        - 레디스가 실행되는 아키텍처에 따라 부동 소수점을 처리하는 방식이 다를 수 있기 때문이다.

## 2.1 AOF 파일을 재구성 하는 방법

- AOF는 커맨드를 대부분 저장히기 때문에 용량이  크다. 때문에 주기적으로 재구성(rewrite) 해줘야한다.
- 재구성은 메모리에 있는 데이터로 파일을 새로 생성하는 방식으로 동작한다. 재구성된 파일은 기본적으로 RDB 형태(*.base.rdb)이지만 aof-use-rdb-preamble 옵션을 no로 변경하면 aof 파일로 저장할 수 있다*(***.base.aof).
- 파일 재구성 시 fork를 이용해 자식프로세스가 재구성을 실행한다.
- 버전 7 이전에는 재구성된 AOF파일 하나에 RDB(binary)와 AOF(RESP 프로토콜) 형태가 공존했다. 이는 AOF 파일 수동 처리 시 관리가 복잡해 진다는 단점이 존재한다.
![redis aof before v7](/img/2025-10-19-redis-backup/img.png)
- 버전 7 이후에는 AOF파일과 RBD 파일을 분리해 저장한다. 또 한, 현재 레디스가 바라보는 파일을 나타내는 매니페스트 파일이 추가되었다. 이 파일들은 모두 설정에서 지정한 appenddirname 이름의 폴더 내에 저장한다.
    - 여기서 생성되는 RDB, AOF 파일명의 번호와 매니페스트 seq 값은 재구성 때 1씩 증가한다.
![redis aof after v7](/img/2025-10-19-redis-backup/img1.png)
- AOF 파일 재구성은 모두 순차 IO를 사용하기에 효율적으로 디스크에 접근한다. 이는 레디스가 복원 시 AOF 파일을 순차 데이터 로드로만 사용하기 때문이다.

### 2.1.1 자동 AOF 재구성

```sql
# 마지막으로 재구성된 aof 파일에 비해, 현재 aof 파일이 n% 만큼 커지면 재구성 시작
auto-aof-rewrite-percentage n
# 마지막으로 재구성된 aof가 없을 때 현재 aof 파일이 xmb를 넘으면 재구성 시작
auto-aof-rewrite-min-size xmb
# 마지막으로 저장된 AOF 파일의 크기
INFO Persistence

# 수동 AOF 재구성 커맨드
BGREWRIETAOF
```

### 2.1.2 AOF 타임스탬프

- 버전 7 이상부터는 aof-timestamp-enabled 설정을 yes로 바꾸어서 AOF 저장에 대한 타임스탬프를 남길 수 있다. 이를 이용해 시스템에서 특정 시점 복원(point-in-time recovery)이 가능하다.
    - ex - src/redis-check-aof —truncate-to-timestamp 1234 appendonlydir/appendonly.aof.manifest
        - redis-check-aof는 AOF 파일 손상 시에도 사용할 수 있다. 서버 장애 발생 시 AOF 파일 작성 도중 중지됐다면, redis-check-aof를 이용해 AOF 파일 정상 여부를 확인할 수 있다. 이때 권장하는 옵션으로 복구한다면 원본 파일이 변경되기 때문에 필요 시 백업이 필요하다.
    - 이렇게 타임스탬프를 지정했다면 버전 7 이전과는 AOF 파일이 호환되지 않는다.

# 3. AOF 파일의 안전성

- RDB 방식보다 AOF 방식이 더 안전한 이유는 다음과 같다.

![redis aof](/img/2025-10-19-redis-backup/img2.png)
- 레디스가 WRITE 시스템 콜 호출 후 우선 OS 버퍼에 데이터를 임시 저장한다. OS 버퍼는 OS가 판단하기에 커널에 여유가 있거나 최대 지연 30초가 도달하면 데이터를 디스크에 내려쓴다.
- FSYNC는 OS 버퍼에 저장된 내용을 실제 디스크에 쓰도록 강제하는 시스템콜이다. OS에 부하가 있어도 FSYNC는 무조건 데이터를 디스크에 flush 한다.
- 레디스는 AOF 파일 저장 시 APPENDSYNC 옵션을 이용해 FSYNC 호출을 제어할 수 있다.
    - APPENDSYNC no: WRITE 시스템 콜을 호출한다. 서버 장애 시 최대 30초에 해당하는 데이터를 잃는다.
    - APPENDSYNC always: WRITE와 FSYNC를 함께 호출한다. 이 때문에 성능이 느리다.
    - APPENDSYNC everysec: 데이터 저장 시 WRITE 호출 하고, 1초에 한번 FSYNC 시스템콜을 호출한다. no와 성능이 비슷하다. 서버 장애시 최대 1초에 해당하는 데이터만 유실되기에 속도와 안전성의 균형을 맞출 수 있다.

# 4. 백업 시 주의사항

- RDB, AOF 파일 백업을 사용한다면 레디스 인스턴스 maxmemory 값을 물리 서버 메모리보다 적게 설정하는 것이 중요하다.
- 레디스는 copy-on-write 방식을 사용해서 자식 프로세스가 메모리상의 데이터를 하나 더 복사해 백업을 진행한다. 그 와중에 부모 프로세스는 클라이언트와의 연결을 처리한다. 때문에 최악의 경우 기존 메모리의 2배를 사용한다. 이 때 maxmemory가 너무 크면 OOM으로 인한 서버 다운이 발생한다.
- 물리적 메모리 용량 별로 적절한 maxmemory값은 다음과 같다.
 
![redis backup](/img/2025-10-19-redis-backup/img3.png)


출처 - [개발자를 위한 레디스](https://product.kyobobook.co.kr/detail/S000210785682)
