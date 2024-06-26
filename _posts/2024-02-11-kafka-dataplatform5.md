---
layout:       post
title:        "5장. 카프카 컨슈머"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- 카프카
- 카프카,데이터플랫폼의최강자
---

프로듀서가 메시지를 생산해서 카프카의 토픽으로 메시지를 보내면, 그 토픽에서 메시지를 가져와 소비하는 것이 카프카 컨슈머의 역할이다. 

컨슈머의 주요 기능은 특정 파티션을 관리하고 있는 파티션 리더에게 메시지 가져오기를 요청하는 것이다. 각 요청은 로그의 오프셋을 명시하고, 그 위치로부터 로그 메시지를 수신한다. 컨슈머는 가져올 메시지의 위치를 조정할 수 있고, 필요하다면 이미 가져온 데이터도 다시 가져올 수 있다.

# 1. 컨슈머 주요 옵션

컨슈머에는 다음과 같은 종류가 있다.

- 올드 컨슈머(Old Consumer)
- 뉴 컨슈머(New Consumer)

위 두 컨슈머 차이는 주키퍼 사용 유무다. 0.9 버전 이전엔 주키퍼 지노드에 컨슈머 오프셋을 저장했다. 그러나 0.9 버전 이후부터는 오프셋을 카프카 토픽에 저장한다.

컨슈머가 지원하는 옵션은 다음과 같다.

- bootstrap.servers
    - 카프카 클러스터에 처음 연결하기 위한 호스트와 포트 정보를 나타낸다. “hostName:port, hostName:port”와 같이 연달아 기재할 수 있다. 단일 호스트만 입력할 수도 있지만, 카프카 클러스터가 살아있고 해당 호스트만 장애가 발생할 수도 있기에 리스트 전체를 입력하는 것이 좋다.
- fetch.min.bytes
    - 한 번에 가져올 수 있는 최소 데이터 사이즈이다. 지정한 사이즈보다 작을 경우, 요청에 대해 응답하지 않고 데이터가 누적될 때까지 기다린다.
- fetch.max.bytes
    - 한 번에 가져올 수 있는 최대 데이터 사이즈
- fetch.max.wait.ms
    - fetch.min.bytes에 의해 설정된 데이터보다 적은 경우 요청에 응답을 기다리는 최대 시간
- group.id
    - 컨슈머가 속한 컨슈머 그룹을 식별하는 식별자이다
- enable.auto.commit
    - 백그라운드로 주기적으로 오프셋을 커밋 한다
- auto.commit.interval.ms
    - 주기적으로 오프셋을 커밋 하는 시간
- auto.offset.rest
    - 카프카에서 초기 오프셋이 없거나 현재 오프셋이 더 이상 존재하지 않을 경우에 다음 옵션으로 리셋한다
        - earliest: 가장 초기의 오프셋 값으로 설정한다
        - latest: 가장 마지막의 오프셋 값으로 설정한다
        - none: 이전 오프셋 값을 찾지 못하면 에러를 나타낸다
- heartbeat.interval.ms
    - 그룹 코디네이터에게 얼마나 자주 KafkaConsumer poll() 메서드로 하트비트를 보낼 것인지 조정한다. 아래에서 설명할 session.timeout.ms보다 값이 낮아야 하며, 보통 1/3 수준으로 설정한다(default 3s)
- session.timeout.ms
    - 컨슈머와 브로커 사이의 세션 타임아웃 시간, 브로커가 컨슈머가 살아있는 것으로 판단하는 시간(default: 10s). 컨슈머가 그룹 코디네이터에게 하트비트를 보내지 않고 해당 옵션에서 지정한 시간만큼 지나면, 해당 컨슈머는 종료되어가 장애가 발생한 것으로 판단하고 컨슈머 그룹은 리밸런스(rebalance)를 시도한다.
    - 이 값을 기본값보다 낮게 설정하면 실패를 빨리 감지할 수 있지만, GC나 pool 루프를 완료하는 시간이 길어진다면, 원치 않는 리밸런스가 일어나기도 한다. 반대로 높게 설정하면 실제 오류를 감지하는 데 시간이 오래 걸릴 수 있다.
- max.pool.records
    - 단일 호출 poll()에 대해 최대 레코드 수를 조정한다. 이 옵션을 통해 애플리케이션이 폴링 루프에서 데이터양을 조정할 수 있다.
- max.pool.interval.ms
    - 컨슈머가 살아있는지를 체크하기 위해 하트비트를 주기적으로 보내다 보면, 실제 메시지를 가져오지 않고 하트비트만 보낼 수 있다. 이런 경우 컨슈머가 무한정 해당 파티션을 점유할 수 없게 주기적으로 poll을 호출하지 않으면 장애라고 판단하고, 컨슈머 그룹에서 제외한 뒤, 다른 컨슈머가 해당 파티션에서 메시지를 가져갈 수 있게 한다.

# 2. 파티션과 메시지 순서

토픽의 파티션이 여러 개 일 때, 프로듀서가 보낸 메시를 컨슈머가 소비하는 순서를 보장할 수 없다. 예컨대, 프로듀서가 a, b, c, d, e를 메시지로 보냈다면 컨슈머가 소비하는 순서는 a, d, b, e, c 일 수도 있다. 프로듀서가 보낸 메시지는 여러 파티션에 나눠서 저장되고, 컨슈머는 오직 파티션의 오프셋 기준으로만 메시지를 가져오기 때문이다.

![kafka partition, page sequence](/img/2024-02-11-kafka-dataplatform5.md/img.png)

즉, 카프카 컨슈머에서 메시지 순서는 동일한 파티션 내에서는 프로듀서가 생성한 순서와 동일하게 처리하지만, 파티션과 파티션 사이에서는 순서를 보장하지 않는다.

만약 메시지 순서를 보장하고 싶다면, 토픽 파티션 수를 1로 설정하면 된다. 다만, 분산 처리가 안되고 하나의 컨슈머에서만 처리할 수 있어서 처리량이 낮아진다는 단점이 존재한다.

# 3. 컨슈머 그룹

컨슈머는 카프카 토픽에서 메시지를 읽어온다. 이때, 같은 컨슈머 그룹에 있는 컨슈머들은 하나의 토픽에 동시에 접속해 메시지를 가져올 수 있다. 이는 기존의 메시지 큐에서 컨슈머가 메시지를 한 번 가져가면 삭제되는 것과 대조되는 점이다.

컨슈머 그룹을 사용하면 컨슈머 확장에도 용이하다. 아래와 같이 파티션 수가 컨슈머 수 보다 많은 상황을 생각해 보자.

![kafka consumer group](/img/2024-02-11-kafka-dataplatform5.md/img1.png)

이 상황에서 프로듀서가 메시지를 토픽에 보내는 속도가 컨슈머의 소비 속도보다 빠르다면, 컨슈머가 소비하지 못하는 메시지는 점점 많아지게 된다.  이때, 단순히 컨슈머만 추가한다면, 기존 컨슈머의 오프셋 정보와 새로운 컨슈머의 오프셋 정보가 뒤섞이게 된다. 컨슈머 그룹은 동일한 컨슈머 아이디를 설정해서 컨슈머를 추가하면, 기존 컨슈머가 가지고 있던 파티션 소유권은 새로운 컨슈머로 이전하는 리밸런스(rebalance)를 제공한다. 이 기능을 통해 컨슈머 그룹에는 컨슈머를 쉽고 안전하게 추가할 수 있고 제거할 수도 있어서 높은 가용성과 확장성을 확보할 수 있다. 위 예시를 리밸선스 했을 때 상황은 다음과 같다.

![kafka consumer group2](/img/2024-02-11-kafka-dataplatform5.md/img2.png)

만약 이렇게 토픽의 파티션 수와 동일하게 컨슈머 수를 늘렸음에도 프로듀서가 보내는 메시지 속도를 따라가지 못한다면, 토픽과 파티션 수를 같이 늘려줘야 한다. 파티션 하나에는 하나의 컨슈머만 연결할 수 있기 때문이다.

그룹 내에 존재하는 컨슈머는 하트비트를 이용해 할당된 파티션의 소유권을 유지한다. 하트비트는 컨슈머가 poll할 때와 가져한 메시지의 오프셋을 커밋 할 때 보낸다. 컨슈머가 오랫동안 하트비트는 보내지 않으면, 세션은 타임아웃되고, 해당 컨슈머가 다운되었다고 판단해서 리밸런스를 진행한다.

![kafka consumer group3](/img/2024-02-11-kafka-dataplatform5.md/img3.png)

# 4. 커밋과 오프셋

컨슈머가 poll()을 호출할 때마다 컨슈머 그룹은 카프카에 저장되어 있고 아직 읽기 않은 메시지를 가져온다. 컨슈머 그룹의 컨슈머들은 이 기능을 위해 각 파티션에서 자신이 가져간 메시지의 위치 정보(오프셋)을 기록한다. 각 파티션에 대해 현재 위치를 업데이트하는 동작을 커밋(commit)이라고 한다.

카프카는 각 컨슈머 그룹의 파티션 별로 오프셋 정보를 저장하기 위한 저장소가 별도로 필요하다. 0.9버전 이전의 카프카 컨슈머는 주키퍼에 이 정보를 저장했다. 그 이후부터는 카프카 내에 별도로 내부에서 사용하는 토픽(__consumer_offsets)을 만들고 그 토픽에 오프셋 정보를 저장한다. 이로 인해 리밸런스가 일어나도, 컨슈머는 새로운 파티션에 대해 가장 최근 커밋된 오프셋을 읽고, 그 이후부터 메시지들을 가져올 수 있다.

커밋에는 자동 커밋과 수동 커밋이 있다.

## 4.1 자동 커밋

컨슈머 애플리케이션들의 기본 값으로 가장 많이 사용하는 방식이다. 컨슈머 옵션 중 enable.auto.commit=true를 이용하면 5초마다 컨슈머가 poll()을 호출해 가장 마지막 오프셋을 커밋 한다. 5초 주기는 기본값이며 auto.commit.interval.ms를 사용해 조정할 수 있다. 

자동 커밋은 이미 읽은 메시지를 중복해 읽는 문제를 야기할 수 있다. 예컨대, 파티션 p로부터 컨슈머 c1이 메시지를 읽고 마지막 커밋으로부터 아직 5초가 지나지 않았다고 해보자. 이때, 리밸런스가 되어서 새로운 컨슈머 c2가 해당 파티션으로부터 메시지를 읽는다면, 오프셋이 아직 커밋 되지 않았기에 c1과 동일한 메시지를 읽게 된다. 중복을 줄이기 위해 자동 커밋 시간을 줄이면 되지만, 근본적인 해결책은 아니다. 

## 4.2 수동 커밋

수동 커밋은 메시지 처리가 완료될 때까지 메시지를 가져온 것으로 간주해서는 안 되는 경우에 사용한다. 예를 들어 메시지를 가져와 DB에 저장하는 경우, DB에 데이터가 완전히 저장될 때까지 오프셋을 커밋하면 안 된다. 그렇지 않으면 메시지에 손실이 발생하게 된다. 이 경우 수동 커밋을 이용해 직접 커밋을 호출해야 한다.

수동 커밋 역시 중복이 발생할 수 있다. 메시지들이 DB에 저장하는 도중 실패하게 된다면, 마지막 커밋 된 오프셋부터 메시지를 다시 가져오게 된다. 이때, 일부 메시지들이 이미 DB에 저장되어 있다면, 중복이 발생하게 된다. 

카프카에서 메시지는 한 번씩 전달되지만, 장애 등의 이유로 중복이 발생할 수 있어서 at leat once를 보장한다.

## 4.3 특정 파티션 할당

다음과 같은 경우 특정 파티션에 대한 세밀한 제어를 사용할 수 있다.

- 키-값 형태로 파티션에 저장되어 있고, 특정 파티션에 대한 메시지만 가져와야 하는 경우
- 컨슈머 프로세스가 가용성이 높은 구성일 때, 카프카가 컨슈머의 실패를 감지하고 재조정이 필요 없고 자동으로 프로세스가 다른 시스템에서 재시작 되는 경우(쿠버네티스 사용 등)

다만 임의로 특정 파티션을 할당한다면, 각 칸슈머 인스턴스마다 컨슈머 그룹 아이디를 서로 다르게 설정해야 한다. 만약 동일한 컨슈머 그룹 아이디를 설정하게 되면, 컨슈머들끼리 할당된 같은 파티션에 대한 오프셋 정보를 공유해서 원치 않는 동작을 할 수도 있다.

## 4.4 특정 오프셋부터 메시지 가져오기

만약 메시지 중복 처리 등의 이유로 오프셋 관리를 수동으로 해야 한다면, 수동으로 메시지를 읽어올 지점을 정해야 한다. 이때, seek() 메서드를 사용하면 된다.

출처 - [카프카, 데이터플랫폼의 최강자](https://product.kyobobook.co.kr/detail/S000001973303)