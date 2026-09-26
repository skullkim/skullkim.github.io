---
layout:       post
title:        "객체 공유"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
  - java
  - 병렬프로그래밍
  - ComputerScience
---

- 특정 객체를 여러 스레드가 접근할 때 안전하게 동작하게 객체를 공유하는 방법을 살펴보자.
- 크리티컬 섹션에 대한 처리를 하지 않으면 메모리 가시성(memory visibility) 문제가 발생할 수 있다.
    - 메모리 가시성은 한 스레드가 변경한 값을 다른 스레드가 제떄 확인할 수 없는 것을 의미한다.
    - 이는 하드웨어 성능 때문에 각 CPU 코어가 캐시를 두고, 컴파일러나 CPU가 명령어를 재정렬해서 발생한다. 이 때, 각 스레드는 자신들의 캐시에 쓰기를 반영하기 때문에 실제 값이 메모리에 반영되기 까지 시간이 걸린다. 이 시간으로 인해 타 스레드는 이전 값을 조회한다.
- 때문에 크리티컬 섹션에 있는 값을 다른 스레드가 접근하지 못하게 하고, 변경된 값을 즉시 메모리에 반영해야한다.

# 1. 가시성

- 멀티 스레드 환경에서 메모리 가시성 때문에 특정 변수의 값을 값을 가져갈 때 다른 스레드가 쓴 값을 가져갈 수 있다는 보장이 없다. 때문에 반드시 동기화 기능을 구현해야한다.
    - 동기화가 없다면 컴파일러, JVM 등에서 최적화를 위해 프로그램 코드 실행 순서를 바꿀 수 있다.
- 이렇게 동기화 문제로 갱신이 되지 않은 이전 데이터를 stale data라고 한다.
- 가시성과 원자성 차이
    - 가시성: 한 스레드가 바꾼 값을 다른 스레드가 볼 수 있나?
    - 원자성: 여러 개의 연산이 중간에 끼어들 수 없는 하나로 취급되나?

## 3.1 단일하지 않은 64비트 연산

- 스테일 데이터 현상은 이전 값을 사용하는 거지 엉뚱한 값이 생기는 것이 아니다. 그러나 자바에서 64비트를 사용하는 숫자형(double, long 등)을 volatile 키워드 없이 사용한다면 엉뚱한 값이 생길 수 있다.
- 자바 메모리 모델은 메모리에서 값을 fetch하고 store하는 연산이 단일해야 한다고 규정하지만, volatile로 지정되지 않은 long, double형은 메모리를 쓰거나 읽을 때 두 번의 32비트 연산을 사용하게 허용한다. 때문에 이전 값과 현재 값을 각각 32비트씩 읽어와 엉뚱한 값이 생길 수도 있다.
    - volatile로 선언한 변수는 항상 최신 값을 유지한다. volatile로 지정된 변수는 프로세서의 레지스터와 외부 캐시에 포함되지 않는다. 때문에 항상 최신값을 읽어갈 수 있다.
    - volatile은 가시성만 보장하고 락은 원자성과 가시성 모두 보장한다. 때문에 volatile은 실제로는 여러 단계로 나뉘어진 count++ 와 같은 연산의 동기화까지 맞춰지지는 않는다.
    - 때문에 volatile 변수는 다음과 같은 상황에서만 사용해야 한다.
        - 변수에 값을 저장하는 작업이 해당 변수의 현재 값과 관련이 없거나 해당 변수의 값을 변경하는 스레드가 하나만 존재
        - 해당 변수 불변조건(invariant - 항상 참이어야하는 다른 변수와의 관계)과 관련 없다
        - 해당 변수를 사용하는 동안에는 어떤 경우라도 락을 걸 필요가 없다. → 락을 걸거면 volatile을 쓸 이유가 없다.

## 3.2 공개와 유출

- 공개(published): 특정 스코프 외부로 객체를 전달하는 행위이다. 객체 리턴, private이 아닌 메서드 파라미터로 객체 전달 등이 있다.
- 유출(escaped) 상태: 의도적으로 공개하지 않았지만 외부에서 사용할 수 있는 상태
- 객체를 공개하면 private이 아닌 메서드와 변수가 모두 같이 공개된다.

### 3.2.1 생성 메소드 안전성

- 객체는 생성자가 완료되어야 생기기 때문에, 생성 메서드 내부에서 this 등을 이용해 해당 메서드를 외부에 공개한다면, 해당 객체는 정상적으로 생성되지 않을 수 있다.

```java
public class ThisEscape {       // 바깥 클래스
    void doSomething(Event e) { }

    public ThisEscape(EventSource source) {
        source.registerListener(new EventListener() {         // 내부(익명) 클래스
                public void onEvent(Event e) {
                    doSomething(e);
                    // doSomething은 바깥 ThisEscape의 메서드
                    // → 바깥 ThisEscape 객체가 있어야 호출 가능
                    // → 내부 클래스가 바깥 객체(this)를 자동으로 붙잡고 있다
                }
            }
        );
    }
}
```

- 위 같은 상황을 보자. ThisEscape의 객체는 생성자가 끝나기 전까지 생성되지 않는다. 떄문에 source에 this.doSomthing(e)를 가진 EventListener 객체가 먼저 등록된다. 여기서, source는 객체이기에 참조로 넘어오기때문에, 외부에서 ThisEscape 생성자 완료 전에 source에 등록한 EventLisener의 객체를 호출할 수 있다.
- 이런 상황을 방지하기 위해서 팩토리 패턴을 사용하는게 권장된다.

```java
public class SafeListener {
    private final EventListener listener;

    // private 생성자 — 외부에서 직접 new 못 함
    private SafeListener() {
        listener = new EventListener() {
            public void onEvent(Event e) {
                doSomething(e);
            }
        };
    }

    // 팩토리 메서드
    public static SafeListener newInstance(EventSource source) {
        SafeListener safe = new SafeListener();  // ① 객체를 완전히 생성
        source.registerListener(safe.listener);  // ② 그 다음에 등록
        return safe;
    }
}
```

# 3.3 스레드 한정

- 스레드 하나에서만 객체를 다루는게 보장된다면 스레드 안전성을 확보할 수 있다.
- 이런 스레드 한정 기법은 언어 자체 지원과 라이브러리에서 제공한다고 해도 개발자가 스레드 외부로 유출되지 않게 항상 신경써야 한다.

## 3.3.1 주먹구구식

- 어떤 라이브러리나 프레임워크 도움 없이, 개발자가 사람 수준에 의존해 스레드 한정을 진행할 경우 예외를 제대로 컨트롤하지 못해 스레드 한정이 쉽게 깨질 수 있다.

## 3.3.2 스택 한정

- 특정 값을 로컬 변수를 통해서만 사용한다면, 해당 값을 스레드 안전하다.
- 기본 변수형을 사용하는 로컬 변수는 스택 한정 상태가 보장된다.
- 객체형 로컬 변수는 해당 객체 참조가 외부에 노출되게 하지 않으면 된다.

### 3.3.3 TheadLocal

- TheadLocal을 사용하면 get, set 메서드를 통해 스레드마다 다른 값을 사용할 수 있게 관리해준다.
- 다만, TheadLocal은 전역변수 처럼 동작하기 때문에, 자칫 잘못하면 전역 변수를 사용하는 것과 같은 문제들을 야기한다.

# 3.4 불변성(Immutable)

- 불변 객체는 맨 처음 생성되는 시점을 제외하면 그 값이 바뀌지 않는다
- 자바 언어 명세(Java Language Specifications)나 자바 메모리 모델은 객체 불변성에 대해 언급하지 않지만, 다음과 같은 조건을 만족시켜서 불변객체를 만들 수 있다
    - 생성되고 난 뒤 상태를 변경할 수 없게 한다
    - 내부의 모든 변수는 final로 설정한다
    - 적절한 객체 생성 방식을 사용한다.(위 에서 언급한 this 유출 같은 상황을 방지한다)
- final 키워드를 사용하면 초기화 안전성(initializaiton safety)을 보장하기때문에 별다른 동기화 없이 불변 객체를 사용하고 공유할 수 있다. 객체가 불변이 아니여도 final을 사용하면 고려할 범위가 줄어들기 때문에 프로그램을 작성할 때 편리하다.

    ```java
    public class Holder {
        private  int value;  // final
    
        public Holder(int value) {
            this.value = value;
        }
    }
    
    Holder holder = new Holder(42);
    holder = ...
    ```

    - 위와 같은 코드를 멀티 스레드 환경에서 사용한다면 A 스레드가 holder 객체가 생성 완료하기 전에 그 다음 줄을 스레드 B가 호출할 수도 있다. 이는 Java Memory Model에서 단일 스레드 내에서 순서를 바꿔도 동작이 문제 없다면, 최적화를 위해 동작 순서를 바꾸기 때문이다. 때문에 재정렬은 스레드마다 독립적이다.
    - 그러나 “private final int value;” 처럼 final을 사용한다면 객체 생성과 그 이후 로직 간 재정렬을 freeze 하기 때문에 이런 현상이 발생하지 않는다. 때문에 final을 사용하면 모든 스레드는 freeze 이후 확정된 값을 본다.

# 3.5 안전 공개

- 객체를 여러 스레드가 공유하게 공개할 때 public으로 공개하는건 안전한 방법이 아니다
- 아래 예제에서 한 스레드는 생성자 메서드를 이용해 객체를 공개하고, 다른 한 스레드가 assertSanity()를 호출한다면 AssertionError가 발생할 수 있다. 객체 생성 완료 전 그 객체를 사용하려 했기 때문이다.

```java
public class Holder {
	private int n;
	
	public Holder(int n) { this.n = n; }
	
	public void assertSanity() {
			if (n != n)
					throw new AssertionError("This statement is false.");
	}
}

public Holder holder;
public void initialize() {
    holder = new Holder(42);
}
```

- 이는 두 가지 문제를 야기한다.
    1. holder 변수 자체에서 stale 상태가 발생한다. 변수값 지정 이후에도 null값이 지정되거나 예전에 사용하던 참조가 들어간다.
    2. holder 내부 변수(n)에서 stale이 발생한다. 생성 메서드가 지정하는 값이 최초 값이여도 Object 클래스를 상속하기 때문에 Object 클래스가 설정한 최초값이 stale data가 될 수 있다.

## 3.5.1 불변 객체와 초기화 안전성

- 위 같은 상황 방지를 위해선 객체를 외부 공개할 때 동기화 방법이 필요하다. 하지만, 객체가 불변이라면 동기화를 하지 않아도 항상 안전하게 올바른 값을 참조할 수 있다.

## 3.5.2 안전한 공개 방법의 특성

- 불변 객체가 아닐 경우, 객체를 공개하는 스레드와 객체를 불러와 사용하는 스레드 모두에 동기화할 방법이 필요하다.
- 여기서는 1.객체를 사용하는 스레드가 공개된 값을 안전히 불러와 사용하는 것과 2.공개된 이후에 변경된 값을 정확하게 사용하는 것 두 가지를 고려해야 한다.
- 우선 객체를 사용하는 스레드가 공개된 값을 안전히 불러와 사용하는 것을 살펴보자.
    - 객체를 안전하게 공개하려면 객체에 대한 참조, 객체 내부의 상태를 외부 스레드에게 동시 공개해야한다.
    - 올바른 생성 메서드를 사용한 후 다음과 같은 방법으로 안전하게 공개할 수 있다.
        - 객체에 대한 참조를 static 메서드에서 초기화시킨다. 이는 static 블록을 JVM이 락을 걸고 실행하기 때문이다.

            ```jsx
            public static Holder holder = new Holder(42);
            // 또는
            public static Holder holder;
            static {
                holder = new Holder(42);
            }
            ```

        - 객체에 대한 참조를 volatile 변수 또는 AtomicReference 클래스에 보관한다.
            - AtomicReference는 원자적으로 참조값을 다룰 수 있게 해준다. 내부적으로 volatile을 사용하고 compareAndSwap()을 지원한다. 이는 락없는 동시성을 지원한다.

            ```java
            AtomicReference<Holder> ref = new AtomicReference<>();
            ref.set(new Holder(42));   // 원자적으로 참조 설정
            Holder h = ref.get();      // 원자적으로 참조 읽기
            ```

        - 객체에 대한 참조를 올바르게 생성된 클래스 내부의 final 변수에 보관한다.
        - 락을 사용해 올바르게 막혀있는 변수에 객체에 대한 참조를 보관한다.

## 3.5.3 결과적으로 불변인 객체

- 안전하게 공개된 객체는 추후에 객체 내부 값이 바뀌지 않는다면 여러 스레드가 해당 값을 가져다 사용해도 동기화 문제가 발생하지 않는다.
- 따라서 이런 객체는 정의상 불변이 아니여도 한번 공개된 후 내용이 바뀌지 않는다면 기술적으로는 불변이라 볼 수 있다.
- 이런 객체는 개발 과정이 불변 객체 보다 간단하기에 프로그램 성능을 개선하는데 도움이 된다.

## 3.5.4 가변 객체

- 만약 객체를 안전하게 공개하기만 한다면 공개 후 다른 스레드가 값을 읽는대 문제가 없는 정도만 보장된다.
- 때문에 동기화와 락을 사용해 스레드 안전성을 확보해야한다.

## 3.5.5 객체를 안전하게 공유하기

- 결론적으로 병렬 프로그래밍에서 객체를 공유해 사용할 때 다음과 같은 원칙이 사용도니다.
    - 한 스레드에 객체 한정
    - 읽기 전용 객체를 공유
    - 스레드에 안전한 객체를 공유
    - 동기화 방법 적용 (락 등)

출처 - [자바병렬프로그래밍](google.com/search?q=자바병렬프로그래밍&oq=자바병&gs_lcrp=EgZjaHJvbWUqCggBEAAYogQYiQUyBggAEEUYOTIKCAEQABiiBBiJBTIHCAIQABjvBTIKCAMQABiiBBiJBdIBCDMxNDJqMGo5qAIGsAIB8QV2EoGbIEFLUw&sourceid=chrome&ie=UTF-8)