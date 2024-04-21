---
layout:       post
title:        "3. 스파크 기능 둘러보기"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- apache spark
- 스파크 완벽 가이드
---

스파크는 저수분 API, 구조적 API, 추가 기능을 제공하는 표준 라이브러리로 구성되어 있다.
![spark structure](/img/2024-04-17-spark-definition3/img.png)

# 1. 운영용 애플리케이션 실행하기

spark-submit 명령어를 사용하면 대화형 셸에서 개발한 프로그램을 운영용 애플리케이션으로 전환할 수 있다. spark-submit 명령은 코드를 클러스터에 전송하고 실행시키는 역할을 한다. 스파크 애플리케이션은 standalone, 메소스, yarn 클러스터 매니저를 이용해 실행된다.

# 2. Dataset: 타입 안전성을 제공하는 구조적 API

Dataset API는 정적 타입 코드를 지원하기 위해 고안된 구조적 API이다. 그 때문에 파이썬과 R에서는 사용할 수 없다.

DataFrame은 테이블형 데이터를 Row 타입으로 구성해 보관하는 분산 컬렉션이다. DataSet API는 DataFrame의 레코드를 사용자가 자바나 스칼라로 정의한 클래스에 할당하고 컬렉션으로 다룰 수 있는 기능을 제공한다. DataSet API는 타입 안전성을 지원하기에 잘 정의된 인터페이스로 상호작용하는 대규모 애플리케이션 개발에 유용하다.

Dataset 클래스는 내부 객체의 데이터 타입을 매개변수로 사용한다. 이 타입은 분석된 뒤 Dataset 표 형식 데이터에 적합한 스키마 생성에 사용된다.

Dataset은 collect, take 메서드를 호출하면 DataFrame을 구성하는 row 타입 객체가 아닌 Dataset에 매개변수로 지정한 타입 객체를 반환하기에 코드 변경 없이 타입 안전성을 보장한다.

# 3. 구조적 스트리밍

스크림 처리용 고수준 API이다. 구조적 스트리밍을 사용하면 배치 처리용 코드를 약간 수정해 스트리밍을 실행하고, 지연시간을 줄일 수 있다. 배치 코드를 스트리밍 데이터로 바꾸는 예시는 다음과 같다.

```python
# 배치 코드
static_data_frame = spark.read.format("csv")\
	.option("header", "true")\
	.option("inferSchema", "true")\
	.load("/data/retail-data/*.csv")
static_schema = static_data_frame.schema

static_data_frame.createOrReplaceTempView("reatil_data")
static_data_frame.selectExpr(
		"CustomerId",
		"(UnitPrice * Quantity) as total_cost",
		"InvoiceDate")\
	.groupBy(
		# 윈도우 함수는 집계 시에 시계열 컬럼을 기준으로 각 날짜에 대한 전체 데이터를 가지는
		# 윈도우를 구성한다
		col("CustomerId"), window(col("InvoiceDate"), "1 day"))\
	.sum("total_cost")
	.show(5)
	
	# 스트리밍 코드
	streaming_data_frame = spark.readStream\
		.schema(static_schema)
		.option("maxFilesPerTrigger", 1)\
		.format("csv")\
		.option("header", "true")\
		.load("/data/retail-data/*.csv")
	
	streaming_data_frame.isStreaming # DataFrame 유형이 스트리밍이면 true 반환
```

# 4. 저수준 API

스파크는 RDD를 통해 자바, 파이썬 객체를 다루는 데 필요한 다양한 기본 기능을 제공한다. DataFrame은 RDD 기반으로 만들어졌기에 분산처리를 위해 저수준 명령으로 컴파일된다. RDD 대신 구조적 API를 사용하는 것이 좋지만 RDD를 사용하면 DataFrame보다 더 세밀한 제어가 가능하다. RDD 사용 예시는 다음과 같다

- 드라이버 시스템 메모리에 저장된 원시 데이터 병렬 처리
- 비정형데이터, 정제되지 않은 원시 데이터 처리

출처 - [스파크 완벽 가이드](https://product.kyobobook.co.kr/detail/S000001810100)