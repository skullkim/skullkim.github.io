---
layout:       post
title:        "레디스 자료구조"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
  - redis
---

레디스는 키-값 형태 저장소이다. 저장된 데이터 검색은 키를 식별자로 한다.

# 1. 레디스의 자료구조

## 1.1 String

- 레디스에서 가장 간단한 자료구조다.
- 문자열 하나는 최대 512MB 이다.
- biary-safe해서 바이트값을 저장할 수 있다.
- 키-값이 1:1인 유일한 자료구조다.

명령어

```yaml
SET k v # key-value 쌍 저장, Key가 있는 값이면 value가 덮어씌워진다
# 옵션
SET k v NX # 지정한 키가 없을 때만 저장
# XX는 키가 있을 때만 덮어씌우며 저장

GET k # key에 대응하는 값 조회

# 숫자 원자적 조작
INCR # 1씩 증가
INCRBY N # 저장된 수 += N
DECR, DECRBY # 감소 연산

# 성능이 중요한 대규모 시스템에서 유용
MSET k1 v1 k2 v2 # 한 번에 여러 값 저장
MGET k1 k2 # 한 번에 여러 값 조회
```

## 1.2 list

- 순서를 가지는 문자열 목록
- 단일 리스트에 최대 42억개 아이템 저장 가능
- 인덱스를 이용한 접근 가능, 스택 또는 큐로 사용 가능
    - 인덱스 중간 접근은 O(n) → 데이터 증가에 따라 성능 저하

명령어

```yaml
LPUSH k v # 왼쪽에 삽입
RPUSH k v # 오른쪽에 삽입

# 인덱스 범위에 있는 데이터 검색
# 정수는 왼쪽부터 인덱스, 음수는 오른쪽부터 인덱스
LRANGE k 0 -1 # 전체 데이터 검색
LRANGE k 0 3 # 오른쪽에서 0~3번 인덱스까지 조회

LPOP k # 왼쪽 첫 번째 아이템 조회 후 삭제
LTRIM k sIdx eIdx # sIdx~eIdx 범위에 속하지 않는 아이템 삭제, 저장할 데이터 갯수 유지에 유용

# key가 k인 리스트의 v1 값 이전에 v2 삽입, 이후에 삽입은 AFTER사용
# 기준이 되는 지정 데이터(v1)이 없으면 에러
LINSERT k BEFORE v1 v2

LSET k idx v # k의 idx 인덱스의 값을 v로 덮어씌운다
LINDEX k idx # k의 idx 인덱스의 값을 확인

```

## 1.3 hash

- field-value 쌍을 가진 아이템 집합
    - field는 하나의 hash내에서 고유하다
    - field, value 모두 string으로 저장된다
- 객체를 저장하기 편하다는 관점에서 RDB와의 변환이 간편하다
- RDB와 달리 새로운 필드 추가가 쉽다는 이점이 있다.
![redis hash](/img/2025-10-08-redis-data-structure/img.png)
- 
명령어
```yaml
HSHET key field value # hash에 아이템 저장
HGET key field # 저장된 value 조회
HNGET key f1 f2 # 여러 필드 한번에 조회
HGETALL key # key에 해당하는 해시 내의 모든 filed-value 쌍 반환
```

## 1.4 Set
![redis set](/img/2025-10-08-redis-data-structure/img1.png)
- 정렬되지 않은 문자열 모음
- set 내의 원소는 고유하다.
- 집합 관련 연산이 가능해서 객체 가 관계 계산 등에 유용

명령어

```yaml
# SADD는 실제 저장된 원소 갯수 반환
SADD s v # set s에 값 v 추가
SADD s v1 v2 v3 # 여러 값 한번에 추가
SMEMBEEERS s # Set s에 저장된 모든 값 조회, 순서는 랜덤
SREM s v1 # s에서 v1 삭제
SPOP s # Set s의 원소 중 하나를 랜덤하게 반환하고 삭제
SUNION s1 s2 # s1 s2 합집합
SINER s1 s2 # s1 s2 교집합
SDIFF s1 s2 # s1 s2 차집합
```

## 1.5 sortedSet
![redis sorted-set](/img/2025-10-08-redis-data-structure/img2.png)
- 스코어 값에 따라 정렬되는 고유한 문자열 집합 (정렬을 저장시 수행, 스코어가 같으면 사전순 정렬)
- 모든 아이템은 scroe-value 쌍을 가진다.
- index를 통한 원소 접근이 가능하다
    - 접근 속도는 O(log(n))으로 list index 접근이 O(n)보다 빠르다 ⇒ 아이템 조회가 많으면 sorted set이 더 효육적이다.

명령어

- ZADD

```yaml
# 저장할 데이터(v)가 없으면 생성 후 저장
# 저장할 데이터가 있으면 스코어만 업데이트.
# 지정된 키가 sorted set이 아닌 형태로 존재하면 에러 반환
ZADD s sc v # Set s에 스코어-값 쌍인 sc-v를 저장한다.
ZADD s sc1 v1 sc2 v2 # Set s에 스코어-값 쌍 여러개 저장 가능
```

- ZADD 옵션
    - XX: 아이템이 이미 존재할 때만 스코어 업데이트
    - NX: 아이템이 존재하지 않을 때에만 신규 업데이트
    - LT: 업데이트 하고자 하는 스코어가 기존 아이템 스코어보다 작을 때 업데이트. 기존 아이템이 없으면 삽입.
    - GT: 업데이트하고자 하는 스코어가 기존 아이템 스코어보다 클 때에만 업데이트. 기존 아이템이 없으면 삽입.
- ZRANGE

```yaml
# 저장된 데이터 조회
# 기본적으로 인덱스를 기준으로 조회한다.(start, stop로 조회할 인덱스 범위 선택)
# list와 같이 음수 인덱스 사용 가능
ZRANGE key start stop [BYSCORE | BYLEX] [REV] [LIMIT offset count] [WITHSCORES]
```

- 조회 조건
    - 기본: 인덱스를 기준으로 조회. start, stop은 인덱스범위
    - BYSCORE: 스코어 범위로 조회. start, stop은 스코어값. -inf, +inf 로 인덱스 최댓값 표현
    - BYLEX: 모든 데이터를 사전순으로 조회.
        - 사용 예: ZRANGE sKey (b [f BYLEX → ‘(’는 해당 문자 포함, ‘[’는 해당 문자 비포함
        - ZRAGE sKey - + BYLEX 는 해당 sorted set에 저장된 모든 데이터 조회

## 1.6 비트맵
![redis bitmap](/img/2025-10-08-redis-data-structure/img3.png)
- String 타입에서 비트 연산을 할 수 있게 확장한 형태 → String 특성을 그대로 가지고 있다(512MB 크기 - 2^32 bit, binary safe)
- 저장 공간을 획기적으로 줄일 수 있다(40억건 정수 ID로 구분되는 유저 Y/N 데이터를 512MB 안에 저장 가능)
- 명령어

    ```yaml
    # key 비트맵의 offset번쨰 값을 value(0 or 1)로 세팅
    SETBIT key offset value
    GETBIT key offset # 값 조회
    # 미트맵 키에 대한 복수 작업을 한번 에 수행
    BITFIELD key [GET type offset] [SET type offset value] [INCRBY type offset increment] [OVERFLOW policy]
    # type: 
    # - u	부호 없는 정수 (u1 ~ u64)	1비트 ~ 64비트
    # - i	부호 있는 정수 (i1 ~ i64)	1비트 ~ 64비트
    # OVERFLOW: INCRBY 명령 사용 시, 비트 영역의 최댓값(혹은 최솟값)을 초과할 때 Redis가 어떻게 처리할지 정책을 지정
    # - WRAP: 기본값, overflow, underflow 발생 시 값 순환
    # - SAT: overflow시 최댓값으로 고정, underflow시 최소값으로 고정
    # - FAIL: overflow, underflow 발생 시 작업 중단 후 NULL 반환
    
    BITCOUNT key # 1인 비트 갯수 반환
    ```


## 1.7 Heperloglog

- 집합 원소 갯수를 추정할 수 있는 자료구조 (추정 오차 0.81%)
- 입력된 값을 해싱한 후 얻은 두 가지 통계를 저장하는 레지스터 배열을 사용해서 데이터 갯수와 상관없이 일정한 메모리를 유지할 수 있다.
- 최대 12KB, 2^64개 데이터 저장 가능.

명령어

```yaml
PFADD key value # 데이터 저장
PFCOUNT key # 데이터 카운트
```

## 1.8 Geospatial

- 경도, 위도 쌍으로 지리 데이터 저장
- 내부적으로 sorted set 사용

명령어

```yaml
# 데이터 추가
# member는 위치와 연결할 이름
# sorted set과 같은 옵션 사용 가능
GEOADD key longitude latitude member

# 위도 경도 조회
GEOPOS key member

# 두 멤버 간 거리 조회
# unit은 m(meter), km(kilo meter), mi(mile), ft(feet)
GEODIST key member1 member2 unit

# GEOSEARCH 를 이용해 특정 위치 기준 원하는 거리 내의 아이템 검색 가능
# - BYRADIUS 옵션으로 반경 거리 기준 검색 가능
# - BYBOX 기준으로 직사각형 거리 기준 데이터 검색 가능
```

## 1.9 Stream

- 레디스를 메시지 브로커로 사용할 수 있게 하는 자료구조
- append-only 방식 사용

# 2. 레디스에서 키를 관리하는 법

- 키가 여러개 아이템을 가지는 자료구조에서는 자동으로 키가 생성되고 삭제된다. 키 관리는 다음과 같은 규칙을 따른다.
    - 키가 존재하지 않을때 아이템을 넣으면 아이템을 삽입하기 전에 빈 자료구조를 생성한다
    - 모든 아이템을 삭제하면 키도 자동으로 삭제된다 (Stream은 예외)
    - 키가 없는 상태에서 읽기 전용 커맨드를 수행하면 에러를 반환하는 대신 키가 있으나 아이템이 없을 것처럼 동작한다.
- 키 관련 명령어

```yaml
# key 존재 여부 조회
EXISTS key [key...]

# 패턴에 매칭되는 키를 조회
# 한번에 매칭되는 모든 키를 반환하기 떄문에 키가 많으면 다른 커맨드가 대기하는 문제 발생
KEYS pattern
# pattern
# - h?llo: ?에 아무 문자 하나가 들어가는 모든 키
# - h*ll0: *에 임의의 길이, 문자가 들어가는 모든 키
# - h[ae]llo: a 또는 e가 들어간 키
# - h[^e]llo: e를 제외한 모든 문자가 들어간 키
# - h[a-b]llo: a, b가 들어간 키

# KEYS를 대체해 키 조회에 사용할 수 있는 커맨드. 커서 기반으로 동작
# COUNT를 통해 조회 갯수 조정 가능
# - 레디스는 메모리 스캔 후 저장 형식에 따라 몇 개의 키를 더 읽어오는게 효율적이라 판단하면 
# - 그 만큼을 더 반환한다. 때문에 꼭 count만큼을 가져오지 않을 수도 있다
# TYPE은 지정한 타입의 키만 반환한다
SCAN cursor [MATCH pattern] [COUNT count] [TYPE type]

# STORE: 정렬 결과를 destination에 저장
# GET pattern: 정렬 결과 외에, 주어진 패턴에 속하는 키의 값을 정렬된 순서로 가져올 때 사용
# BY pattern: key 요소를 정렬하는 대신, 요소 값을 사용해서 pattern에 속하는 키의 값을 정렬한다
SORT key [BY pattern] [LIMIT offset count] [GET pattern [GET pattern ...]] [ASC | DESC] [ALPHA] [STORE destination]

# 키 이름 변경
RENAME key newKey
RENAMENX key newKey # 오직 key가 기존에 존재할 때만 동작

# source key의 값을 destination key로 복사, REPLACE가 있으면 destination 값을 덮어 씌운다. 없으면 에러
# destination-db는 source를 복사할 DB 인덱스
COPY source destination [DB destination-db] [REPLACE]

# key의 자료구조 반환
TYPE key

# 키에 대한 상세 정보 반환
OBJECT <subcommand> [<arg> [value] [opt] ...]

# 모든 키를 삭제. 기본값은 SYNC
# ASYNC일 경우 삭제 도중 추가되는 키는 삭제되지 않는다.
# lazyfree-lazy-user-flush 옵션이 yes라면 ASYNC가 없어도 비동기 동작한다. 버전7 기준 기본값은 no이다.
FLUSHALL [ASYNC | SYNC]

# 키와 키에 저장된 모든 데이터 삭제, 동기 동작
DEL key [key...]

# 키와 키를 삭제한다, 비동기 동작
# 키와 연결 데이터를 우선 끊는 것으로 시작한다.
# SET 같이 키 하나에 아이템 여러개가 있는 경우 삭제에 오랜 시간이 소요되어 비동기 권장
UNLINK key [key...]

# 키가 만료된 시간을 초 단위로 정의
EXPIRE key seconds [NX | XX | GT | LT]
# NX: 키 만료 시간이 정의돼 있지 않을 경우만 실행
# XX: 키 만료 시간이 정의돼 있을 때에만 실행
# GT: 현재 키가 가진 만료 시간보다 새로 입력한 초가 더 클때만 실행
# LT: 현재 키가 가진 시간보다 새로 입력한 초가 더 작을때만 실행

# 키 만료 시간 지정
EXPIREAT key uniz-time-seconds [NX | XX | GT | LT]

# 키가 만료되는 시간(unix timestamp)
# 만료 시간이 없으면 -1, 키가 없으면 -2
EXPIRETIME key

# key가 몇 초 뒤에 만료되는지
# 만료 시간이 없으면 -1, 키가 없으면 -2
TTL key
```

출처 - [개발자를 위한 레디스](https://product.kyobobook.co.kr/detail/S000210785682)