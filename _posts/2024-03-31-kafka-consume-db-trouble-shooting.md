---
layout:       post
title:        "카프카 메시지 키값 설정으로 DB 동시성 이슈 해결하기"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 회고
---

- 본 글에 사용된 코드는 문제 상황을 설명하기 위한 예시이며, 실제로 사용된 코드가 아닙니다.

회사에서 작성한 코드를 테스트하던 도중, 로컬에서는 발생하지 않는 문제가 테스트 서버에서는 발생하는 이상한 상황을 만났다. 

# 문제 상황

DB 테이블 DDL은 다음과 같다. DB는 Postgresql이다.

```sql
create table test1 (
    id bigserial primary key,
    user_id bigint,
    last_access_time timestamp
)
```

내가 구현해야 했던 로직은 다음과 같다

1. 카프카 프로듀서가 어떠한 이벤트를 produce한다. 
    - 이때 토픽을 T1이라 하자.
    - 이벤트에는 유저를 식별할 수 있는 userId가 존재한다.
2. 하나의 컨슈머 그룹에 있는 컨슈머들은 T1으로부터 메시지를 소비한다
3. 소비한 메시지에서 userId를 사용해 다음과 같은 로직을 수행한다
    - userId를 통해 DB 레코드가 있는지 확인한다
        - 레코드가 있으면 레코드를 update한다
        - 레코드가 없으면 새로운 레코드를 insert한다.
4. manual commit을 진행한다.

위 상황에서 3번에서 다음 그림과 같이 동일한 userId를 가진 레코드가 여러번 새롭게 insert되는 문제가 발생했다.
![concurrency error](/img/2024-03-31-kafka-consume-db-trouble-shooting/img.png)

이런 문제는 토픽의 파티션과 컨슈머들이 1:1 대응되는 상황에서, producer가 메시지를 produce할 때 라운드로빈 방식으로 각 파티션에 메시지를 produce하기 때문에 발생했다. 즉, 같은 userId를 가지 여러 메시지가 각기 다른 파티션에서 각기 다른 consumer에 의해 소비되어서 동시에 userId를 기준으로 디비 레코드 존재 유무를 판단해서 발생한 문제였다. 이 상황을 consumer와 DB 관점에서 보면 다음과 같다.

![consumer, db perspective](/img/2024-03-31-kafka-consume-db-trouble-shooting/img1.png)

# 해결 방법

이 문제의 해결 방법은 간단하다. producer에서 메시지를 produce할 때 userId를 키값으로 정해주면 된다. 키값을 정해주면 그 키를 기준으로 메시지가 들어갈 파티션이 정해진다. 따라서 여러 파티션에 같은 userId를 가진 여러 메시지가 분산되어서 저장될 일이 없다. 결국, 서로 다른 컨슈머들이 같은 userId를 가진 서로 다른 메시지를 동시에 소비할 일이 없어서 위 문제가 해결된다.


![after solution](/img/2024-03-31-kafka-consume-db-trouble-shooting/img2.png)

코드 단에서 변경할 부분은 다음과 같이 아주 작다. produce하는 부분만 조금 바꿔주면 된다.

- as-is:

```kotlin
@Component
class TestProducer(
    private val kafkaTemplate: KafkaTemplate<String, String>
) {
    
    fun produce(topic: String, message: String) {
        kafkaTemplate.send(topic, message)
    }
}
```

- to-be:

```kotlin
@Component
class TestProducer(
    private val kafkaTemplate: KafkaTemplate<String, String>
) {
    
    fun produce(topic: String, key: String, message: String) {
        kafkaTemplate.send(topic, key, message)
    }
}
```