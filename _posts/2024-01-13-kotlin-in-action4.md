---
layout:       post
title:        "4장. 클래스, 객체, 인터페이스"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- kotlin
- 코틀린인액션
---

# 1. 클래스 계층 정의

## 1.1 코틀린 인터페이스

코틀린 인터페이스 안에는 추상 메서드와 구현이 있는 메서드를 정의할 수 있다. 그리고 상태를 포함할 수 없다. 또 한, 자바와 같이 인터페이스는 원하는 만큼 구현할 수 있지만, 클래스는 오직 하나만 확장할 수 있다.

```kotlin
interface Clickable {
    fun click()
		// 디폴트 메서드 구현에 default와 같은 키워드를 사용할 필요가 없다.
    fun hello() = println("hello")
}

class Button: Clickable {
		// @Override 애노테이션과 같은 역할을 하는 override 변경자 사용
    override fun click() {
        println("click")
    }
}

Button().click()
Button().hello()
```

만약 이름과 시그니처가 같은 멤버 메서드에 대해 둘 이상의 디폴트 구현이 있다면, 인터페이스를 구현하는 하위 클래스에서 명시적으로 새로운 구현을 제공해야 한다.

```kotlin
interface Clickable {
    fun hello() = println("hello")
}

interface Pushable {
    fun hello() = println("push hello")
}

class Button: Clickable, Pushable {
    override fun hello() {
				// 상위 타입 이름을 아래와 같이 super를 이용해 지정하면 어떤 상위 타입 멤버 메서드를 호출할지 지정할 수 있다.
				// 또는 다른 로직을 구현할 수도 있다.
        super<Pushable>.hello()
    }
}

Button().hello()
```

코틀린은 자바 6과 호환되게 설계됐다(지금은 최소 자바 8이다). 따라서 인터페이스의 디폴트 메서드를 지원하지 않는다. 따라서 코틀린은 디폴트 메서드가 있는 인터페이스를 만들 때 1. 일반 인터페이스, 2. 디폴트 메서드 구현이 정적 메서드로 들어있는 클래스를 조합해 구현한다. 때문에 디폴트 메서드가 포함된 코틀린 인터페이스를 자바 클래스에 상속해 구현하고 싶다면, 디폴트 메서드와 추상 메서드를 모두 구현해야 한다. 하지만, 코틀린 1.5부터는 코틀린 컴파일러가 자바 인터페이스의 디폴트 메서드를 생성해 준다.

## 1.2 open, final, abstract 변경자: 기본적으로 final

취약한 기반 클래스(fragile base class)라는 문제는 하위 클래스가 기반 클래스에 대해 가졌던 가정이 기반 클래스를 변경해서 깨져버리는 경우 생긴다. 어떤 클래스가 자신을 상속하는 방법에 대해 정확한 규칙을 제공하지 않으면, 그 클래스의 클라이언트는 기반 클래스를 작성한 사람의 의도와 다른 방식으로 메서드를 오버라이드할 위험이 있다. 

코틀린은 이런 문제를 방지하기 위해 의도한 클래스와 메서드가 아니면 모두 final로 만든다. 상속을 허용하고 싶은 클래스, 오버라이드를 허용하고 싶은 메서드, 프로퍼티가 있다면 앞에 open을 붙여야 한다. 또 한, 기반 클래스나 인터페이스 멤버를 오버라이드 하는 경우 그 메서드는 기본적으로 열려있다. 오버라이드 하는 메서드는 구현을 하위 클래스에서 오버라이드 하지 못하게 금지하기 위해서 final을 붙여야 한다.

```kotlin
interface Clickable {
    fun click()
}

open class Button: Clickable {
    
    fun disable() {} // final 함수, 하위 클래스가 오버라이드할 수 없다

    open fun animate(){} // 열려있는 함수, 하위 클래스가 오버라이드할 수 있다
    
    // 오버라이드해서 구현한 함수를 final로 처리했다. Button 클래스를 상속한 클래스에선 해당 메서드를 오버라이드할 수 없다
    final override fun click() {} 
}

class SubButton: Button() {

    override fun disable() {} // 에러

    override fun animate() {}

    override fun click() {} // 에러
}
```

자바처럼 코틀린에서도 클래스를 abstract로 선언할 수 있다.

```kotlin
// abstract class는 인스턴스화할 수 없다
abstract class Animated {
		abstract fun animate() // 추상함수는 항상 열려있다
		open fun stopAnimating() {} // 추상 클래스에 속한 비추상 함수는 기본적으로 final이다
}
```

## 1.3 가시성 변경자: 기본적으로 공개

가시성 변경자(visibility modifier)는 코드 기반에 있는 선언에 대해 클래스 외부 접근을 제어한다. 기본적으로는 자바와 같이 public, private, protected가 있지만 디폴트가 public이라는 점이 다르다. 이는 코틀린이 패키지를 네임스페이스 관리를 위해서만 사용하기 때문이다. 대신 internal이라는 가시성 변경자를 사용한다. 이 변경자를 사용하면 모듈 내부에서만 사용 가능하다. 모듈이란 한 번에 한꺼번에 컴파일되는 코틀린 파일들을 의미한다 메이븐, 크레이들 등의 프로젝트가 모듈이 될 수 있다. protected의 경우 자바에서는 같은 패키지 안에서 protected 멤버에 접근할 수 있지만, 코틀린에서는 그렇지 않다.

최상위 선언에 대해 priavate을 사용할 수 있는 것도 차이점이다. 이런 최상위 선언엔 클래스, 함수, 프로퍼티 등이 포함된다. 이를 사용하면 해당 선언인 해당 파일 내부에서만 사용할 수 있으므로 하위 시스템의 자세한 구현 사항을 외부에 감추고 싶을 때 유용한다.

### 1.3.1 코틀린의 가시성 변경자와 자바

코틀린의 변경자는 일반적으로 컴파일된 자바 바이트코드 안에서도 그대로 유지된다. 다만, private 클래스는 다르다. 자바는 private class를 지원하지 않으므로 내부적으로 코틀린은 private 클래스를 패키지 전용 클래스로 컴파일한다.

internal 변경자 역시 자바에선 대응하는 가시성이 없다. 때문에 바이트코드상에선 public이 된다. 이런 차이 때문에 코틀린에서 접근할 수 없는 대상을 자바에서 접근할 수 있는 경우가 발생한다. 예컨대, internal 클래스와 internal 최상위 선언을 모두 외부의 자바 코드에서 접근할 수 있다.

코틀린 컴파일러는 internal 멤버 이름을 가시성이 떨어지게 바꾼다. 그 이유는 다음과 같다.

- 한 모듈에 속한 클래스 A를 모듈 밖에서 상속한 경우, 하위 클래스 내부의 메서드 이름과 A클래스에 속한 internal 메서드의 이름이 같아서 해당 메서드를 오버라이드 하는 경우 방지
- 실수로 internal 클래스를 모듈 외부에서 사용하는 것을 막기 위해

코틀린에선 외부 클래스가 내부 클래스나 중첩된 클래스의 private 멤버에 접근할 수 없다는 차이도 존재한다.

## 1.4 내부 클래스와 중첩된 클래스: 기본적으로 중첩 클래스

코틀린의 중첩 클래스(nested class)는 명시적으로 요청한지 않는 한 바깥쪽 클래스 인스턴스에 대한 접근 권한이 없다. 이는 내부 클래스를 직렬화할 때 이점이 있다. 자바에선 클래스 내에 정의한 클래스는 자동으로 inner class가 된다. 따라서 외부 클래스에 대한 참조를 묵시적으로 포함하고 있기 때문에, 내부 클래스를 직렬화할 때 외부 클래스가 직렬화를 지원하지 않으면 NotSerializableException이 발생한다. 자바에서 이 문제를 해결하기 위해선 내부에 정의한 클래스를 static으로 선언해야 한다. 그러면 바깥쪽 클래스에 대한 묵시적 참조가 사라진다.

코틀린에서 inner class를 사용하고 싶다면 inner 변경자를 붙여야 한다. 또 한, 외부 클래스 참조에 접근하려면 this@ClassName을 사용하면 된다.

```kotlin
class Outer {
		inner class Inner {
				fun getOuterReference(): Outer = this@Outer
		}
}
```

## 1.5 봉인된 클래스: 계층 정의 시 계층 확장 제한

```kotlin
interface Expr
class Num(val value: Int): Expr
class Sum(val left: Expr, val right: Expr): Expr

fun eval(e: Expr): Int =
    when (e) {
        is Num -> e.value
        is Sum -> eval(e.right) + eval(e.left)
        else -> throw IllegalArgumentException()
    }
```

위와 같은 코드에서 when을 사용할 때 반드시 else 분기를 덧붙여야 한다. 이렇게 디폴트 분기가 있는 것은 클래스 계층에 새로운 하위 클래스를 추가해도, 컴파일러가 when이 모든 경우를 처리하는지 제대로 검사할 수 없기 때문에 버그를 야기할 수 있다.

이 문제를 해결하기 위해선 sealed 클래스를 사용하면 된다. 이를 사용하면 하위 클래스 정의를 제한할 수 있다. sealed 클래스의 하위 클래스를 정의할 때는 반드시 상위 클래스 안에 중첩시켜야 한다. 이 상황에서 sealed class의 새로운 하위 클래스를 추가한다면 when 식에 이와 관련된 분기를 추가하기 전까지 컴파일이 되지 않는다.

```kotlin
// sealed class는 private 생성자를 가진다.
// sealed interface는 존재하지 않는다. 자바쪽에서 해당 인터페이스 구현을 막을 수 있는 수단이 없기 때문이다.
sealed class Expr {
    class Num(val value: Int): Expr()
    class Sum(val left: Expr, val right: Expr): Expr()
}

fun eval(e: Expr): Int =
		// 디폴트 분기가 필요 없다.
    when (e) {
        is Expr.Num -> e.value
        is Expr.Sum -> eval(e.right) + eval(e.left)
    }
```

# 2. 뻔하지 않은 생성자와 프로퍼티를 갖는 클래스 선언

코틀린은 주 생성자와 부 생성자를 구분한다. 또 한, 초기화 블록(initializer block)을 통해 초기화 로직을 추가할 수 있다.

## 2.1 클래스 초기화: 주 생성자와 초기화 블록

클래스 이름 뒤에 오는 괄호로 둘러싸인 코드가 주 생성자이다. 주 생성자 선언을 하는 방식 종류는 다음과 같다.

```kotlin
// 방법 1.
// '_'은 프로퍼티와 생성자 파라미터를 구분하는 용도이다. 대신 자바 처럼 this를 사용해도 된다
// init 블록은 초기화 블록으로, 객체가 만들어질 때 실행될 초기화 코드가 들어간다.
// 초기화 블록 여러개를 사용할 수도 있다
class User constructor(_nickname: String) {
    val nickname: String

    init {
        nickname = _nickname
    }
}

// 방법 2.
class User(_nickname: String) {
    val nickname = _nickname
}

// 방법 3.
class User (val nickname: String)
```

주 생성자를 상황에 따라 다음과 같이 사용할 수 있다.

```kotlin
// 디폴트 파라미터 사용 가능
// 모든 생성자 파라미터에 디폴트 값을 지정하면 컴파일러가 자동으로 파라미터가 없는 생성자를 만들어준다.
class User(val nickname: String, isSubscribed: Boolean = false)

// nickname을 받아서 상위 클래스 생성자로 인자를 넘긴다
class TwitterUser(nickname: String): User(nickname) {...}

// 클래스 정의 시 별도 생성자를 정의하지 않으면 컴파일러가 자동으로 비어 있는 디폴트 생성자를 만든다.
class Button {}

// 생성자를 private으로 만든다. 클래스 외부에서 인스턴스화하지 못하게 막는다.
class Secretive private constructor() {}
```

## 2.2 부 생성자: 상위 클래스를 다른 방식으로 초기화

코틀린은 자바의 부 생성자 대부분 역할을 디폴트 파라미터 값과 이름 붙이 인자 문법으로 해결할 수 있다. 그럼에도 부 생성자가 필요한 경우, 다음과 같이 정의해 사용하면 된다. 부 생성자는 자바 상호운용성과 인스턴스 생성 시 파라미터 목록이 여러 생성 방법이 있을 때 사용할 수 있다.

```kotlin
class View {
    
    constructor(context: Context, attr: AttributeSet) {}
    
    // this로 다른 생성자 호출 가능
    constructor(context: Context): this(context, AttributeSet()) {}
}

class MyButton: View {
    
    // super로 상위 생성자 호출
    constructor(context: Context): super(context) {}
}
```

## 2.3 인터페이스에 선언된 프로퍼티 구현

인터페이스에 추상 프로퍼티 선언을 넣을 수 있다. 인터페이스에는 프로퍼티 선언에 뒷받침하는 필드나 게터 등 정보가 있지 않기에 하위 클래스에서 상태 저장을 위한 프로퍼티 등을 만들어야 한다.

```kotlin
interface User {
    val nickname: String
}

class privateUser(override val nickname: String): User {}

class SubScribingUser(val email: String): User {
    
    override val nickname: String
        get() = email.substringBefore('@')
}

class FacebookUser(val accountId: Int): User {
    override val nickname = getFacebookName(accountId)
}
```

인터페이스에는 게터와 세터가 있는 프로퍼티를 선언할 수도 있지만 뒷받침하는 필드를 참조할 수 없다.

```kotlin
// 하위 클래스는 email을 반드시 오버라이드 해야 하지만, nickname은 그냥 사용할 수 있다.
interface User {
    val email: String
    val nickname: String
        get() = email.substringBefore('@')
}
```

## 2.4 접근자의 가시성 변경

getter, setter의 가시성은 기본적으로 프로퍼티와 같지만 원한다면 앞에 private을 붙여서 외부에서 접근하지 못하게 막을 수 있다.

# 3. 컴파일러가 생성한 메서드: 데이터 클래스와 클래스 위임

자바 클래스는 equals, hashCode, toString 등 메서드를 구현해야 한다. 코틀린 컴파일러는 이럼 필수 메서드들을 기계적으로 생성하는 작업을 보이지 않는 곳에서 해준다.

## 3.1 모든 클래스가 정의해야 하는 메서드

코틀린은 다음과 같이 equals, hashCode, toString을 원하는 대로 오버라이드 할 수 있다.

```kotlin
class Client(val name: String, val postalCode: String) {
    
    // Any는 자바의 Object에 해당한다
    override fun equals(other: Any?): Boolean {
        if (this === other) return true
        if (javaClass != other?.javaClass) return false

        other as Client

        if (name != other.name) return false
        if (postalCode != other.postalCode) return false

        return true
    }

    override fun hashCode(): Int {
        var result = name.hashCode()
        result = 31 * result + postalCode.hashCode()
        return result
    }

    override fun toString(): String {
        return "Client(name='$name', postalCode='$postalCode')"
    }
}
```

data라는 변경자를 클래스 앞에 붙이면 위와 같이 필수 메서드를 명시적으로 정의할 필요가 없다. 컴파일러가 자동으로 만들어준다. 자동으로 생성된 equals와 hashCode는 주 생성자에 나열된 모든 프로퍼티를 고려해 만들어진다.

```kotlin
// euqals, hashCode,, toString을 자동으로 생성해준다
data class Client(val name: String, val postalCode: Int)
```

데이터 클래스는 copy라는 편의 메서드도 제공한다. 이는 데이터 클래스 인스턴스를 불변 객체로 더 쉽게 활용할 수 있게 코틀린 컴파일러가 제공하는 메서드이다. copy 메서드는 객체를 복사하면서 일부 프로퍼티를 바꿀 수 있게 해준다.

```kotlin
data class Client(val name: String, val postalCode: String)

val client = Client("name", "postal")
val copiedClient = client.copy("name2", "postal2")
// output:
// Client(name=name, postalCode=postal)
// Client(name=name2, postalCode=postal2)
println("${client}\n${copiedClient}")
```

## 3.2 클래스 위임: by 키워드 사용

상속을 허용하지 않는 클래스에 새로운 동작을 추가해야 할 때 종종 데코레이터 패턴을 사용한다. 이 패턴은 새로운 클래스(데코레이터)를 만들되 기존 클래스와 같은 인터페이스를 데코레이터가 제공하게 만들고, 기존 클래스를 데코레이터 내부에 필드로 유지한다. 이때 새로 정의해야 하는 기능은 데코레이터의 메서드에 새로 정의하고 기존 기능이 그대로 필요한 부분은 데코레이터의 메서드가 기존 클래스의 메서드에게 요청을 전달 (forwarding)한다.

이런 접근 방법은 인터페이스를 구현하면서 복잡한 코드를 만들어야 한다는 단점이 존재한다. 코틀린은 이를 해결하기 위해 by 키워드를 통해 그 인터페이스에 대한 구현을 다른 객체에 위임 중이라는 사실을 명시할 수 있다. 그러면 컴파일러가 전달 메서드를 자동으로 생성해 준다.  메서드 중 동작을 변경하고 싶은 경우에만 메서드를 오버라이드 하면 된다.

```kotlin
// 기존 방식
class DelegatingCollection<T>(override val size: Int) : Collection<T> {
    
    private val innerList = ArrayList<T>()
    
    override fun contains(element: T): Boolean = innerList.contains(element)

    override fun containsAll(elements: Collection<T>): Boolean = innerList.containsAll(elements)

    override fun isEmpty(): Boolean = innerList.isEmpty()

    override fun iterator(): Iterator<T> = innerList.iterator()
}

// by 이용
class DelegatingCollection<T>(innerList: Collection<T> = ArrayList<T>()) : Collection<T> by innerList
```

# 4. object 키워드: 클래스 선언과 인스턴스 생성

코틀린에선 object 키워드를 다음과 같은 상황에서 사용한다

- 객체 선언(object declaration): 싱글턴을 정의하는 방법 중 하나

```kotlin
object Payroll {
    
    val allEmployees = arrayListOf<Person>()
    
    fun calculateSalary() {
        
    }
}

Payroll.allEmployees.add(Person(...))
Payroll.calculateSalary()
```

- 동반 객체(companion object): 인스턴스 메서드는 아니지만 어떤 클래스와 관련 있는 메서드와 팩토리 메서드를 담을 때 쓰인다. 동반 객체 메서드에 접근할 때는 동반 객체가 포함된 클래스의 이름을 사용할 수 있다.
    - 코틀린은 자바의 static 키워드를 지원하는 대신 이 기능을 패키지 수준의 최상위 함수와 객체 선언을 활용한다. 최상위 함수는 private으로 표시된 클래스 비공개 멤버에 접근할 수 없다. 따라서 static 멤버와 같은 역할을 하지만 클래스 내부 정보에 접근해야 할 때 companion을 이용해 동반 객체를 사용한다. 동반 객체의 사용 구문은 자바의 정적 메서드 호출과 정적 필드 사용과 같다. 동반 객체는 자신을 둘러싼 클래스의 모든 private 멤버에 접근할 수 있다.
    
    ```kotlin
    class A {
        
        private var a = "A"
    
        companion object {
            fun bar() {
                println(A().a)
            }
        }
    }
    
    A.bar()
    
    // 팩토리 메서드 예시
    open class User() {
        
        companion object {
            fun createSubscribingUser() = SubscribingUser()
            fun createFacebookUser() = FacebookUser()
        }
    }
    class SubscribingUser: User()
    class FacebookUser: User()
    
    val facebookUser = User.createFacebookUser()
    ```
    
    - 동반 객체를 일반 객체처럼 사용
        - 동반 객체는 클래스 안에 정의된 일반 객체이기에 이름을 붙이거나, 인터페이스를 상속하거나, 안에 확장 함수와 프로퍼티를 정의할 수 있다.
    - 코틀린 동반 객체와 정적 멤버
        - 코틀린의 동반 객체는 클래스에 정의된 인스턴스를 가리키는 정적 필드로 컴파일된다. 동반 객체에 이름을 붙이지 않았다면 자바에선 Companion이라는 이름으로 참조에 접근할 수 있다. 만약 자바에서 사용하기 위해 코틀린 클래스의 엠버를 정적인 멤버로 만들어야 한다면 @JvmStatic 애너테이션을 멤버에 붙이면 된다. 정적 필드가 필요하다면 @JvmField 애너테이션을 최상위 프로퍼티나 객체에 선언된 프로퍼티 앞에 붙이면 된다.
    - 동반 객체 확장
        - 클래스에 동반 객체가 있으면 그 객체 안에 함수를 정의해서 클래스에 대해 호출할 수 있는 확장 함수를 만들 수 있다.
        
        ```kotlin
        class Person(val firstName: String) {
        		companion object {}
        }
        
        fun Person.Companion.fromJSON(json: String): Person {
        		...
        }
        
        val person = Person.fromJSON(json)
        ```
        
- 객체 식은 자바의 무명 내부 클래스(anonymous inner class) 대신 쓰인다.
    - object 키워드를 이용해 무명 객체(anonymous object)를 정의할 때 사용한다.  무명 객체는 한 인터페이스 구현이나 한 클래스만 확장할 수 있는 자바와 달리 여러 인터페이스를 구현하거나 클래스를 확장한면서 인터페이스를 구현할 수 있다.  또 한, 자바 무명 클래스와 달리 final이 아닌 변수도 객체 식 안에서 사용할 수 있다.

```kotlin
window.addMouseListener (

    object: MouseAdapter() {
        override fun mouseClicked(e: MouseEvent?) {
            ...
        }
    }
)

val listener = object: MouseAdapter() {
    override fun mouseClicked(e: MouseEvent?) {...}
}
```

출처 - [코틀린 인 액션](https://product.kyobobook.co.kr/detail/S000001804588)