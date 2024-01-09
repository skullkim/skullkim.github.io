---
layout:       post
title:        "3장. 함수 정의와 호출"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- kotlin
- 코틀린인액션
---

# 1. 코틀린에서 컬렉션 만들기

코틀린은 자체 컬렉션을 가지고 있지 않고 자바의 컬렉션을 그대로 사용한다. 이 때문에 자바 코드와 상호작용하기가 훨씬 쉽다. 다만, 코틀린에서는 자바보다 더 많은 기능을 쓸 수 있다.

```kotlin
val set = hashSetOf(1, 7, 53) // create hash set
val list = arrayListOf(1, 7, 13) // create array list
println(list.last()) // list의 마지막 원소를 가져온다
println(list.max()) // list의 원소 중 최댓값을 가져온다
val map = hashMapOf(1 to "one", 7 to "seven") // create hash map
```

# 2. 함수를 호출하기 쉽게 만들기

아래와 같은 함수가 있다고 해보자. 이 함수는 자바 스타일로 작성한 함수이다.

```kotlin
fun <T> joinToString (
    collection: Collection<T>,
    separator: String,
    prefix: String,
    postfix: String
): String {
    val result = StringBuilder(prefix)

    for ((index, element) in collection.withIndex()) {
        if (index > 0) {
            result.append(separator)
        }
        result.append(element)
    }

    result.append(postfix)
    return result.toString()
}

println(joinToString(listOf(1, 2, 3), "; ", "(", ")"))
```

함수를 이런 식으로 정의해 사용하면 다음과 같은 문제가 발생한다.

- 기능은 같아야 하지만 불필요한 인자가 있을 경우 오버 로딩을 해야 한다. 이는 중복을 야기한다.
- 각 파라미터가 어떤 역할을 하는지 함수 시그니처를 보기 전까지 알 수 없다.

이 문제는 코틀린이 제공하는 인자에 이름을 붙일 수 있는 기능과 디폴트 파라미터 값으로 해결할 수 있다.

```kotlin
fun <T> joinToString (
    collection: Collection<T>,
    separator: String = ", ", // 디폴트값 지정
    prefix: String = "",
    postfix: String = ""
): String {
   ...
}

// 인자에 이름을 명시할 수 있다
println(joinToString(listOf(1, 2, 3), separator = "; ", prefix = "(", postfix = ")"))
// 디폴트값이 있는 인자는 생략 가능하다.
println(joinToString(listOf(1, 2, 3), separator = "; ", prefix = "("))
// 인자 순서가 맞지 않는 상태로, 중간 인자를 생략하려면 생략하지 않을 인자 이름을 명시해야 한다
println(joinToString(listOf(1, 2, 3), postfix = ")"))
```

# 3. 정적인 유틸리티 클래스 없애기: 최상위 함수와 프로퍼티

자바로 코드를 작성하다 보면 다양한 정적 메서드를 모아두는 역할만 담당하는 유틸리티 클래스를 만들게 된다. 코틀린은 함수나 프로퍼티를 직접 소스 파일의 최상위 수준에 위치시킬 수 있기에 이러한 불필요한 클래스를 없앨 수 있다.

```kotlin
package strings

//아래와 같이 선언해 사용할 수 있다.
fun joinToString(...): String {...}
val opCount = 0
```

JVM은 클래스 안에 들어있는 코드만을 실행할 수 있기 때문에 컴파일러는 이 파일을 컴파일할 때 새로운 클래스를 정의한다. 만약 이 클래스 이름을 바꾸고 싶다면, 파일에 @JvmName 애노테이션을 사용하고 원하는 이름을 명시하면 된다.

최상위에 프로퍼티를 선언한 경우 다른 프로퍼티처럼 getter, setter를 통해 접근한다. val로 선언했다면 getter, var로 선언했다면 getter와 setter가 모두 생성된다. 만약 const 변경자를 사용한다면 (const val a = 1) 프로퍼티는 public static final 필드로 컴파일된다(원시타입과 String 타입만 가능하다).

# 4. 메서드를 다른 클래스에 추가: 확장 함수와 확장 프로퍼티

## 4.1 확장 함수

확장 함수(extension function)이란 어떤 클래스의 멤버 메서드인 것처럼 호출 가능하지만 클래스 밖에서 선언된 함수를 의미한다. 확장 함수는 JVM 언어로 작성된 클래스라면 모두 가능하다. 코틀린을 기존 자바 프로젝트에 통합하는 경우 코틀린으로 직접 변환할 수 없거나 미처 변환하지 않은 기존 자바 코드를 처리할 때 유용한다.

```kotlin
package stirngs

// 확장 함수를 만들기 위해선 함수 이름 앞에 그 함수가 확장할 클래스 이름을 덧붙이면 된다.
// 클래스 이름을 수신 객체 타입(reciever type), 확장 함수가 호출되는 대상이 되는 값을 수신 객체(receiver object)라 한다.
fun String.lastChar(): Char = this.get(this.length - 1) // String이 수신 객체 타입, this가 수신 객체
```

확장 함수 안에서는 private 이나 protected 멤버를 사용할 수 없다. 때문에 캡슐화를 깨지 않는다.

확장 함수를 사용하기 위해선 그 함수를 임포트해야 한다. 같은 이름의 확장 함수가 둘 이상일 때 이름이 충돌하는 것을 막기 위해서이다. 확장 함수를 임포트하는 방법은 다음과 같다.

```kotlin
import strings.lastChar
"a".lastChar()

import strings.*
"a".lastChar()

// as를 사용하면 함수를 다른 이름으로 부를 수 있다. 이를 통해 이름 충돌을 막을 수 있다.
import strings.lastChar as last
"a".last()
```

확장 함수를 사용하면 위에서 예시로 든 joinToString을 다음과 같이 사용할 수 있다.

```kotlin
fun <T> Collection<T>.joinToString (
    separator: String = ", ", // 디폴트값 지정
    prefix: String = "",
    postfix: String = ""
): String {
    val result = StringBuilder(prefix)

    for ((index, element) in this.withIndex()) {
        if (index > 0) {
            result.append(separator)
        }
        result.append(element)
    }

    result.append(postfix)
    return result.toString()
}

val list = listOf(1, 2, 3)
println(list.joinToString(separator = "; ", prefix = "(", postfix = ")"))
```

다만 확장 함수는 오버리이드할 수 없다. 확장 함수를 첫 번째 인자가 수신 객체인 정적 자바 메서드로 컴파일 하기 때문이다. 즉, 확장 함수를 호출할 때 수신 객체로 지정한 변수의 정적 타입에 의해 어떤 확장 함수가 호출될지 결정된다.

## 4.2 확장 프로퍼티

확장 프로퍼티를 사용하면 기존 클래스 객체에 대한 프로퍼티 형식의 구문을 사용할 수 있는 API를 추가할 수 있다. 확장 프로퍼티는 아무 상태도 가질 수 없다. 확장 프로퍼티 역시 일반적인 프로퍼티와 같지만 수신 객체 클래스가 추가됐다.

확장 프로퍼티는 뒷받침하는 필드(프로퍼티에 값을 저장하기 위한 필드)가 없어서 최소한 getter는 꼭 정의해야 한다.

```kotlin
val java.lang.StringBuilder.lastChar: Char
    get() = get(length - 1)

val java.lang.StringBuilder.lastChar: Char
    get() = get(length - 1)
    set(value: Char) {
        this.setCharAt(length - 1, value)
    }
```

# 5. 컬랙션 처리: 가변 길이 인자, 중위 함수 호출, 라이브러리 지원

이전 장에서도 말했지만 코틀린은 자바 컬렉션을 그대로 사용하면서 새로운 기능을 추가했다. 이것이 가능한 이유는 위에서 설명한 확장 함수를 사용했기 때문이다. 

컬렉션 처리를 통해 알아볼 수 있는 코틀린의 특성은 다음과 같다.

- vararg 키워드를 사용하면 호출 시 인자 개수가 달라질 수 있는 함수를 정의할 수 있다.
    - 원하는 원소를 개수만큼 넣어 리스트를 생성하는 함수 형태는 다음과 같다.
    
    ```kotlin
    // vararg는 가변 길이 인자를 선언할 때 사용한다
    public fun <T> listOf(vararg elements: T): List<T> = if (elements.size > 0) elements.asList() else emptyList()
    
    // 만약 배열에 들어있는 원소를 가변 길이 인자에 넘기고 싶을 때는 스프레드(spread) 연산자를 사용해야 한다.
    fun main(args: Array<String>) {
    	// *가 스프레드 연산자
    	val list = listOf(*args)
    }
    ```
    
- 중위(infix) 함수 호출 구문을 사용하면 인자가 하나뿐이 메서드를 간편하게 호출할 수 있다.

```kotlin
// to는 중위 호출이라는 특별한 방식으로 호출한 일반 메서드이다.
// 중위 호출은 수신 객체와 유일한 메서드 인자 사이에 메서드 이름을 넣는다. 
val map = mapOf(1 to "one")

// 호출을 허용하고 싶다면 infix 변경자를 함수 선언 앞에 추가해야 한다.
infix fun <A, B> A.to(that: B): Pair<A, B> = Pair(this, that)
```

- 구조 분해 선언(destructuring declaration)을 사용하면 복합적인 값을 분해해서 여러 변수에 나눠 담을 수 있다.

```kotlin
// 위 예시로 사용한 to 함수는 Pair 객체를 만들어 반환한다
// Pair의 내용으로 두 변수를 즉시 초기화할 수 있다. 이런 기능을 구조 분해 선언(destructuring declaration)이라 한다.
val (number, name) = 1 to "one"
```

# 6. 문자열과 정규식 다루기

코틀린 문자열은 자바와 같지만 여러 확장 함수를 제공해서 표준 자바 문자열을 더 편하게 다룰 수 있게 한다. 예를 들어 자바에서 스트링을 특정 기준으로 나누는 split() 함수의 경우 인자로 정규식을 받지만 타입은 String이라 넘겨야 하는 인자가 기준이 되는 부분 문자열이라는 착각을 불러일으킬 수 있다.

```kotlin
public String[] split(String regex) {
    return split(regex, 0);
}
```

그러나 코틀린은 정규식을 받아야 할 경우 Regex 타입을 받고, 일반 텍스트라면 String을 받아서 구분하기가 쉽다. 추가로 코틀린 정규식 문법은 자바와 같다.

# 7. 코드 다듬기: 로컬 함수와 확장

코틀린에서는 함수에서 추출한 함수를 원 함수 내부에 중첩시킬 수 있다. 이를 통해 문법적으로 부가 비용을 들이지 않고도 깔끔하게 코드를 조작할 수 있다. 로컬 함수는 자신이 속한 바깥 함수의 모든 파라미터와 변수를 사용할 수 있다는 특징이 있다.

```kotlin
fun saveUser(user: User) {
    if (user.name.isEmpty()) {
        throw IllegalArgumentException()
    }
    if (user.address.isEmpty()) {
        throw IllegalArgumentException()
    }

		// save user data
}

// 위 함수와 같은 기능을 하지만 로컬 함수를 사용했다
fun saveUser2(user: User) {
		// 로컬 함수
    fun validate(value: String) {
        if (value.isEmpty()) {
            throw IllegalArgumentException()
        }
    }
    
    validate(user.name)
    validate(user.address)

		// save user data
}
```

출처 - [코틀린 인 액션](https://product.kyobobook.co.kr/detail/S000001804588)