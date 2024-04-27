---
layout:       post
title:        "5. 구조적 API 기본 연산"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- apache spark
- 스파크 완벽 가이드
---

DataFrame은 Row 타입의 레코드와 각 레코드에 수행할 연산 표현식을 나타내는 여러 컬럼으로 구성된다. DataFrame에 관한 용어는 다음과 같은 의미를 가진다.

- 스키마: 각 컬럼 명과 데이터 타입을 정의한다.
- 파티셔닝: DataFrame, DataSet이 클러스터에서 물리적으로 배치되는 형태
- 파티셔닝 스키마: 파티션을 배치하는 방법을 정의

# 1. 스키마

스키마는 데이터소스에서 얻거나 직접 정의할 수 있다. 스키마를 출력해 보면 다음과 같다.

```python
flight_data = spark.read.json("/2015-summary.json")
flight_data.schema

# output:
# Out[11]: StructType([StructField('DEST_COUNTRY_NAME', StringType(), True), 
		# StructField('ORIGIN_COUNTRY_NAME', StringType(), True), 
		# StructField('count', LongType(), True)])
# StructField(이름, 데이터 타입, nullable)
```

스키마는 여러 StructField 타입 필드로 구성된 StructType 객체이다. 스파크는 런타임에 데이터 타입이 스키마의 데이터 타입과 일치하지 않으면 오류를 발생시킨다.

DataFrame에 스키마를 만드는 방법은 다음과 같다.

```python
from pyspark.sql.types import StructField, StructType, StringType, LongType

my_manual_schema = StructType([
    StructField("DEST_COUNTRY_NAME", StringType(), True),
    StructField("ORIGIN_COUNTRY_NAME", StringType(), True),
    StructField("count", LongType(), False, metadata = {"hello" : "world"})
]) # 필요한 경우 메타데이터(해당 컬럼과 관련된 정보)를 지정할 수 있다. 스파크 ML 라이브러리에서 사용한다

df = spark.read\
    .format("json")\
    .schema(my_manual_schema)\
    .load("/2015-summary.json")
```

# 2. 컬럼과 표현식

스파크 컬럼은 표현식을 사용해 레코드 단위로 계산한 값을 단순하게 나타내는 논리적 구조이다. 때문에 실제값을 얻으려면 로우가 필요하다. 로우를 얻기 위해선 DataFrame이 필요하다. 따라서 DataFrame을 통하지 않으면 외부에서 컬럼에 접근할 수 없다. DataFrame에서 컬럼 내용을 알기 위해선 스파크 트랜스포메이션을 사용해야 한다.

## 2.1 컬럼

```python
from pyspark.sql.functions import col, column

# 컬럼을 생성하고 참조할 수 있는 방법
col("columnName")
column("columnName")

# 명시적 컬럼 참조
# col 메서드를 사용해 명지적으로 컬럼을 정의하면 
# 스파크는 분석기 실행 단계에서 컬럼 확인 절차를 생략한다
df.col("count")
```

컬럼은 컬럼명을 카탈로그에 저장된 정보와 비교하기 전까지는 알 수 없다. 분석기 동작 단계에서 컬럼과 테이블을 분석한다.

## 2.2 표현식

컬럼은 표현식이다. 표현식은 DataFrame 레코드의 여러 값에 대한 트랜스포메이션 집합이다. 표현식은 expr 함수를 이용해 사용할 수 있다. 이 함수를 사용해 DataFrame의 컬럼을 참조할 수 있다. expre(”someCol”)과 col(”someCol”)은 동일한 동작을 한다.

### 표현식으로 컬럼 표현

컬럼은 표현식의 일부 기능을 제공한다. expr 함수 인수로 표현식을 사용하면 표현식을 분석해 트랜스포메이션과 컬럼 참조를 알아내고 다음 트랜스포메이션에 컬럼 참조를 전달할 수 있다.

컬럼과 컬럼의 트랜스포메이션은 파싱된 표현식과 동일한 논리적 실행 계획으로 컴파일된다. 예를 들어 아래 코드의 경우

```python
(((col("someCol") + 5) * 200) - 6) < col("otherCol")

# 위 코드는 아래와 같다
from pyspark.sql functions import expr
expr("(((someCol + 5) * 200) - 6) < otherCol")
```

다음과 같은 논리적 트리(DAG이다)를 같는다.
![logical tree](/img/2024-04-27-spark-definitive5/img.png)

### DataFrame 컬럼에 접근하기

DataFrame의 columns 속성을 이용해 컬럼에 접근할 수 있다.

```python
spark.read.json("/2015-summary.json").columns
```

# 3. 레코드와 로우

스파크는 레코드를 Row 객체로 표현한다. Row 객체는 내부적으로 바이트 배열을 가지는데, 이 배열 인터페이스는 오직 컬럼 표현식으로만 다룰 수 있다. DataFrame을 사용해 드라이버에 개별 로우를 반환하는 명령은 한 개 이상의 Row 타입을 반환한다.

```python
# first 메서드로 DataFrame의 로우를 확인한다.
df.frist()
```

## 3.1 로우 생성하기

각 컬럼의 해당하는 값을 순서대로 명시해 Row 객체를 생성할 수 있다. 순서가 중요한 이유는 Row 객체가 스키마 값을 가지고 있지 않기 때문이다.

```python
from pyspark.sql import Row
my_row = Row("hello", None, 1, False)

my_row[0] # hello 에 접근
my_row[1[ # None 에 접근
```

# 4. DataFrame의 트랜스포메이션

DataFrame을 다루는 작업은 다음과 같이 나눌 수 있다.

- 로우나 컬럼 추가
- 로우나 컬럼 제거
- 로우를 컬럼으로, 컬럼을 로우로 변환
- 컬럼값을 기준으로 로우 순서 변경

## 4.1 DataFrame 생성하기

원시 데이터 소스에서 DataFrame을 생성할 수 있다.

```python
# 원시 데이터소스에서 DataFrame을 생성하는 방법
df = spark.read.json("/2015-summary.json")
df.createOrReplaceTempView("df_table")

# Row 객체를 가진 Seq 타입을 직접 변환해 생성하는 방법
from pyspark.sql import Row
from pyspark.sql.types import StructField, StructType, StringType, LongType

my_manual_schema = StructType([
    StructField("some", StringType(), True),
    StructField("col", StringType(), True),
    StructField("names", LongType(), False)
])
my_row = Row("Hello", None, 1)
my_df = spark.createDataFrame([my_row], my_manual_schema)
my_df.show()
```

## 4.2 select와 selectExpr

DataFrame을 다룰 때 SQL이나 문자열 컬럼을 받는 메서드를 사용할 수 있다.

```python
from pyspark.sql.functions import expr, col, column

df = spark.read.json("/2015-summary.json")
df.createOrReplaceTempView("df_table")

df.select("DEST_COUNTRY_NAME", "ORIGIN_COUNTRY_NAME").show(2)

# 컬럼을 참조하는 다양한 방법
# 다만, 컬럼 객체를 이용할 경우, 문자열을 이용한 참조는 같이 사용할 수 없다
df.select(
	expr("DEST_COUNTY_NAME"),
	col("DEST_COUNTRY_NAME"),
	column("DEST_COUNTRY_NAME"),
	expr("DEST_COUNTRY_NAME AS destination")
).show(2)

# 위 코드와 같은 동작을 하는 sql
-- SQL
SELECT DEST_COUNTRY_NAME, ORIGIN_COUNTRY_NAME FROM df_table LIMIT 2
```

selectExpr 메서드는 새로운 DataFrame을 생성하는 복잡한 표현식을 간단히 만든다.

```python
df.selectExpr(
    "*",
    "(DEST_COUNTRY_NAME = ORIGIN_COUNTRY_NAME) as withinCountry"
).show(2)

# 위 코드와 같은 기능을 하는 SQL
SELECT *, (DEST_COUNTRY_NAME = ORIGIN_COUNTRY_NAME) as withinCountry
FROM df_table
LIMIT 2

df.selectExpr("avg(count)").show(2)

# 위 코드와 같은 기능을 하는 SQL
SELECT avg(count) FROM df_table LIMIT 1
```

## 4.3 스파크 데이터 타입으로 변환하기

명시적인 값을 스파크에 전달해야 할 때는 literal을 사용하면 된다. 리터럴은 프로그래밍 언어의 리터럴값을 스파크가 이해할 수 있는 값으로 변환한다.

```python
import pyspark.sql.functions import lit

df.select(expr("*"), lit(1).alias("One")).show(2)

# 위 코드와 같은 기능을 하는 SQL
SELECT *, 1 as One FROM df_table LIMIT 2
```

## 4.4 컬럼 추가하기

withColumn 메서드를 이용하면 DataFrame에 신규 컬럼을 추가할 수 있다.

```python
# withColumn(사용할 컬럼명, 값을 생성할 표현식)

# 컬럼을 추가할 수 있다
df.withColumn("withinColumn", expr("ORIGIN_COUNTRY_NAME == DEST_COUNTRY_NAME")).show(2)

# 컬럼명을 변경할 수 있다
df.withColumn("withinColumn", expr("DEST_COUNTRY_NAME")).columns
```

## 4.5 컬럼명 변경하기

```python
df.withColumnRenamed("DEST_COUNTRY_NAME", "dest").columns
```

## 4.6 예약 문자와 키워드

문자열이 아닌 표현식으로 칼럼을 참조할 때 예약 문자(공백, ‘-’ 등)가 존재한다면 백틱(`)을 이용해야 한다.

```python
# 첫 번째 인수는 문자열이라 백틱이 필요 없다. 
df.withColumn(
	"This Long Column-name",
	expr("ORIGIN_COUNTRY_NAME")
)

# 표현식이라 백틱이 필요하다
df.selectExpr(
	"`This Long column-name` as `new col`"
).show(2)
```

## 4.7 대소문자 구분

스파크는 대소문자를 구분하지 않지만, 아래 설정을 통해 대소문자를 구분하게 할 수 있다

```python
set spark.sql.caseSensitive true
```

## 4.8 컬럼 제거하기

drop을 이용해 컬럼을 제거할 수 있다.

```python
df.drop("col1", "col2")
```

## 4.9 컬럼의 데이터 타입 변경

cast 메서드를 이용해 데이터 타입을 변환할 수 있다.

```python
df.withColumn("count2", col("count").cast("string"))

# 위 코드와 같은 기능을 하는 SQL
SELECT *, cast(count as string) AS count2 FROM df_table
```

## 4.10 로우 필터링하기

where나 filter를 이용해서 특정 조건을 만족하지 않는 로우를 걸러낼 수 있다. 

```python
df.filter(col("count") < 2).show(2)
df.where("count < 2").show(2)

# 위 코드와 같은 기능을 하는 SQL
SELECT * FROM df_table WHERE count < 2 LIMIT 2

# 여러 조건으로 필터링을 하는 경우
df.where(col("count") < 2).where(col("ORIGIN_COUNTRY_NAME") != "Croatia").show(2)
```

## 4.11 고유한 루오 얻기

distinct 메서드를 이용하면 모든 로우에서 중복 데이터를 제거할 수 있다.

```python
df.select("ORIGIN_COUNTRY_NAME", "DEST_COUNTRY_NAME").distinct().count()

# 위 코드와 같은 기능을 하는 SQL
SELECT COUNT(DISTINCT(ORIGIN_COUNTRY_NAME, DEST_COUNTRY_NAME)) FROM df_table
```

## 4.12 무작위 샘플 만들기

sample 메서드를 이용해 무작위 샘플 데이터를 만들 수 있다. 샘플 데이터를 만들 때 표본 데이터 추출 비율과 복원 추출(sample with replacement)와 비복원 추출(sample without replacement) 사용 여부를 선택할 수 있다

```python
seed = 5
with_replacement = False
fraction = 0.5
df.sample(withReplacement, fraction, seed).count()
```

## 4.13 임의 분할하기

임의 분할은 원본 DataFrame을 임의 크기로 분할할 때 사용된다. 

```python
# seed라 표현된 파라미터 값을 임의의 숫자로 변경하고 사용해야 한다
# 배열로 분할할 비율을 설정해야 한다. 합은 1이 되야 한다.
# 분할 비율을 설정하지 않으면 0,25, 0.75 비율로 분할된다.
data_frames = df.randomSplit([0.25, 0.75], seed)
data_frames[0].show()
```

## 3.14 로우 합치기와 추가하기

데이터프레임은 불변이기 때문에 레코드를 추가하기 위해선 원본과 새로운 데이터프레임은 union 해야 한다. 또 한, union 하는 두 데이터프레임은 같은 스키마, 같은 컬럼 수를 가져야 한다.

```python
from pyspark.sql import Row

schema = df.schema
new_rows = [
    Row("new Country", "Other Country", 5),
    Row("new Country 2", "Other Country 2", 1)
]
parallelized_rows = spark.sparkContext.parallelize(new_rows)
new_df = spark.createDataFrame(parallelized_rows, schema)

df.union(new_df)\
    .where("count = 1")\
    .where(col("ORIGIN_COUNTRY_NAME") != "United States")\
    .show()
```

## 4.15 로우 정렬하기

sort, orderBy 메서드를 이용해 로우를 정렬할 수 있다.

```python
df.sort("count").show(5)
df.orderBy(expr("count desc")).show(2)
df.orderBy(count("count").desc()).show(2)
```

정렬 시 null을 어디에 표시할지는 asc_nulls_first, desc_nulls_first, asc_nulls_last, desc_nulls_last 메서드를 사용해 정할 수 있다.

트랜스포메이션을 처리하기 전에, 성능 최적화를 위해 파티션별로 정렬을 수행할 수도 있다.

```python
spark.read.json("/2015-summary.json").sortWithinPartitions("count")
```

## 4.16 로우 수 제한하기

limit 메서드를 이용하면 표시할 로우 수를 제한할 수 있다.

```python
df.limit(5).show

# 위 코드와 같은 기능을 하는 SQL
SELECT * FROM df_table LIMIT 5
```

## 4.17 repartition과 coalesce

필터링하는 컬럼을 기준으로 데이터를 분할해서 최적화할 수 있다. repartition 메서드는 전체 데이터를 셔플한다. 향후 사용할 파티션 수가 현재 파티션 수보다 많거나 컬럼을 기준으로 파티션을 만드는 경우에만 사용한다.

```python
df.repartition(5)

# 자주 필터링 되는 컬럼을 기준으로 파티션을 재분배
df.repartition(col("DEST_COUNTRY_NAME"))

# 파티션 수를 5로 지정
df.repartition(5, col("DEST_COUNTRY_NAME"))
```

coalesce는 전체 데이터를 셔플하지 않고 파티션을 병합할 때 사용한다.

```python
df.repartition(5, col("DEST_COUNTRY_NAME")).coalesce(2)
```

## 4.18 드라이버로 로우 데이터 수집하기

스파크는 드라이버에서 클러스터 상태 정보를 유지한다. 로컬 환경에서 데이터를 다루러면 드라이버로 데이터를 수집해야 한다.

드라이버로 데이터를 수집하는 연산 종류는 다음과 같다.

```python
collect_df = df.limit(10)
collect_df.take(5) # 상위 N개 로우를 반환한다.
collect_df.show() # 여러 로우를 보기 좋게 출력한다.
collect_df.show(5, take)
collect_df.collect() # 전체 데이터프레임의 모든 데이터를 수집한다
collect_df.toLocalIterator() # 데이터셋의 파티션을 차례로 반복 처리한다
```

출처 - [스파크 완벽 가이드](https://product.kyobobook.co.kr/detail/S000001810100)