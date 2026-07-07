---
layout:       post
title:        "스레드 안전성"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
  - java
  - 병렬프로그래밍
  - ComputerScience
---

- 병렬 프로그래밍에서 안전한 코드의 근본 목적은 공유되고 변경할 수 있는 상태 접근을 관리하는 것이다. 이를 위해 스레드와 락 등 도구를 사용한다.
- 스레드 안전성은 공유되는 상태를 제어 없이 동시 접근하는 것을 막는 것이다. 이를 위해서 동기화라는 상태 접근에 대한 조율 과정이 필요하다.
- 스레드 안전성을 지키는 가장 좋은 방법은 애초에 클래스 설계 시 이를 염두하는 것이다. 추후 스레드 안전성을 지키기 위해 작업한다면 많은 리소스가 소요된다. 스레드 안전성을 지키기 위한 리펙터링에는 다음과 같은 접근법이 있다.
    - 해당 상태 변수를 스레드 간에 공유하지 않는다
    - 해당 상태 변수를 변경할 수 없게 만든다
    - 해당 상태 변수에 접근할 땐 언제나 동기화를 사용한다.
- 스레드 안전한 클래스를 설계할 때는 캡슐화와 불변 객체를 잘 활용해야한다. 상태를 외부에 드러내는 일이 적어야 적절히 동기화가 잘 되는지 확인하기 쉽다.

# 1. 스레드 안전성이란?

- 스레드 안전성 정의:
    - 여러 스레드가 클래스에 접근할 때, 실행 환경의 스레드 스케줄링 방식에 영향받지 않고 클라이언트에서 추가적인 동기화가 없어도 정확이 동작하는 클래스
- 상태를 갖지 않는 코드는 레이싱 컨디션이 없어서 스레드 안전하다
- 아래와 같이 상태를 갖거나 유효하지 않는 값을 참조해 다음 로직을 결정하는 check-then-act 형태 구문은 경쟁 조건 대상이다.
```java
@ThreadSafe
public class StatelessFactorizer implements Servlet {
    private long count = 0;
    
    @Override
    public void service(ServletRequest req, ServletResponse resp)
            throws ServletException, IOException {
        BigInteger i = extractFromRequest(req);
        BigInteger[] factors = factor(i);
        count++;
        encodeIntoResponse(resp, factors);
    }
}
```
- 스레드 안전성 보장을 위해선 연산이 여러 하위 동작으로 이루어진 복합 동작(compound action)이면 안된다. 전체가 단일 연산이어야한다. 위예제를 단일 연산 변수(actomic variable)를 이용해 다음과 같이 스레드 안전하게 수정할 수 있다.
```java
@ThreadSafe
public class StatelessFactorizer implements Servlet {
    private final AtomicLong count = new AtomicLong(0);
    
    @Override
    public void service(ServletRequest req, ServletResponse resp)
            throws ServletException, IOException {
        BigInteger i = extractFromRequest(req);
        BigInteger[] factors = factor(i);
        count.incrementAndGet();
        encodeIntoResponse(resp, factors);
    }
}
```
# 2. 락

- 상태가 한개라면 atomic variable로 커버되지만, 상태를 일관성있게 유지해야하는 변수가 여러개라면 다른 방법을 사용해 단일 연산으로 갱신해야한다. 락을 통해 이를 해결할 수 있다

## 2.1 암묵적인 락(Intrinsic lock)

- 자바에 내장된 락을 암묵적 락 또는 모니터 락(monitor lock)이라 한다.
- synchronized block은 락으로 사용 될 객체의 참조값과 해당 락으로 보호하려는 코드블록으로 나뉜다. 블록에 진입하면 락이 획득되고, 예외 발생 또는 블록을 벗어나면 락이 자동 해지된다.
```java
synchronized (lock) {...}

synchronized void fun(...) {...}
```
- 하지만 이 방법을 사용한 서블릿은 여러 클라이언트가 동시에 사용할 수 없어서 응답성이 떨어진다.

## 2.2 재진입성

- 재진입성은 락을 획득한 스레드가 같은 락을 획득하려고 할 때 다시 락을 획득할 수 있는 성질이다. 즉, 락은 스레드 단위로 관리된다.
- 재진입성이 없다면, 락을 취득한 스레드가 같은 락을 요구하는 코드를 실행해야 할때 데드락에 빠질 수 있다.
```java
synchronized void a() {...}
synchronized void b() {
	a(); // b() 진입에서 락 취득 후, 같은 락으로 a() 진입 필요
}
```
## 2.3 락으로 상태 보호하기

- 락을 확보한 상태로 복합 동작을 실행하면, 이 동작들이 원자적으로 실행되는것 처럼 보이게 할 수 있다.
- 공유 변수는 read, write 상관 없이 접근에는 모두 동일한 락을 확보한 상태여야한다.
- Java에서 Vector를 포함한 동기화된 컬랙션 클래스는 변경 가능한 변수를 캡슐화하고, 객체의 암묵적인 락을 사용해 변수에 접근하는 모든 경로를 동기화해서 내부 변수를 보호한다.
- 여러 변수에 대한 불변조건이 있다면, 해당 변수들은 모두 같은 락으로 보호해야한다.

## 2.5 활동성과 성능

- 너무 많은 양의 코드를 synchronized로 락을 잡으면 병렬 처리 능력이 떨어진다. 때문에 오래 걸리는 작업을 synchronized 블록 내부에서 배제시켜서 병렬성을 지킬 필요가 있다.
- 락을 잡을 때는 안전성, 단순성, 성능 등 서로 상충하는 설계 원칙 사이에 적절한 타협이 필요하다.

출처 - [자바병렬프로그래밍](google.com/search?q=자바병렬프로그래밍&oq=자바병&gs_lcrp=EgZjaHJvbWUqCggBEAAYogQYiQUyBggAEEUYOTIKCAEQABiiBBiJBTIHCAIQABjvBTIKCAMQABiiBBiJBdIBCDMxNDJqMGo5qAIGsAIB8QV2EoGbIEFLUw&sourceid=chrome&ie=UTF-8)
