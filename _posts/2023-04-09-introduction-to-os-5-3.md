---
layout:       post
title:        "Chapter5-3 임계구역 해결 방법"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
- ComputerScience
---

  임계구역 문제를 해결하는 가장 단순한 방법은 락을 거는 거다. 임계구역 문제를 해결하기 위한 세 가지 조건인 상호 배제, 한정 대기, 진행의 융통성을 모두 만족하는 락, 락 해제, 동기화 구현 방법을 알아보자.

  아래 설명에서 다음과 같은 코드를 사용할 예정이다.
``` c
#include <stdio.h>
 
// C 에는 boolean이 없어 직접 정의한다.
typedef enum {false, true} boolean;
extern boolean lock = false;
extern int balance;
 
int main() {
    while(lock == true);
    lock = true;
    balance += 10;
    lock = false;
}
```
# 임계구역해결 조건을 고려한 코드 설계
## 상호 배제 문제
  위 코드에서 11번째 줄이 임계구역, lock이 공유변수이다.

  위 코드는 언뜻 문제가 없어 보이지만 다음과 같은 상황에서 문제가 발생한다.

  1. 두 개의 프로세스가 동시에 위 프로그램을 실행한다.

  2. 첫 번째 프로세스 P1은 while(lock == true);를 실행한다. 임계구역에 프로세스가 없어 루프를 종료하고 다음 코드를 실행한다. 다음 코드를 실행하기 전 timeout으로 P1이 준비 상태가 된다. 이때의 lock은 false이다.

  3. 두 번째 프로세스 P2도 while(lock == true);를 실행한다. lock이 false이기 때문에 P2는 임계구역에 진입할 수 있다.

  4. P1이 lock=true;를 실행해 임계구역에 락을 건다.

  5. P2가 lock=true;를 실행해 임계구역에 락을 건다. 결국 둘 다 임계구역에 진입하게 된다.

  위 시나리오는 상호 배제 조건을 보장하지 못한다. 위 코드의 또 다른 문제는 busy waiting을 하기 때문에 리소스 낭비가 심하다는 것이다.
  ## 한정 대기 문제
  상호 배제를 만족하기 위해 다음과 같이 코드를 수정해 보자.
``` c
#include <stdio.h>
 
// C 에는 boolean이 없어 직접 정의한다.
typedef enum {false, true} boolean;
extern boolean lock1 = false;
extern boolean lock2 = false;
extern int balance;
 
// process P1
int main() {
    lock1 = true;
    while(lock2 == true);
    balance += 10;
    lock1 = false;
}
 
// process P2
int main() {
    lock2 = true;
    while(lock1 == true);
    balance += 10;
    lock2 = false;
}
```

 위 코드는 우선 락을 걸고 다른 프로세스에 락이 있는지 확인하기 때문에 두 프로세스의 상호 배제가 보장된다. 하지만, 위 코드는 다음과 같은 상황에서 데드락이 발생한다.

  1. P1은 lock1=true;를 실행하고 timeout이 나서 P2가 실행상태가 된다.

  2. P2도 lock2=true;를 실행하고 timeout이 나서 P1이 실행상태가 된다.

  3. P2, P1 각각 while(lock1==true);와 while(lock2==true);에서 빠져나오지 못한다.

  위 코드는 데드락 문제뿐만 아니라 프로세스가 늘어날수록 락을 위한 공유 변수가 많아져야 한다는 문제도 가지고 있다.
  ## process flexibility 문제
  문제 해결을 위해 코드를 다음과 같이 수정해 보자.
``` c
#include <stdio.h>
 
extern int lock = 1;
 
// process P1
int main() {
    while(lock == 2);
    balance += 10;
    lock = 2;
}
 
// process P2
int main() {
    while(lock == 1);
    balance += 10;
    lock = 1;
}
```
락을 거는 공유 변수를 boolean이 아닌 값을 통해 확인하는 방식이다. 잠금을 확인하는 방식이 하나라 상호 배제와 한정 대기를 보장한다. 그러나 두 프로세스가 반드시 번갈아 실행돼야 한기 때문에 process flexibility를 해친다. 하나의 프로세스가 두 번 연속 실행되지 못한다. 이렇게 하나의 프로세스가 다른 프로세스를 방해하는 현상을 경직된 동기화(lockstep synchronization)라 한다.

## 하드웨어적인 해결 방법
  처음 제시했던 코드는 while(lock==true);와 lock=true;사이에서 타임아웃이 걸릴 때 문제가 된다. 따라서 다음과 같이 수정해 하드웨어적으로 두 명령어를 동시에 실행하면 임계구역 문제를 해결할 수 있다.
``` c
#include <stdio.h>
 
typedef enum {false, true} boolean;
extern boolean lock = false;
extern int balance;
 
int main() {
    while(testandset(&lock));
    balance += 10;
    lock = false;
}
```
  testandset은 lock이라는 변수 값을 테스트하고 1로 바꾸는 작업을 하나의 atomic operation으로 실행한다. atomic operation은 인터럽트가 발생하는 하나의 단위이다. 이 방법은 여전히 busy waiting을 해결하지 못했다는 문제가 있다.

# 피터슨 알고리즘
피터슨 알고리즘은 임계구역 문제를 해결한 알고리즘 중 하나이다. 이 알고리즘의 코드는 다음과 같다.
``` c
#include <stdio.h>
 
// C 에는 boolean이 없어 직접 정의한다.
typedef enum {false, true} boolean;
extern boolean lock1 = false;
extern boolean lock2 = false;
extern in turn = 1;
extern int balance;
 
// process P1
int main() {
    lock1 = true;
    turn = 2;
    while(lock2 == true && turn == 2);
    balance += 10;
    lock1 = false;
}
 
// process P2
int main() {
    lock2 = true;
    turn = 1;
    while(lock1 == true && turn == 1);
    balance += 10;
    lock2 = false;
}
```
  피터슨 알고리즘은 변수 turn을 이용해 두 프로세스가 동시에 lock을 설정해 임계구역에 못 들어가는 상황을 대비한다. P2의 잠금 설정 여부와 관련 없이 곧바로 turn=1로 바꾸면 프로세스 P1은 임계구역에 진입해 작업을 마친 후 잠금을 해제하고 임계구역을 빠져나온다. P2도 같은 방식을 사용한다. 

  피터슨 알고리즘은 오직 두 개의 프로세스만 사용 가능하다는 문제가 있다. 프로세스가 늘어날수록 공유 변수를 추가하고 코드를 변경해야 한다.
  # 데커 알고리즘
  데커 알고리즘 코드는 다음과 같다.
``` c
#include <stdio.h>
 
// C 에는 boolean이 없어 직접 정의한다.
typedef enum {false, true} boolean;
extern boolean lock1 = false;
extern boolean lock2 = false;
extern in turn = 1;
extern int balance;
 
// process P1
int main() {
    // P1은 잠금을 건다
    lock1 = true;
    // P2의 잠금이 걸렸는지 확인한다
    while(lock2 == true) {
        // 프로세스 P2도 잠금을 걸었다면 누가 먼저인지 확인한다
        if (turn == 2) {
            // 프로세스 P2의 차례이므로 P1은 락을 풀고
            lock1 = false;
            // P2가 작업을 마칠때 까지 기다린다.
            while (turn == 2);
            lock1 = true;
        }
    }
    // 프로세스 P1의 차례(turn == 2)라면 임계구역에 진입히한다.
    balance += 10;
    turn = 2;
    lock1 = false;
}
 
// process P2
int main() {
    lock2 = true;
    while(lock1 == true) {
        if (turn == 1) {
            lock2 = false;
            while (turn == 1);
            lock2 = true;
        }
    }
    balance += 10;
    turn = 1;
    lock2 = false;
}
```
데커 알고리즘 역시 프로세스 개수가 증가하면 공유 변수가 증가한다는 문제가 있고 로직이 매우 복잡하다.

# 세마포어(semaphore)
  위에서 설명한 알고리즘들은 너무 복잡하고, busy waiting을 사용하기 때문에 리소스 낭비도 심하다. 이런 단점들을 해결하기 위해 에츠로흐 데이크트리(Edsger Djikstra)는 세마포어라는 알고리즘을 제안했다.

  세마포어 프로세스는 임계구역에 진입하기 전에 스위치를 사용 중으로 놓고 임계구역으로 들어간다. 이후에 도착하는 프로세스는 앞의 프로세스가 작업을 마칠 때까지 기다린다. 프로세스가 작업을 마치면 세마포어는 다음 프로세스에 임계구역을 사용하라는 동기화 신호를 보낸다.
``` c
  #include <stdio.h>
 
extern int RS;
 
// process P1
int main() {
    // n은 공유 가능한 리소스의 수
    semaphore(n);
    // 임계구역 진입 전 사용 표시
    p();
    balance += 10;
    // 임계구역 나온 후 나옴 표시
    v();
}
 
// 전역변수 RS를 n으로 초기화한다. 
// RS에는 현재 사용 가능한 자원의 수가 저장된다.
void semaphore(n) {
    RS = n;
}
 
// 잠금을 수행한다
void p() {
    // 사용 가능한 자원이 있으면 하나를 감소시키고 임계구역에 진입한다.
    if (RS > 0) RS--;
    // 사용 가능한 자원이 없다면 대기한다.
    else block();
}
 
// 잠금 해제와 동기화를 같이 수행한다.
void v() {
    RS++;
    // 세마포어에서 기다리는 프로세스에게 임계구역에 진입해도 좋다는 신호를 보낸다.
    wake_up();
}
```
세마포어에서 락이 해제되기를 기다리는 프로세스는 세마포어 큐에 저장되어 있다가 wake_up 신호를 받고 임계구역에 진입하기에 busy waiting을 하지 않아도 된다. 하지만, p()나 v()가 실행되는 도중 다른 코드가 실행되면 상호 배제와 한정 대기 조건을 보장하지 못한다. 따라서 testandset을 이용해 분리 실행되지 않게 해야 한다.

# 모니터(monitor)
  세마포어는 피터슨이나 데커보다는 단순하지만 잘못 사용하면 임계구역을 보호받지 못하는 문제가 있다. 예컨대 프로세스가 세마포어를 사용하지 않거나, 위 예시에서의 p()나 v()를 잘못된 부분에서 호출하는 등의 경우 임계구역이 보호받지 못한다. 만약 모든 프로세스가 세마포어 알고리즘을 따른다면 p()와 v()를 외부로 노출시키지 않고 자동으로 처리하게 하면 된다. 이를 구현한 것이 모니터이다. 모니터는 공유 자원들 내부적으로 숨기고 공유 자원에 점근 하기 위한 인터페이스만 제공해 리소스를 보호하고 프로세스 간 동기화를 시킨다.

  모니터의 작동 원리는 다음과 같다.

  1. 임계구역으로 지정된 변수나 직원에 접근하고자 하는 프로세스는 직업 p()나 v()를 사용하지 않고 모니터에 작업 요청을 한다.

  2. 모니터는 요청받은 작업을 모니터 큐에 저장한 뒤 순서대로 처리하고 그 결과만 해당 프로세스에 알려준다.

 

출처 - 쉽게 배우는 운영체제