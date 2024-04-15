---
layout:       post
title:        "2. 스파크 간단히 살펴보기"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- apache spark
- 스파크 완벽 가이드
---
스파크는 클러스터에서 데이터 처리 작업을 관리하고 조율하는 프레임워크이다. 연산에 사용할 클러스터는 클러스터 매니저가 관리한다. 사용자는 스파크 애플리케이션을 클러스터 매니저에게 제출(submit)한다. 사용자가 제출하면 클러스터 매니저는 애플리케이션 실행에 필요한 자원을 할당해서 작업을 마무리한다. 클러스터 매니저 종류로는 spark standalone, hadoop yarn, method가 있다.

## 1. 스파크 애플리케이션

스파크 애플리케이션은 드라이버(driver) 프로세스와 다수의 executor 프로세스로 구성된다. 드라이버가 마스터라 생각하면 된다. 모두 다 클러스터 내의 각자의 노드에서 실행되며 드라이버 프로세스가 하는 일은 다음과 같다.

- 스파크 애플리케이션 정보의 유지 관리
- 사용자 프로그램, 입력에 대한 응답
- executor 작업과 관련된 분석, 배포, 스케줄링
- 애플리케이션 수명 주기 동안 관련된 정보를 모두 유지

Executor는 다음과 같은 일을 한다

- 프로세스가 할당한 작업을 수행한다
- 진행 상황을 드라이버 노드에 보고한다

스파크의 driver, executor, cluster manager의 상관관계는 다음과 같다.

![driver, executor, cluster manager relationship](/img/2024-04-13-spark-definition2/img.png)

- 스파크는 사용 가능한 자원 파악을 위해 클러스터 매니저를 사용한다
- 드라이버 프로세스는 주어진 작업을 완료하기 위해 드라이버 프로그램의 명령을 executor에서 실행해야 한다.

# 2. 스파크의 다양한 언어 API

스파크의 언어 API를 이용하면 다양한 프로그래밍 언어로 스파크 코드를 실행할 수 있다. 지원하는 언어는 다음과 같다. 스칼라, 자바, 파이썬, SQL, R. 구조적 API만 사용한다면 언어와 무관하게 비슷한 성능을 낸다. 

SparkSession은 스파크 코드를 시작하기 위한 엔트리포인트이다. 스파크는 사용자가 작성한 코드를 executor의 JVM에서 실행할 수 있는 코드로 변환한다.

![language api](/img/2024-04-13-spark-definition2/img1.png)

# 3. 스파크 API

스파크가 다양한 언어를 지원하는 이유는 스파크가 저수준 비구조적 API, 고수준 구조적 API 둘을 지원하기 때문이다.

# 4. 스파크 시작하기

대화형 모드를 스파크를 시작하면 스파크 애플리케이션을 관리하는 SparkSession이 자동으로 생성된다. Standalone 모드로 시작한다면 사용자가 애플리케이션에서 직접 SparkSession 객체를 생성해야한다.

# 5. SparkSession

스파크는 SparkSession이라고 불리는 드라이버 프로세스로 스파크 애플리케이션을 제어한다. 스파크 애플리케이션과 SparkSession은 1:1 대응된다. SparkSession 작업을 클러스터에서 실행한다.

SparkSession을 생성하고 1,000 개의 로우를 가지는 DataFrame을 만드는 예제는 다음과 같다. 이 예제를 실행하면 숫자 범위의 각 부분은 서로 다른 executor에 할당된다.

```python
from pyspark.sql import SparkSession
spark = SparkSession.builder\
    .appName("mySession")\
    .getOrCreate()
my_range = spark.range(1000)\
	.toDF("number") # DataFrame 생성
```

# 6. DataFrame

DataFrame은 테이블의 데이터를 컬럼과 로우로 표현한 구조적 API이다.  컬럼과 컬럼 타입을 정의한 목록은 스키마라 부른다. DataFrame은 여러 컴퓨터에 데이터를 분산해 저장한다. 스파크와 R도 DataFrame을 지원하지만 단일 컴퓨터에 저장된다는 점이 다르다.

## 6.1 파티션

물리적 머신에 존재하는 로우 집합이다. Executor가 병렬로 작업을 처리할 수 있게 파티션이라는 단위로 데이터가 분할된다. 때문에 파티션 갯수와 excutor 갯수는 곧 병렬성을 나타낸다. 파티션 갯수와 executor 갯수 중 낮은 것이 해당 클러스터의 병렬성이다.

DataFrame을 사용하면 파티션을 수동, 개별적으로 처리할 필요가 없다. 물리적 파티션에 데이터 변환용 함수를 지정하면 스파크가 실제처리 방법을 결정한다.

# 7 트랜스포메이션

스파크 핵심 데이터 구조는 immutable 하다. 때문에 DataFrame를 변경하려면 원하는 변경 방법을 알려줘야 한다. 이 때 사용하는 명령을 트랜스포메이션이라한다. 하지만 트랜스포메이션은 액션을 호출하지 않는다면 실제 트랜스포메이션을 수행하지 않는다.

```python
# 트랜스포메이션 예제
# 액션이 없어 실제 트랜스포메이션은 수행하지 않는다
divis_by_2 = my_range.where("number % 2 = 0")
```

트랜스포메이션의 종류는 다음과 같다

- 좁은 트랜스포메이션: 하나의 파티션이 하나의 출력 파티션에만 영향을 준다. 파이프라이닝을 자동으로 수행한다.
- 넓은 트랜스포메이션: 하나의 입력 파티션이 여러 출력 파티션에 영향을 미친다. 스파크가 클러스터에서 파티션을 교환하는 것을 셔플이라 한다. 셔플의 결과는 디스크에 저장된다.

## 7.1 지연 연산 (lazy evaluation)

스파크가 연산 그래프를 처리하기 직전까지 기다리는 동작 방식을 의미한다. 스파크는 연산 명령이 내려졌을 때 우선 트랜스포메이션에 대해 실행 계획을 생성한다. 그 후 코드를 실행하는 마지막 순간까지 대기하다가 원형 DataFrame 트랜스포메이션을 간결한 물리적 실행 계획으로 컴파일한다. 이 과정을 통해 데이터 흐름을 최적화 한다.

# 8. 액션

일련의 트랜스포메이션으로부터 결과를 계산하게 하는 명령이다. 

```python
# 액션 예시
divis_by_2.count()
```

액션 유형은 다음과 같다

- 콘솔에서 데이터를 보는 액션
- 각 언어로 된 네이티브 객체에 데이터를 모으는 액션
- 출력 데이터소스에 저장하는 액션

액션을 지정하는 스파크 잡이 시작된다. 스파크 잡은 필터(좁은 트랜스포메이션)를 수행한 뒤 파티션별로 레코드 수를 카운트(넓은 트랜스포메이션)한다. 그 후 각 언어에 적합한 네이티브 객체에 결과를 모은다

# 9. 스파크 UI

스파크는 잡의 진행 상황을 모니터링할 수 있는 UI를 제공한다. 드라이버 노드의 4040포트로 접속할 수 있다. 

# 10. 종합 예제

## 10.1 데이터 읽기

```python
flight_data = spark\
    .read\
    .option("inferSchema", "true")\ # DataFrame의 스키마 정보를 알아내는 스키마 추론 기능
    .option("header", "true")\ # 파일의 첫 로우를 헤더로 지정하는 옵션
    .csv("./2015-summary.csv")

# take 액션을 호출해서 로컬 배열로 변환
flight_data.take(3)
# output:
	# [Row(DEST_COUNTRY_NAME='United States', ORIGIN_COUNTRY_NAME='Romania', count=15),
	# ...]
```

## 10.2 실행계획 읽기

```python
# sort는 트랜스포메이션이라 호출 시 데이터에 변화를 주지 않는다
# 하지만 스파크는 실행 계획을 만들고, 클러스터에서 처리할 방법을 알아내기에
# 실행계획을 조회할 수 있다.
flight_data.sort("count")\
    .explain()

# output: 실행계획에서 최종 결과는 가장 위, 데이터 소스는 가장 아래에 있다.
# == Physical Plan ==
# AdaptiveSparkPlan isFinalPlan=false
# +- Sort [count#50 ASC NULLS FIRST], true, 0
#   +- Exchange rangepartitioning(count#50 ASC NULLS FIRST, 200), ENSURE_REQUIREMENTS, [plan_id=89]
#      +- FileScan csv [DEST_COUNTRY_NAME#48,ORIGIN_COUNTRY_NAME#49,count#50]
```

```python
# 스파크는 기본적으로 200개의 셔플 파티션을 생성한다.
# 이 값을 5로 바꾼다
# 사용자는 물리적 데이터를 직접 다루는 대신, 속성으로 물리적 실행 특성을 제어한다
spark.conf.set("spark.sql.shuffle.partitions", "5")

flight_data.sort("count").take(2)
```

위 예제를 도식화하면 다음과 같다
![code explain](/img/2024-04-13-spark-definition2/img2.png)

# 10.3 DataFrame과 SQL

사용자는 DataFrame과 SQL을 이용해 비즈니스 로직을 표현할 수 있다. 그러면 스파크는 실제 로직 실행 전에 해당 로직을본 실행 계획으로 컴파일한다. 스파크 SQL을 사용하면 모든 DataFrame을 데이블이나 뷰(임시 테이블)로 등록한 뒤 SQL을 사용할 수 있다.

```python
# DataFrame을 테이블이나 뷰로 만든다
flight_data.createOrReplaceTempView("flight_data")

# 쿼리를 사용하는 방법
sql_way = spark.sql('''
    select DEST_COUNTRY_NAME, count(1)
    from flight_data
    group by DEST_COUNTRY_NAME
''')

# 데이터프레임을 사용하는 방법
dataframe_way = flight_data.groupBy("DEST_COUNTRY_NAME")\
    .count()
```

## 10.4 DataFrame의 변환 과정

DataFrame의 실행 계획은 기본적으론 트랜스포메이션 하나가 하나의 단계이다. 이 단계들은 물리적 실행 시점에 실행하는 최적화로 인해 줄어들 수 있다. 실행 계획은 트랜스포메이션의 DAG(Directed Acyclic Graph)이며 액션이 호출되면 결과를 만든다. DAG의 각 단계는 immutable한 새로운 DataFrame을 만든다.

출처 - [스파크 완벽 가이드](https://product.kyobobook.co.kr/detail/S000001810100)
