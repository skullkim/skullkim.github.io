---
layout:       post
title:        "6장. 코틀린 타입 시스템"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- kotlin
- 코틀린인액션
---

# 1. 널 가능성

널 가능성(nullability)는 NullPointerException 오류를 피할 수 있게 돕기 위한 코틀린 타입 시스템 특성이다. 최신 언어들은 널로 인한 문제를 최대한 방지하기 위해 널이 될 수 있는지를 타입 시스템에 추가해서 컴파일러가 여러 가지 오류를 컴파일 시 미리 감지해서 실행 시점에 발생할 수 있는 예외의 가능성을 줄인다.

## 1.1 널이 될 수 있는 타입

코틀린 타입 시스템은 널이 될 수 있는 타입을 명시적으로 지원한다. 널이 될 수 있는 타입은 프로그램 안의 프로퍼티나 변수에 null을 허용하게 만드는 방법이다. 널이 될 수 있는 타입은 널이 될 수 없는 타입을 감싼 래퍼 타입이 아니다. 모든 검사는 컴파일 시점에 수행한다. 따라서 실행 시점에 널이될 수 있는  타입과 널이 될 수 없는 타입의 객체는 같다. 이 때문에 코틑린에서는 널이 될 수 있는 타입을 처리하는 데 별도의 실행 시점 부가 비용이 들지 않는다.

```elixir
// string은 널을 허용하지 않는 String 타입이다.
fun getStringLength(string: String) = string.length

// ERROR: Null can not be a value of a non-null type String
getStringLenght(null)

// null을 허용하기 위해선 타입 뒤에 '?'를 붙이면 된다.
// 어떤 타입이든 타입 이름 뒤에 '?'를 붙이면 null 참조를 저장할 수 있다.
fun getStringLength(string: String?) = string.length
```

널이 될 수 있는 타입의 변수에 대해선 그가 수행할 수 있는 연산이 제한된다. 제한은 다음과 같다.

- ‘변수.메서드()’처럼 메서드를 직접 호출할 수 없다.
- 널이 될 수 있는 값을 널이 될 수 없는 타입의 변수에 대입할 수 없다.
- 널이 될 수 있는 타입의 값을 널이 될 수 없는 타입의 파라미터를 받는 함수에 전달할 수 없다

```elixir
// ERROR: only safe (?.) or non-null asserted(!!.) calls are allowed on a nullable receiver of type String?
fun getStringLength(string: String?) = string.length
getStringLenth(null)
```

널이 될 수 있는 타입은 제약이 많지만, 널과 비교할 수 있다. 일단 널과의 비교를 통해 컴파일러가 널이 아님을 확실한 영역이 있다면, 그 영역에서는 해당 변수를 널이 될 수 없는 값처럼 사용할 수 있다.

```elixir
fun getStringLength(string: String?) = if (string != null) string.length else 0
```

## 1.2 안전한 호출 연산자: ?.

‘?.’연산자는 a?.method()와 같이 사용할 수 있다. 이는 널 검사와 메서드 호출을 한 번의 연산으로 수행한다. 만약 호출하려는 값이 널이 아니라면 일반 메서드 호출처럼 동작하고, 호출하려는 값이 널이라면 널이 결괏값이 된다. 즉, if (a != null) a.method() else null과 같다.

## 1.3 엘비스 연산자: ?:

코틀린은 널 대신 사용할 디폴트 값을 지정할 때 사용할 수 있는 연산자를 제공한다. 이 연산자를 엘비스(elvis - ‘?:’) 연산자라고 한다.

```elixir
fun foo(s: String?) {
	// s가 널이면 ""를 반환한다
	val t: String = s ?: ""
}

fun foo(s: String?) {
	// 코틀린에선 return이나 throw 등 연산도 식이기에 아래와 같이 사용할 수 있다
	val t: String = s ?: throw IllegalArguemntException()
}
```

## 1.4 안전한 캐스트: as?

as를 이용해 타입을 캐스트 하기 전에 is를 통해서 변환 가능한지를 검사할 수도 있다. 또한, 이 방식을 줄여서 ‘as?’ 연산자를 사용해도 된다. ‘as?’ 연산자는 값을 대상 타입으로 변환할 수 없으면 널을 반환한다.

## 1.5 널 아님 단언(not-null assertion): !!

‘!!’를 사용하면 어떤 값이든 널이 될 수 없는 타입으로 바꿀 수 있다. 이는 널이 아님이 확실시되는 상황에 사용할 수 있다. 예컨대, 함수가 값이 널인지를 검사하고 다른 함수 b를 호출한다면, b 안에선 안전하게 그 값을 사용할 수 있음을 인식할 수 없다. 이때, ‘!!’를 사용해 널이 아닌 값을 전달받는다는 사실을 분명히 해서 널 검사를 다시 수행하지 않게 할 수 있다.

```kotlin
fun ignoreNulls(s: String?) {
	val notNullStr: String = s!!
	...
}
```

## 1.6 let 함수

let 함수를 사용하면 원하는 식을 평가해서 널인지를 검사하고, 그 결과를 변수에 넣는 작업을 간단하게 할 수 있다. let을 사용하는 가장 흔한 방식은 nullable  값을 nullable 하지 않은 인자를 받는 함수에 넘기는 경우다.

```kotlin
fun sendEmailTo(email: String) {
    println("send email to ${email}")
}

fun main() {
    val email: String? = "example@gmail.com"
		// it는 email의 값이다
    email?.let { sendEmailTo(it) }
}
```

위 예제의 경우 sendEmailTo()의 email 인자는 nullable 하지 않지만 nullable 한 email 변수를 넘기고 있다. 위와 같이 let을 사용하면 email의 값이 null이 아닌 경우에만 sendEmailTo()를 호출한다.

let은 중첩해서 사용할 수 있지만, 중첩해서 사용하면 코드가 복잡해지기 때문에 이 경우는 if를 사용하는 것이 좋다.

## 1.7 나중에 초기화할 프로퍼티

코틀린은 일반적으로 생성자에서 모든 프로퍼티를 초기화해야 한다. 때문에 초기화 값을 생성자에서 제공하지 못할 경우 nullable 하게 둘 수밖에 없다. 이 문제는 lateinit으로 해결할 수 있다. lateinit은 반드시 var와 함께 사용해야 하며 프로퍼티를 나중에 초기화할 수 있게 해준다.

## 1.8 널이 될 수 있는 타입 확장

Nullable 한 타입에 대해 확장 함수를 정의하면 null 값을 다루는 도구로 활용할 수 있다. 어떤 메서드를 호출하기 전에 객체가 널이 될 수 없다는 것을 보장하는 대신, 확장 함수가 알아서 널을 처리하게 할 수 있다. 예컨대 String? 타입 수신 객체는 다음과 같은 메서드를 제공한다.

```kotlin
@kotlin.internal.InlineOnly
public inline fun CharSequence?.isNullOrBlank(): Boolean {
    contract {
        returns(false) implies (this@isNullOrBlank != null)
    }

    return this == null || this.isBlank()
}

val str: String? = "a"
str.isNullOrBlank()
```

isNullOrBlank()는 안전한 호출(?.) 없이도 수신 객체 타입에 대해 선언된 확장 함수를 호출할 수 있다. Null이 들어와도 적절한 처리를 진행한다. nullable 한 타입에 대해 확장 함수를 정의하면 nullable 한 값에 대해 그 확장 함수를 호출할 수 있다. 이때, 함수 내부의 this는 널이 될 수 있어서 명시적으로 null 검사를 해야 한다. 이 점이 자바와 다르다.

## 1.9 타입 파라키터의 널 가능성

코틀린에서 함수나 클래스의 모든 타입 파라미터는 기본적으로 nullable 하다.

```kotlin
// T는 nullable 하다
fun <T> printHashCode(t: T) {
    println(t.hashCode())
}

printHashCode(null)
```

만약 T가 nullable 한 것을 막고 싶다면, 널이 될 수 없는 타입으로 upper bound를 지정해야 한다.

```kotlin
fun <T: Any> printHashCode(t: T) {
    println(t.hashCode())
}
```

## 1.10 널 가능성과 자바

코틀린은 자바와의 상호운용성을 위해 다음과 같은 방식을 사용한다.

- 애너테이션으로 널 가능성 표기
    - @Nullable String은 코틀린의 String? 과 같다
    - @NotNull String은 코틀린의 String과 같다.
    - 이뿐만 아니라 코틀린은 다양한 의존성에 존재하는 널 가능성 애너테이션을 알아본다.
- 플랫폼 타입
    - 널 가능성 애너테이션이 소스코드에 없다면 코틀린은 이를 플랫폼 타입으로 인식한다. 플랫폼 타입은 널이 될 수 있는지를 알지 못하는 타입을 말한다. 따라서 컴파일러는 모든 연산에 대한 책임을 사용자에게 부여한다. 코틀린은 보통 nullable 하지 않은 값에 대해 널 안전성 검사를 하지 않으면 경고를 표시하지만 플랫폼 타입은 아무런 경고도 하지 않는다. 따라서 자바 API를 다룰 때는 자바 메서드의 문서를 자세히 살펴보고, 그 메서드가 널을 반환한다면 널 검사를 추가해야 한다.
    - 코틀린이 모든 자바 타입을 널이 될 수 있는 타입으로 다루지 않고 플랫폼 타입을 도입한 이유는, 불필요한 널 검사를 줄이기 위해서이다. 모든 타입을 널이 될 수 있는 타입으로 하면 불필요한 널 검사를 해야 한다.

### 상속

코틀린에서 자바 메서드를 오버라이드 할 때, 그 메서드의 파라미터와 반환 타입을 nullable 하게 할지 말지를 결정해야 한다.

```kotlin
// interface
interface StringProcessor {
	void process(String value);
}

// 아래 구현이 모두 가능하다
class StringPrinter: StringProcessor {
	override fun process(value: String) {
		println(value)
	}
}

class NulableStringPrinter: StringProcessor {
	override fun process(value: String?){
		if (value != null) {
			println(value)
		}
	}
}
```

# 2. 코틀린의 원시 타입

## 2.1 원시 타입: Int, Boolean 등

코틀린은 원시 타입과 래퍼 타입을 구분하지 않는다. 항상 같은 타입을 사용한다. 따라서 컴파일 시에 상황에 따라서 알맞은 자바 타입으로 변환된다. 숫자 타입은 가능 한 효율적인 방식으로 표현된다. 자바의 원시 타입으로 표현이 불가능한 경우(컬렉션 등)에만 래퍼 클래스로 표현된다.

## 2.2 널이 될 수 있는 원시 타입: Int?, Boolean? 등

코틀린에서 널이 될 수 있는 원시 타입을 사용하면 그 타입은 자바의 래퍼 타입으로 컴파일된다. 

## 2.3 숫자 변환

코틀린과 자바의 가장 큰 차이 중 하나는 숫자를 변환하는 방식이다. 코틀린은 한 타입의 숫자를 다른 타입의 숫자로 자동 변환하지 않는다. 

```kotlin
val i = 1
val longNumber: Long = i // type mismatch error
```

대신 toByte(), toChar()와 같이 모든 원시 타입(Boolean 제외)에 대한 변환 함수를 제공한다. 이런 함수를 통한 타입 간의 변환은 타입의 표현 범위를 가리지 않는다. 따라서 표현 범위가 큰 타입을 표현 범위가 작은 타입으로 변환할 때 다음과 같은 문제가 발생하기도한다.

```kotlin
 val longValue: Long = Long.MAX_VALUE
 println(longValue.toInt()) // output: -1
```

코틀린은 개발자의 혼란을 피하기 위해 타입 변환은 명시한다. 자바 박스 타입을 비교하는 경우, 두 박스 타입 간의 equals 메서드는 객체 내부의 value를 비교하기 전에 박스 타입이 같은지부터 검사한다. 때문에 실제로 value가 같아도 타입이 다르면 equals()는 false를 반환한다.

```kotlin
// Integer class의 equals 구현은 다음과 같다.
public boolean equals(Object obj) {
    if (obj instanceof Integer) {
        return value == ((Integer)obj).intValue();
    }
    return false;
}

// equals() 구현이 위와 같기 때문에 다음 코드의 결과는 false이다
(new Integer(1)).equals(new Long(1))
```

코틀린은 타입을 명시적으로 변환해야 하기 때문에 다음과 같이 명시적 변환을 해야 제대로 컴파일이 된다.

```kotlin
val x = 1
val list = listOf(1L, 2L, 3L)
// Long 타입으로 명시적 변환
println(x.toLong() in list)

// 명시적 변환을 하지 않으면 Type inference failed가 발생한다.
println(x in list)
```

코틀린은 다음과 같은 숫자 리터럴을 지원한다.

- Long 타입 리터럴 L: 1L
- 표준 부동소수점 표기법을 사용한 Double 타입 리터럴: 0.12, 1.2e10
- Float 타입 리터럴 f or F: 1.2f, 1.2F
- 16진수 리터럴 0x: 0xCA
- 2진수 리터럴 0b or 0B: 0b001

숫자 리터럴을 사용한다면 변환 함수를 호출하지 않아도 된다. 또 한, 숫자 리터럴을 타입이 알려진 변수에 대입하거나 함수에게 인자로 넘기면 컴파일러가 자동으로 변환해 준다. 또 한, 산술연산자는 적당한 타입의 값을 받아들일 수 있게 오버로드되어 있다.

## 2.4 Any, Any?: 최상위 타입

코틀린에서 Any는 자바의 Object와 같은 타입 계층 구조의 최상의 타입이다. 다만 다음과 같은 차이가 존재한다.

- Any는 원시 타입을 포함한 모든 타입의 조상이다.
- Any는 널을 허용하지 않기에 널을 포함해 모든 값을 대입하는 변수를 원하는 Any?를 이용해야 한다.
- Any 내부에는 equals, toString, hashCode가 존재하지만 Object에 존재하는 wait, notify 등의 메서드는 존재하지 않는다. 따라서 필요하다면 java.lang.Object 타입으로 값을 캐스팅해야 한다.

## 2.5 Unit 타입: 코틀린의 void

Unit 타입은 자바의 void와 같은 기능을 한다. 

```kotlin
// 함수에 반환 타입이 없을 경우 다음과 같은 두 표기 중 하나를 사용할 수 있다.
fun f(): Unit { ... }
fun f() { ... }
```

함수 반환 타입이 Unit이고 그 함수가 제네릭 함수를 오버라이드 하지 않으면, 그 함수는 내부에서 자바 void 함수로 컴파일된다. 

Unit과 자바 void의 차이는 Unit은 모든 기능을 갖는 일반적인 타입이고 Unit을 타입 인자로 사용할 수 있다는 것이다. Unit에 속한 값은 단 하나, Unit뿐이다. Unit 타입의 함수는 Unit 값을 묵시적으로 반환한다. 때문에 제네릭 파라미터를 반환하는 함수의 반환값을 Unit으로 사용할 수 있다.

```kotlin
interface Processor<T> {
	fun process():T
}

class NoResultProcessor: Processor<Unit> {

	// 반환값이 Unit이므로 어떤 값을 명시적으로 return 하지 않아도 된다.
	override fun process() {
		...
	}
}
```

자바에서 위와 같은 동작을 java.lang.Void 타입을 사용해서 구현해도 되지만 return null을 명시해야 한다는 점이 다르다. 

코틀린에서 이런 void 대용의 값을 Void가 아닌 Unit이라 칭한 이유는 함수형 프로그래밍 때문이다. 함수형 프로그래밍에서 전통적으로 unit은 ‘단 하나의 인스턴스만 갖는 타입’을 의미한다. 이 유일한 인스턴스의 유무 차이가 자바 void와 코틀린의 Unit을 구분하는 가장 큰 차이다.

## 2.5 Nothing 타입: 이 함수는 결코 정상적으로 끝나지 않는다

결코 성공적으로 값을 돌려주는 일이 없는, ‘반환값’이라는 개념 자체가 의미 없는 함수가 존재한다. 예컨대, 무한 루프를 도는 함수는 결코 값을 반환하고 정상 종료하지 않는다. 이런 함수를 호출하는 코드를 분석할 때, 함수가 정상 종료되지 않음을 알면 유용한다. 이런 경우 Nothing이란 타입을 사용한다.

Nothing은 함수의 반환 타입이나, 반환 타입으로 쓰일 타입 파라미터로만 사용할 수 있다.

```kotlin
fun fail(message: String): Nothing {
	throw new IllegalArgumentException(message)
}
```

# 3. 컬랙션과 배열

## 3.1 널 가능성과 컬랙션

컬랙션을 사용할 때 지정하는 타입은 nullable 할 수 있다(ex - List<Int?>). 이 경우 null이 컬랙션의 원소로 들어갈 수 있다. 여기서 변수 타입의 널 가능성과 타입 파라미터로 쓰이는 타입의 널 가능성의 차이에 유의해야 한다. 변수 타입이 nullable(ex - List<Int?>) 하면 컬랙션이 가진 여러 원소 중 null이 포함될 수 있다는 의미다. 반면 타입 파라미터로 쓰이는 타입이 nullable(List<Int>?) 하다는 것은 컬랙션 자체가 null이 될 수 있다는 의미이다.

코틀린은 nullable한 타입 원소로 이루어진 컬랙션에서 널을 걸러내는 함수를 제공한다.

```jsx
val numbers: List<Int?>
// null이 아닌 원소만 걸러낸다. 반환 타임이 nullable하지 않다.
val validNumbers: List<Int> = numbers.filterNotNull()
```

## 3.2 읽기 전용과 변경 가능한 컬랙션

코틀린 컬랙션은 데이터를 읽고, 쓰는 인터페이스를 분리해 놓았다. 이런 구분은 컬랙션을 다룰 때 사용하는 가장 기초적인 인터페이스에서부터 시작한다. kotlin.collections.Collection은 컬랙션 데이터를 읽는 여러 연산을 수행하는 메서드만 존재한다. 데이터 쓰기에 대한 메서드는 kotlin.collections.MutableCollection에 존재한다.

```kotlin
// kotlin.collections.Collection
public interface Collection<out E> : Iterable<E> {

    public val size: Int

    public fun isEmpty(): Boolean

    public operator fun contains(element: @UnsafeVariance E): Boolean

    override fun iterator(): Iterator<E>

    // Bulk Operations
    /**
     * Checks if all elements in the specified collection are contained in this collection.
     */
    public fun containsAll(elements: Collection<@UnsafeVariance E>): Boolean
}

public interface MutableCollection<E> : Collection<E>, MutableIterable<E> {

    override fun iterator(): MutableIterator<E>

    public fun add(element: E): Boolean

    public fun remove(element: E): Boolean

    public fun addAll(elements: Collection<E>): Boolean

    public fun removeAll(elements: Collection<E>): Boolean

    public fun retainAll(elements: Collection<E>): Boolean

    public fun clear(): Unit
}
```

코드에선 가능하면 read-only 인터페이스를 사용하는 것을 권장한다. 변경이 필요할 떄만 변경 가능한 버전을 사용해야 한다 .

이렇게 읽기와 쓰기를 두 인터페이스로 나누는 이유는 프로그램 내에서 데이터에 어떤 일이 벌어지는지를 더 쉽게 이해할 수 있기 때문이다. 어떤 함수가 MultableCollection을 인자로 받는다면 그 함수가 컬렉션의 데이터를 바꾼다는 것을 짐작할 수 있다.

Read-only 컬렉션을 사용할 때는, thread-safe 하지 않다는 것을 항상 염두에 두어야 한다. 이는 하나의 컬렉션 인스턴스를 여러 개의 참조가 가리킬 수 있기 때문이다.

![List, MutableList](/img/2024-02-25-kotlin-in-action-6/img.png)

이런 상황에서 여러 참조가 동일한 컬랙션 내용을 수정한다면 ConcurrentModificationException 등의 오류가 발생할 수 있다. 따라서 다중 스레드 환경에선 적절한 데이터 동기화하거나 동시에 접근을 허용하는 데이터 구조를 활용해야 한다.

## 6.3 코틀린 컬렉션과 자바

코틀린 컬렉션은 그에 상응하는 자바 컬렉션 인터페이스의 인스턴스이다. 그런데 자바는 컬렉션 읽기, 쓰기에 대해 인터페이스를 구분하지 않는다. 그럼에도 코틀린은 읽기, 쓰기 전용 인터페이스를 제공하면서 자바 인터페이스와의 호환을 제공한다. 이것이 가능한 이유는 코틀린의 읽기, 쓰기 전용 인터페이스가 java.util 패키지에 있는 자바 컬렉션 인터페이스를 그대로 옮겨놓으면서, 읽기 전용 인터페이스는 대응하는 쓰기 인터페이스를 확장하기 때문이다.

![java, kotlin collection type system](/img/2024-02-25-kotlin-in-action-6/img1.png)

위 그림에서 자바 클래스인 ArrayList는 코틀린의 변경 가능한 인터페이스를 확장한다.

이렇게 코틀린에서만 read-only 컬렉션을 구분하기 때문에 자바 컬렉션과 같이 사용할 때 의도치 않은 변경을 초래할 수도 있다. 코틀린에서 read-only Collection으로 선언된 객체를 자바 코드에 넘기면, 자바에서는 변경이 가능해진다. 코틀린 컴파일러는 자바 코드가 컬렉션에 대해 어떤 동작을 하는지 완벽히 파악할 수 없다. 때문에 컬렉션을 자바로 넘길 때, 자바 코드가 컬렉션을 변경할지 여부에 따라 올바른 파라미터 타입을 사용할 책임은 사용자에게 있다. 이런 문제는 코틀린에서 nullable 하지 않은 타입으로 이루어진 컬렉션 타입을 자바 메서드로 넘길 때도 발생한다. 자바 컬렉션은 nullable 하기 때문이다.

## 6.4 컬렉션을 플랫폼 타입으로 다루기

코틀린은 자바에서 선언한 컬렉션 타입 역시 플랫폼 타입으로 본다. 따라서 코틀린에선 그 타입을 읽기 전용 컬렉션이나 변경 가능한 컬렉션 중 원하는 형식으로 사용할 수 있다. 이는 일반적인 상황에 동작이 잘 수행되므로 문제가 되지 않지만, 자바 컬렉션 타입을 파라미터로 사용하는 자바 인터페이스를 코틀린에서 오버라이드 할 경우, 해당 파라미터를 어떤 코틀린 컬렉션 타입으로 선택해야 할지 결정해야 한다. 결정시 고려할 조건은 다음과 같다.

- 컬렉션이 널이 될 수 있는가?
- 컬렉션의 원소가 널이 될 수 있는가?
- 오버라이드 하는 메서드가 컬렉션을 변경할 수 있는가?

## 6.5 객체의 배열과 원시 타입의 배열

코트린 배열은 원소 타입을 타입 파라미터로 받는 클래스이다. 코틀린에서 배열은 만드는 방식은 다음과 같다.

```kotlin
val arrayOf = arrayOf(1, 2, 3) // [1, 2, 3]
// 인자로 넘긴 수 만큼 null 원소를 가진 배열 생성
val arrayOfNulls = arrayOfNulls<Int>(3) // [null, nul, null]
// 람다 식을 호출해 배열을 만든다
val array = Array(3) { i -> i } // [0, 1, 2]
```

위와 같은 방식으로 배열을 선언하면 자바로 변환 시 박싱 된 타입 배열로 반환된다(ex - arrayOf(1, 2)  → java.lang.Integer[]). 만약 원시 타입 배열로 변환을 원한다면, 각 타입에 맞게 코틀린이 제공하는 별도 클래스를 사용하면 된다. 

```kotlin
// 배열 크기를 인자로 받고, 그 만큼을 0(원시 디폴드값)으로 초기화한다.
IntArrya(3) // [0, 0, 0]  
// 여러 값을 가변 인자로 받아서 배열로 만들어준다
inteArrayOf(1, 2) // [1, 2]
// 람다식을 이용해 반환값들을 배열 원소로 만든다.
IntArray(2) { i -> i } // [0, 1]
```

코틀린은 배열 기본 연산뿐만 아니라 컬렉션에서 사용할 수 있는 모든 확장 함수를 배열에서 제공한다.

출처 - [코틀린 인 액션](https://product.kyobobook.co.kr/detail/S000001804588)