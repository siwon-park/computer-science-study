# 6장-Process-Synchronization

[강의 링크] (http://www.kocw.net/home/search/kemView.do?kemId=1046323)

> 공유데이터의 동시 접근은 데이터의 불일치 문제를 발생시킨다. 
>
> 일관성 유지를 위해서는 협력 프로세스 간의 실행 순서를 정리해주는 메커니즘이 필요하다. 

<br>

### 1. 기본 개념

### 1)  Race Condition

> Race Condition(경쟁 상태)는 여러 프로세스들이 동시에 데이터를 접근하는 상황에서 어떤 순서로 접근하느냐에 따라 결과가 달라지는 상황을 의미한다. 

여러 프로세스들이 동시에 공유 데이터를 접근하는 상황으로 데이터의 최종 연산 결과는 마지막에 그 데이터를 다룬 프로세스에 따라 달라진다. 

- Kernel 수행 중 인터럽트 발생
  - 커널모드 running 중 인터럽트가 발생하여 인터럽트 처리 루틴이 수행되면 양쪽 다 커널 코드이므로 kernel address space를 공유한다. 
  - 해결책: 커널모드의 수행이 끝나기 전에는 인터럽트를 받지 않는다. (disable/enable)
- Process가 System call을 해서 kernel mode로 수행 중인데 context swtich가 일어난 경우
  - 두 프로세스의 주소 공간에서ㄷ는 데이터를 공유하지 않지만 시스템 콜을 수행할 때는 둘 다 커널 주소 공간의 데이터에 접근한다. 
  - 커널 주소 공간에 작업을 수행하는 도중에 CPU를 빼앗으면 race condition이 발생한다. 
  - 해결책: 커널 모드를 수행 중일 땐 CPU가 preempt 하지 않고, 커널 모드에서 유저 모드로 돌아갈 때 preempt 한다. 
- Multiprocessor에서 shared-memory 내의 kernel data
  - 해결책: 커널 내부에 있는 공유 데이터에 접근할 때마다 그 데이터에 대해서 lock/unlock 한다. 

**race condition을 막기 위해서는 concurrent process는 동기화 되어야 한다.** 

<br>

### 2) Critical-Section

> n개의 프로세스가 공유 데이터를 동시에 사용하기를 원하는 경우로 race condition이 발생할 수 있는 특정 부분을 의미한다. 

- 각 프로세스의 code segment에는 공유 데이터를 접근하는 코드인 critical section이 존재한다.
- 해결 법의 충족 조건
  - Mutual Exclusion (상호 배제): 프로세스가 critical section 부분을 수행 중이면 다른 프로세스들은 그들의 critical section에 들어가면 안된다. 
  - Progress (진행): 아무도 critical section에 있지 않은 상태에서 critical section에 들어가고자 하는 포르세스가 있으면 critical section에 들어가게 해주어야 한다. 
  - Bounded Waiting (유한 대기): 프로세스가 critical section에 들어가려고 요청한 후부터 그 요청이 허용될 떄까지 다른 프로세스들이 critical section에 들어가는 횟수에 한계가 있어야 한다. 

- 하드웨어적으로 현재 상태를 확인하고 변경하는 Test & modify를 atomic하게 수행할 수 있도록 지원하면 간단하게 해결할 수 있다. 
  - 데이터를 읽으면서 동시에 쓰는 것이 하나의 instruction으로 수행이 가능하다면, 수행 중 CPU를 빼앗기지 않는다. 
  - Test_and_set(a): a의 값을 읽고 a의 값을 1로 세팅한다. => 하나의 instruction이다. 
    - lock이 안 걸렸다면, 걸고 들어간다. 
    - lock이 걸려있으면, while 문을 돌면서 기다린다. 

```c
// Synchronization variable: 
boolean lock = false;

// Process Pi
do {
    while(Test_and_Set(lock));
    critical section
    lock = false;
    remainder section
}
```

<br>

## 2. Semaphores

> 소프트웨어상에서 Critical Section 문제를 해결하기 위한 동기화 도구로 공유자원을 획득하고 반납하는 것을 처리한다. 
>
> 주로 S라는 정수형 변수로 나타내며, 이는 사용 가능한 자원의 개수를 의미한다.

- Counting Semaphore
  - 자원의 개수가 여러 개 있다. (여분의 자원을 사용 가능)
  - 도메인이 0 이상인 임의의 정수 값
  - 주로 resource counting에 사용한다. 

- Binary Semaphore
  - 변수가 0 혹은 1인 경우이다. (자원의 개수가 1개인 경우)
  - 0 또는 1 값만 가질 수 있는 Semaphore
  - 주로 mutual exclusion에 사용한다. 

<br>


세마포어 변수는 오직 두 개의 atomic 한 연산을 통해서 접근할 수 있다

- p 연산: 공유 데이터를 획득 하는 과정
- v 연산: 공유 데이터를 반납하는 과정 

<br>

### 1)  Busy-wait

```c
// Synchronization variable: 
sempaphore mutex; 

ProcessPi
do {
    P(mutex);  // if positive, dec-&-enter, Othrewise, wait
    critical section
    V(mutex);  // Increment semaphore
    remainder section
}white(1);
```

- Busy Waiting이 발생한다. 
  - Busy Waiting:  Critical Section 에 진입해야하는 프로세스가 진입 코드를 계속 반복 실행해야 하여 CPU 시간을 낭비하는 것.
- 그래서 Block & Wake up 방식을 사용한다. 

<br>

### 2)  Block & Wake up 

> Critical Section으로의 진입에 실패한 프로세스를 기다리게 하지 않고 Block 시킨다. 
> Critical Section에 자리가 나면 다시 깨워줌으로써 Busy waiting에서의 CPU 낭비 문제를 해결한다. 

semaphore를 획득 하지 못하면 block 되고 PCB를 큐에 넣고 semaphore를 기다린다. 

```c
typedef struct
{
    int value;          // semaphore
    struct process *L;  // process wait queue
}
```

| 단어   | 설명                                                         |
| ------ | ------------------------------------------------------------ |
| block  | 커널은 block을 호출한 프로세스를 suspend 시킨다. <br />이 프로세스의 PCB를 semaphore에 대한 wait queue에 넣는다. |
| wakeup | block된 프로세스 P를 wakeup시킨다.<br />이 프로세스의 PCB를 ready queue로 옮긴다. |

<br>

```c
// P(S)
S.value++; // prepare to enter
if (S.value < 0) // Oops, negative, I cannot enter
{
    add this process to S.L;
    block();
}

// V(S)
S.value++;
if (S.value <= 0) {
    remove a prosess P from S.L;
    wakeup(P);
} 
```

<br>

### 3) Busy-wait vs Block/Wakeup

- Critial Section의 길이가 긴 경우 Block/Wakeup이 적당하다.
- Critial Section의 길이가 매우 짧은 경우 Block/Wakeup 오버 헤드가Busy-Wait 오버헤드보다 더 커질 수 있다. 
- 일반적으로는 Block/Wakeup방식이 더 좋다.

<br>

### 4) 문제점

- Deadlock
  - 둘 이상의 프로세스가 서로 상대방에 의해 충족될 수 있는 event를 무한히 기다리는 현상
  - 세마포어가 Ready Queue 를 가지고 있고, 둘 이상의 프로세스가 Critical Section 진입을 무한정 기다리고 있어서 Critical Section에서 실행되는 프로세스는 진입 대기 중인 프로세스가 실행되야만 빠져나올 수 있는 상황을 지칭한다.

- Starvation
  - 프로세스가 suspend된 이유에 해당하는 세마포어 큐에서 빠져나갈 수 없는 현상 (Indefinite blocking)


<br>