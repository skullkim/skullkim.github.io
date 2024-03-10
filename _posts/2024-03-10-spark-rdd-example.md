---
layout:       post
title:        "아파치 스파크 RDD 문법 예제"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- apache spark
---

- 예제 1: 기본 문법

```python
import pyspark

test_file = "file:///home/jovyan/work/sample/helloWorld.txt"
# test_file 내용:
# hello world
# hello world
# hello world
# hello world
# hello world
# hello world

# 기존에 존재하는 spark context 객체가 있으면 반환하고, 없으면 만들어서 반환한다.
spark_context = pyspark.SparkContext.getOrCreate();

# spark context를 textFile() 메서드를 이용해서 RDD로 만든다.
text_file = spark_context.textFile(test_file)

counts = text_file.flatMap(lambda line: line.split(" ")) \ # text를 라인 별로 split한다
    .map(lambda word: (word, 1)) \ # 각자의 RDD를 tuple로 만든다.
    .reduceByKey(lambda a, b: a + b) # 각 튜블을 읽어서 셔플링을 하고, 같은 키의 밸류를 합한다

# collect는 RDD 파티션에 있는 데이터들을 모아서 하나의 리스트로 반환한다.
print(counts.collect())
# output: [('hello', 6), ('world', 6)]

# text_file.flatMap(lambda line: line.split(" ")) 
	# output: ['hello', 'world', 'hello', 'world', 'hello', 'world', 'hello', 'world', 'hello', 'world', 'hello', 'world']
# .map(lambda word: (word, 1))
	# output: [('hello', 1), ('world', 1), ('hello', 1), ('world', 1), ('hello', 1), ('world', 1), ('hello', 1), ('world', 1), ('hello', 1), ('world', 1), ('hello', 1), ('world', 1)]
```

- 예제 2: 기본 문법

```python
import collections
import pyspark

test_file = "file:///home/jovyan/work/sample/grade.txt"
# test_file 내용:
# tom 70
# sara 80
# joon 100
# kevin 90
# John 90

spark_context = pyspark.SparkContext.getOrCreate()

text_file = spark_context.textFile(test_file)

# split을 하면서 grade만 가져온다
grade = text_file.map(lambda line: line.split(" ")[1])

# grade의 각 unique value가 존재하는 횟수를 카운트해서 딕셔너리로 변환한다.
# 각 요소의 값은 키로 사용되고, 요소의 존재 횟수가 값이 된다.
# output: defaultdict(<class 'int'>, {'70': 1, '80': 1, '100': 1, '90': 2})
grade_count = grade.countByValue()

# dictionary의 각 item을 뽑아서 2 번째 value인 count 값을 기준으로 내림차순 정리
for grade, count in sorted(grade_count.items(), key=lambda item: item[1], reverse=True):
    print(f"{grade}: {count}")
    
# output:
# 90: 2
# 70: 1
# 80: 1
# 100: 1
```

- 예제 3: key, value 조작

```python
import pyspark
from operator import add

spark_context = pyspark.SparkContext.getOrCreate()

from operator import add
# parallelize()는 로컬 컬렉션을 RDD로 변환할때 사용한다.
rdd = spark_context.parallelize([("a", 1), ("b", 1), ("a", 1)])
# 키를 기준으로 reduce 연산을 수행하되 add 로 수행한다.
sorted(rdd.reduceByKey(add).collect())
# output:
# [('a', 2), ('b', 1)]

rdd = spark_context.parallelize([("a", 1), ("b", 1), ("a", 1)])
# reduce 연산이 아닌, 키를 기준으로 grouping 수행
# 그 후 각 원소의 value값에 대해 map연산을 실행. value값에 대해 len 연산을 수행한다.
# key값은 변경시키지 않는다.
sorted(rdd.groupByKey().mapValues(len).collect())
# output: [('a', 2), ('b', 1)]

# 각 원소의 value 값을 list로 만든다
sorted(rdd.groupByKey().mapValues(list).collect())
# output: [('a', [1, 1]), ('b', [1])]

tmp = [('a', 1), ('b', 2), ('1', 3), ('d', 4), ('2', 5)]
# key를 기준으로 정렬
spark_context.parallelize(tmp).sortByKey().collect()
# output: [('1', 3), ('2', 5), ('a', 1), ('b', 2), ('d', 4)]

# rdd의 key 또는 value 만 가져온다
rdd = spark_context.parallelize([("a", 1), ("b", 1), ("a", 1)])
rdd.keys().collect() # output: ['a', 'b', 'a']
rdd.values().collect() # output: [1, 1, 1]

# join, rightOuterJoin, leftOuterJoin, cogroup, subtractByKey 
x = spark_context.parallelize([("a", 1), ("b", 4)])
y = spark_context.parallelize([("a",2), ("a", 3)])
sorted(x.join(y).collect())

# cogroup: 두 개의 RDD에 동일한 키가 있을 경우, 해당 키에 대한 값들을 모두 
# 그룹화해서 튜플로 반환
x.cogroup(y)

# subtractByKey: 두 RDD를 결합하고 키를 기준으로 subtractByKey()를 
# 호출한 RDD에만 존재하는 값을반환한다.
x.subtractByKey(y)
```

- 예제 4: csv 파일을 읽어서 평균 구하기

```python
import pyspark

spar_context = pyspark.SparkContext.getOrCreate()
test_file = "file:///home/jovyan/work/sample/house_price.csv"

def parse_line(line: str):
	city, price, count = line.split(',')
	return (int(price), int(count))

lines = spark_context.textFile(test_file)
price_count = lines.map(parse_line)

sum_of_count = price_count.mapValues(lambda count: (count, 1))\
	.reduceByKey(lambda a, b: (int(a[0]) + int(b[0]), int(a[1]) + int(b[1])))
	
avg_by_count = sum_of_count.mapValues(lambda total_count: int(total_count[0]) / total_count[1])
results = avg_by_count.collect()
print(results)
```

- 예제 5: filter, max, min

```python
import pyspark

spark_context = pyspark.SparkContext.getOrCreate()
test_file = "file:///home/jovyan/work/sample/temperature.csv"

def get_data(line, header):
    if line != header:
        col = line.split(',')
        city = col[6].strip("\"")
        avg_temp_fahr = col[4]
        yield (city, avg_temp_fahr)
 
lines = spark_context.textFile(test_file)
header = lines.first()
# get_data()는 city와 avg_temp_fahr만을 반환한다
parsed_line = lines.flatMap(lambda line: get_data(line, header))
# avg_temp_fahr이 "NA"가 아닌 데이터만 가져온다.
filtered_line = parsed_line.filter(lambda x: "NA" not in x[1])

# 각 도시의 최소 온도
min_temp = filtered_line.reduceByKey(lambda x, y: min(float(x), float(y)))
final_list = min_temp.collect()
for city, temperature in final_list:
    print(f"{city}: {temperature}")

print("------------------------")

# 각 도시의 최대 온도
max_temp = filtered_line.reduceByKey(lambda x, y: max(float(x), float(y)))
final_list = max_temp.collect()
for city, temperature in final_list:
    print(f"{city}, {temperature}")
```

- 예제 6: map, flatmap

```python
# faltmap은 하나의 원소가 array, list 또는 어떠한 컬랙션일 경우
# 그 원소를 flatten 해서 연산을 적용한다
import pyspark

spark_context = pyspark.SparkContext.getOrCreate()

rdd = spark_context.parallelize([("name", "joe,sarah,tom"), ("car", "hyundai")])
result = rdd.map(lambda x: x[1].split(","))
result.collect()
# output: [['joe', 'sarah', 'tom'], ['hyundai']]

rdd = spark_context.parallelize([("name", "joe,sarah,tom"), ("car", "hyundai")])
result = rdd.flatMap(lambda x: x[1].split(","))
result.collect()
# output: ['joe', 'sarah', 'tom', 'hyundai']
```

출처 - [실리콘밸리 엔지니어에게 배우는 파이썬 아파치 스파크](https://www.inflearn.com/course/%EC%8B%A4%EB%A6%AC%EC%BD%98%EB%B0%B8%EB%A6%AC-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%EC%95%84%ED%8C%8C%EC%B9%98-%EC%8A%A4%ED%8C%8C%ED%81%AC/dashboard)