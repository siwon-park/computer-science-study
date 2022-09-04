# 5장-CPU 스케줄링

4장 프로세스 관리2 48분 14초부터 듣기

### CPU and I/O Bursts in Program Execution

어떤 프로그램이든 CPU를 실행하고 있는 단계와 I/O를 실행하는 단계를 번갈아가며 실행됨

사람과 상호작용이 많은 프로그램일 수록 해당 스테이지들이 많이 반복됨

컴퓨터 안의 작업은 CPU bound job과 I/O bound job으로 나뉘어져 섞여 있음

### CPU-burst Time의 분포

![image](https://user-images.githubusercontent.com/93081720/188294882-aa375601-69fb-4e19-97dd-894bd9aa9674.png)

그래프 해석

- I/O bound job이 CPU를 많이 쓰는 것처럼 오해할 수 있으나, 실제로 CPU를 많이 쓰는 것은 CPU bound job임
- I/O 작업을 위해 CPU를 수행하는 단계와 I/O를 수행하는 단계가 번갈아가면서 일어나서 CPU의 등장 빈도가 많아진 것이지, CPU를 많이 쓰는 것이 아님
- 오히려 CPU를 많이 쓰는 것은 CPU bound job이고, CPU를 한번 잡고 계속해서 쓰고 있으므로, CPU의 등장 빈도가 낮은 것임

### 프로세스의 특성 분류

- I/O bound process
  - CPU를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 일

- CPU bound process
  - 계산 위주의 작업


### CPU Scheduler & Dispatcher

#### CPU Scheduler

Ready 상태의 프로세스 중에서 CPU를 줄 프로세스를 결정하는 것

#### Dispatcher

CPU를 누구한테 줄 지 결정했으면, CPU 제어권을 선택된 프로세스에게 넘기는 것(이 과정을 context switch라고 함)

#### CPU 스케줄링이 필요한 경우?

프로세스에 다음과 같은 상태 변화가 있는 경우에 CPU 스케줄링이 필요하다

- Running → Blocked(예 - I/O를 요청하는 시스템 콜 발생 시)
- Running → Ready(예 - 할당 시간 만료로 타이머에 의한 인터럽트 발생시)
- Blocked → Ready (예 - I/O 완료 후 인터럽트; 단, I/O가 끝났다고 해서 무조건 CPU를 바로 넘기는 것은 아님)
- Terminate



### Preemptive & Nonpreemptive

#### Preemptive

강제로 빼앗음(선점)

#### Nonpreemptive

강제로 빼앗지 않고, 자진 반납함(비선점)