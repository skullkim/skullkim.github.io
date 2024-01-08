---
layout:       post
title:        "2장. 코틀린 기초"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- kotlin
- 코틀린인액션
---

# 1. 함수

- 코틀린에서 if는 문(statement)이 아닌 식(expression)이다.
    - 식(expression)은 값을 만들어 내며 다른 식의 하위 요소로 계산에 참여할 수 있다.
    - 문(statement)은 자신을 둘러싸고 있는 가장 안쪽 블록의 최상위 요소로 존재하며 아무런 값을 만들어내지 않는다.
- 따라서 다음과 같은 동작이 가능하다.

```kotlin
fun max(a: Int, b: Int): Int { // a, b를 비교해서 최댓값을 반환
	return if (a > b) a else b
}
```

- 오직 식 하나로 이루어진 함수는 다음과 같이 표현할 수 있다.

```kotlin
fun max(a: Int, b: Int) = if (a > b) else b // 위 max 함수 예시와 같은 기능을 하는 함수
```

- 본문이 중괄호로 둘러싸인 함수를 블록이 본문인 함수라 한다. 등호화 식으로 이뤄진 함수를 식이 본문인 함수라 한다. 식이 본문인 함수는 반환 타입을 명시하지 않아도 컴파일러가 타입 추론을 해준다.

# 2. 변수

- 타입으로 변수 선언을 시작한다면, 타입을 생략할 경우 변수 선언과 식을 구별할 수 없다. 따라서 코틀린은 val이라는 키워드를 사용해서 변수 선언을 시작하고 변수명 뒤에 타입을 명시하거나 생략한다.

```kotlin
val number: Int = 12
val number = 12

// 초기화 삭이 없다면 반드시 타입을 명시해야 한다
val number: Int
number = 12
```

- 변수 선언 시 다음과 같은 두 가지 키워드를 사용할 수 있다.
    - val(value - 값을 의미): immutable 참조를 저장한다. 초기화 이후 재대입이 불가능하다. 자바의 final에 해당한다. 그러나 어떤 블록이 실행될 때 오직 한 초기화 문장만 실행됨을 컴파일러가 확인할 수 있다면 조건에 따라 val 값을 다른 여러 값으로 초기화할 수도 있다.
        
        ```kotlin
        val message: String
        if (...) {
        	message = "a"
        } else {
        	messsage = "b"
        }
        ```
        
    - var(variable - 변수를 의미): mutable 참조이다. 자바의 일반 변수에 해당한다.
- 어떤 타입을 가진 변수에 다른 타입의 값을 저장하려면 변환 함수를 사용하거나 강제 형 변환을 해야 한다.
- 문자열 템플릿
    - 문자열 템플릿은 변수를 문자열 안에서 사용할 수 있게 해주는 유용한 기능이다. 다음과 같이 사용할 수 있다.
    
    ```kotlin
    val name = "skull"
    println("I'm $name") // output: I'm skull
    // $name님 처럼 변수명 뒤에 한글을 바로 사용하면 컴파일러가 영문자와 한글을 
    // 한꺼번에 식별자로 인식해서 unresolved references 에러가 발생한다.
    // 따라서 ${}를 사용해야 한다.                  
    println("${name}님 반가워요")
    
    println("\$x") // output: $x
    
    // 복잡한 식은 ${}를 사용
    println("I'm ${if (args.size > 0) args[0] else "someone"}")
    ```
    

# 3. 클래스와 프로퍼티

코틑린은 값 객체를 자바보다 더 간결하게 선언할 수 있다.

```kotlin
public class Person {

	private final String name;

	public Person(String name) {
		this.name = name;
	}

	public String getName() {
		return name;
	}
}

// 위 자바 코드를 코틀린으로 이용하면 다음과 같이 변환할 수 있다.
// 이렇게 변환을 하면 public 가시성 변경자(visibility modifier)가 사라진다.
// 코틀린 기본 가시성은 public이다.
class Person(val name: String)
```

## 3.1 프로퍼티

자바에서는 필드와 접근자를 묶어서 프로퍼티(property)라고 한다.코틀린의 프로퍼티는 자바의 필드와 접근자 메서드를 대체한다.

```kotlin
class Person (
	val name: String, // read-only 프로퍼티로, 비공개 필드와 단순한 getter를 만들어낸다
	var isMarried: Boolean // write가 가능한 프로퍼티로, 비곡개 필드, getter, setter를 만들어 낸다
)

// 자바와의 상용법을 비교하면 다음과 같다 (주석이 자바)
val person = Person("Bob", true) // Person person = new Person("Bob", true);
person.name // person.getName();
person.isMarried = false; // person.setIsMarried(false);
```

- 커스텀 접근자. 프로퍼티의 접근자를 직접 작성하 수도 있다.

```kotlin
class Rectangle(val height: Int, val width: Int) {
    
    val isSquare
        get() = (height == width)
}
```

# 4. 패키지

코틀린에서는 여러 클래스를 한 파일에 넣을 수 있고, 파일의 이름도 마음대로 정할 수 있다. 코틀린은 디스크상의 어느 디렉터리에 소스코드 파일을 위치시키든 상관없다. 그럼에도 자바와 같이 패키지별로 디렉터리를 구성하는 것이 좋다. 그래야 자바와 코틀린을 함께 사용할 때 문제가 생기지 않는다.

# 5. 선택 표현과 처리: enum과 when

## 5.1 enum

코틀린에서 enum은 소프트 키워드(soft keyword)이다. enum은 class 앞에 있을 때 특별한 의미를 지니지만 다른 곳에서는 이름에 사용할 수 있다. 반면 class는 키워드이기에 이름으로 사용할 수 없다.

```kotlin
enum class Color (
    val r: Int,
    val g: Int,
    val b: Int
) {
    RED(255, 0, 0),
    ORANGE(255, 165, 0)
    ; // 코틀린에서 유일하게 ';'을 사용하는 부분이다

    fun rgb() = (r * 256 + g) * 256 + b
}

println(Color.RED.rgb())
```

## 5.2 when으로 enum 클래스 다루기

when은 자바 switch에 해당한다. when 역시 if과 같은 식이므로 식이 본문인 함수를 작성할 수 있다. when과 if의 내용이 길어진다면 {}를 활용해 분기 블록을 만들 수 있다. 이 경우 블록의 맨 마지막에 분기의 결괏값을 넣으면 된다.

```kotlin
// 위 예제의 enum Color 사용
fun getColor(color: Color) =
        when (color) {
            Color.RED -> "red"
            Color.ORANGE, Color.YELLOW -> "or" // 한 분기에서 여러 값을 매치 패턴으로 사용할 때 ',' 사용
        }

println(getColor(Color.RED)) // output: red
println(getColor(Color.ORANGE)) // output: or
println(getColor(Color.YELLOW)) // output: or

when (color) {
	Color.Red -> {
			...
			"red"
	} // "red" 반환
}
```

# 5.3 when과 임의의 객체를 함께 사용

코틀린의 when은 분기 조건에 상수뿐만 아니라 임의의 객체를 넣을 수도 있다.

```kotlin
fun mix(c1: Color, c2: Color) = 
    when (setOf(c1, c2)) { // Set 생성
        setOf(Color.RED, Color.YELLOW) -> Color.ORANGE
        else -> throw Exception("Dirty color")
    }
```

# 5.4 인자 없는 when 사용

위 예제는 매번 비교 때마다 setOf()로 객체를 생성한다. 인자가 없는 when 식을 사용하면 불필요한 객체 생성을 막을 수 있다. 

```kotlin
fun mix(c1: Color, c2: Color) =
    when {
        (c1 == Color.RED && c2 == Color.YELLOW) 
                ||(c1 == Color.YELLOW && c2 == Color.RED) -> Color.ORANGE
        else -> throw Exception("Dirty Color")
    }
```

# 5.5 스마트 캐스트: 타입 검사와 타입 캐스트를 조합

스마트 캐스트란 어떤 변수가 원하는 타입인지 일단 is로 검사하고 나면 굳이 변수를 원하는 타입으로 캐스팅하지 않아도 해당 타입으로 선언된 것처럼 사용할 수 있는 기능이다. 따라서 다음과 같은 동작을 할 수 있다.

```kotlin
interface Expr
class Num(val value: Int): Expr // Expr 인터페이스를 implements한다
class Sum(val left: Expr, val right: Expr): Expr

fun eval(e: Expr): Int {
    if (e is Num) {
				// 타입 체크를 한 뒤 명시적으로 캐스팅을 해주지 않아도 된다.
				// 그럼에도 명시적으로 캐스팅을 해주고 싶다면 val n = e as Num 같이 as키워드를 사용하면 된다.
        return e.value
    } else if (e is Sum) {
        return eval(e.right) + eval(e.left)
    }
    throw IllegalArgumentException("Unkown expression")
}
```

스마트 캐스트는 is로 변수에 든 값의 타입을 검사한 뒤, 그 값이 바뀔 수 없는 경우에만 동작한다. 예컨대, 위 예제에서 클래스의 프로퍼티가 val이며 커스텀 접근자를 사용하지 않았다. 커스텀 접근자를 사용하면 해당 프로퍼티에 대한 접근이 항상 같은 값을 내놓는다고 확신하지 못한다.

# 6. 대상을 이터레이션: while과 for 루프

- 코틀린의 while, do..while은 자바와 같다.
- for는 자바의 for-each loop에 해당하는 형태만 존재한다. 때문에 값을 증가, 감소 등의 연산을 하면서 반복하기 위해 downTo, step, until 이란 함수를 사용한다.

```kotlin
val oneToTen = 1..10 // 1 ~ 10까지 수를 가진 변수 선언

// 1 ~ 10 까지 1 씩 증가하며 순환
for (i in 1..10) {
	...
}

// 2 씩 감소시키면서 1이 될때 까지 순회, i 초기 값은 10
for (i in 10 downTo 1 step 2) {
	...
}

// 1 ~ 9 까지 1씩 증가하며 순회
for (i in 1 until 10) {
	...
}
```

- 컬렉션과 for..in 루프를 같이 사용한다면, 다음과 같은 동작들을 할 수 있다

```kotlin
val binaryReps = TreeMap<Char, String>()
for (c in 'A'..'F') {
    binaryReps[c] = Integer.toBinaryString(c.code) // 아스키코드를 2진표현으로 바꾼다
}
// key는 맵의 키값, value는 맵의 키에 대응하는 밸류값
for ((key, value) in binaryReps) {
    ...
}

val list = arrayListOf("10", "11", "1001")
// index는 리스트 원소의 인덱스 번호, element는 리스트의 원소
for ((index, element) in list.withIndex()) {
    ...
}

// 변수 c의 값이 a~z 범위에 존재하면 true 반환
fun isLetter(c: Char) = c in 'a'..'z'
// 변수 c의 값이 0~9 범위에 존재하지 않으면 true 반환
fun isNotDigit(c: Char) = c !in '0'..'9'
```

in 키워드로 인한 비교는 java.lang.Comparable 인터페이스를 구현한, 즉 비교가 가능한 클래스라면 모두 사용할 수 있다. 따라서 다음과 같은 동작도 가능하다.

```kotlin
println("Kotlin" in "Java".."Scala") // String에는 Comparable 구현이 두 문자열을 알파벳 순서로 비교한다
println("Kotlin" in setOf("Java", "Scala") // 집합에 Kotlin이 들어있나
```

# 7. 코틀린의 예외 처리

코틀린의 예외 처리(try, catch, fianlly)는 기본적으로 자바와 같지만 예외를 checked exception와 unchecked exception으로 나누지 않는다. 모두 unchecked exception으로 간주한다. 또 한, try 키워드 역시 if와 같은 식이다. try의 본문은 반드시 {}로 감싸야 하며, try와 catch 모두 식의 마지막 값이 전체 결과이다. 따라서 다음과 같은 방식으로 코드를 작성할 수 있다.

출처 - [코틀린 인 액션](https://product.kyobobook.co.kr/detail/S000001804588)