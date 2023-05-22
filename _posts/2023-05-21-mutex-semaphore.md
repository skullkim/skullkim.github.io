---
layout:       post
title:        "mutex lock vs semaphore"
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- OS
- ComputerScience
---

hardware instruction 등 하드웨어 레벨에서 critical-section problem을 해결하는 방식은 일반 애플리케이션 개발자가 직접 사용하지 못합니다. 대신, OS가 구현해 놓은 툴을 사용하고 그중 대표적인 것이 mutex와 semaphore입니다.

# Mutex(MUTual EXclusion) Lock
mutex lock을 사용하면 race condition을 방지할 수 있습니다. mutex를 올바르게 사용하기 위해선 critical section 진입 전에 락을 취득하고 critial section이 끝난 뒤 락을 풀어주어야 합니다. 이를 위해 mutex는 acquire()과 release()라는 함수를 제공합니다. 이 함수들은 atomic 하게 작동합니다.  
mutex lock을 사용해 critial section problem을 다음과 같이 해결할 수 있습니다
``` c
while (true) {
    acquire();
    // critical section
    release();
    ...
}
```
mutex lock은 락을 사용할 수 있는지를 나타내기 위해 내부적으로 하나의 boolean 변수를 사용합니다. 이 변수가 참이면 락을 취득할 수 있고 거짓이면 락을 취득하는 대신 busy waiting을 합니다.
acquire()과 release()의 대략적인 구현은 다음과 같습니다.
```c
acquire() {
    while (!available); // busy waiting
    available = false;
}

release() {
    available = true;
}
```
위에서 잠깐 언급했듯 mutex lock은 busy waiting 이란 문제를 가지고 있습니다. Busy waiting 이란 리소스 취득을 대기하면서 CPU 자원을 불필요하게 소모하는 것을 의미합니다. mutex lock의 경우 하나의 프로세스 또는 스레드가 락을 취득한 상태에서 다른 하나의 프로세스나 스레드가 락 취득을 위해 aquire()의 무한 루프를 돌때 발생합니다. 이는 다른 프로세스가 사용해야 할 자원을 점유하는 꼴이 되므로 성능 저하로 이어집니다. 
이렇게 프로세스가 락을 취득하기 위해 불필요하게 회전(spin)하면서 대기하는 방식의 락을 spin-lock이라 합니다. 하지만 spin-lock이 무조건 나쁜 것은 아닙니다. busy waiting을 하는 대신 context switching을 하지 않는다는 장점이 존재합니다. 따라서 context switching 비용이 busy waiting 비용보다 크다면 spin-lock을 사용하는 것이 더 현명합니다.
# Semaphore
세마포어는 mutex lock과 달리 하나의 정수를 사용해 락을 관리합니다. 이 때문에 프로세스 수를 카운팅 할 수 있다는 장점이 있습니다. 세마포어는 wait()와 signal()이라는 연산을 사용하며 이들 역시 atomic합니다. wait()와 signal()의 대략적인 정의는 다음과 같습니다.
```c
wait(S) {
    while (S <= 0); // busy waiting
    S--;
}

signal (S) {
    S++;
}
```
세마포어는 counting semaphore와 binary semaphore로 나뉘지고 나누는 기준은 S의 범위입니다. S가 0 <= S <= 1의 범위를 가진다면 binary semaphore입니다. 이 경우 오직 한 개의 프로세스만 락을 취득할 수 있으므로 mutex lock과 같은 역할을 한다고 볼 수 있습니다. Counting semaphore는 S에 제한이 없습니다. 따라서 유한한 개수의 프로세스를 통제해야 할 때 사용됩니다. 
## busy waiting 문제 해결하기
위에서 서술한 semaphore 방식 역시 mutex lock처럼 busy waiting 문제를 가지고 있습니다. 따라서 semaphore 작동 방식을 조금 개선해 busy waiting을 해결해 보겠습니다. 만약 프로세스가 대기가 필요하다면 waiting queue에 넣어 대기시키면 됩니다. 그 후 실행 중인 프로세스가 실행을 종료할 때 queue에서 프로세스를 꺼내주면 됩니다. 이 과정을 코드로 서술하면 다음과 같습니다.
```c
typedef struct {
    int processes; // 프로세스 수
    struct process* waitingQueue; // 대기 큐
} Semaphore; // 세마포어 타입 정의

wait (Semaphore* semaphore) {
    semaphore->processes--;
    // busy waiting을 사용한 방식과 달리 대기중인 프로세스 수가 음수일 수 있다.
    // semaphore->processes 음수의 절댓값은 대기 중인 프로세스 수를 나타낸다.
    if (semaphore->processes < 0) {
        add this process to semaphore->waitingQueue;
        sleep(); // system call
    }
}

signal(Semaphore* semaphore) {
    semaphore->processes++;
    if (semaphore->processes <= 0) {
        remove a process P from semaphore->waitingQueue;
        wakeup(P); // system call
    }
}
```
위에서 잠시 얘기했듯 sempahore에 관련된 연산들은 atomic 하게 실행돼야 합니다. 즉, 두 개의 프로세스가 동시에 같은 세마포어의 wait()과 signal()을 실행하면 안 됩니다. 싱글 프로세스 환경에선 단순히 wait()과 signal() 실행 도중 interrupt 발생을 방지하는 것만으로 atomic 함을 보장할 수 있습니다. 그러나 멀티 코어 환경에선 모든 프로세싱 코어에서 interrupt가 비활성화되어 있어야 합니다. 서로 다른 코어에서 실행 중인 서로 다른 프로세스의 instruction이 실행될 수 있기 때문입니다. 따라서 Symmetric multi-processing 환경에선 compare_and_swap()이나 spin-lock을 이용해 wait()과 signal()이 atomic하게 실행되는 것을 보장해야 합니다. 즉, 이 방식은 busy waiting을 완전히 없앤 방법이 아닙니다. 단지 busy waiting을 하는 시점을 wait()와 signal()에 국한시켜 busy waiting에 대한 단점이 없다고 할만큼 짧게 가져가는 방식입니다. 