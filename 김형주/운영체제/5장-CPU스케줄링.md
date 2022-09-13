### CPU 스케줄링
- 현재 ready que에 들어와 있는 CPU를 얻고자 하는 프로세스들 중에서 어떤 프로세스에게 CPU를 줄 것인지를 결정하는 것이 CPU 스케줄링이다.
- 2가지 이슈
  - 여러 개의 프로세스 중 누구에게 CPU를 줄 것인가
  - CPU를 처음부터 끝까지 다 줄 것인가 아니면 중간에 나눠서 줄 것 인가
    - 너무 많이 CPU를 붙잡고 있으면 사람들이 지나치게 오래 기다리게 된다.

### 스케줄링 성능 척도
- 시스템 입장에서 성능 척도
  - 이용률
    - keep the CPU as busy as possible
  - 처리량
    - of processes that complete their execution per time unit
- 프로그램 입장에서 성능 척도
  - 소요시간, 반환시간
    - amount of time to execute a particular process
    - 총 시간/ 기다리는 시간, CPU를 사용한 시간, 나갈 때까지 걸린 총 시간
  - 대기 시간
    - amount of time a process has been waiting in the ready queue
  - 응답 시간
    - amount of time it takes from when a request was submitted until the first response is produced, not output
    - CPU를 처음 얻기까지의 시간

### 스케줄링 알고리즘
- FCFS(First-Come First-Served)
  - 먼저오면 먼저 제공한다.
  - Convoy effect: queue에서 오래 기다리는 것
  - 비선점형 스케줄링

- SJF(Shortest-Job-Frist)
  - 짧은 시간을 사용하는 프로세스부터 사용한다.
  - 평균 대기 시간을 줄일 수 있다.
  - 더 짧은 프로세스가 오더라도 CPU를 선점하고 있음 (비선점형 방식)
  - 더 짧은 프로세스가 오면 CPU를 뺏김 (선점형 방식)
  - Starvation 문제: 긴 프로세스들이 차례를 받지 못함
  - CPU 사용시간을 정확하게 미리 알 수 없다.
    - exponential averaging 방법을 이용해서 추정함

- Priority Scheduling
  - 우선 순위 스케줄링
  - 우선 순위가 높은 스케줄링에게 CPU를 준다.
  - 우선 순위가 높은 프로세스가 오더라도 CPU를 선점하고 있음 (비선점형 방식)
  - 우선 순위가 높은 프로세스가 오면 CPU를 뺏김 (선점형 방식)
  - SJF의 Starvation 문제가 나타날 수 있다.
    - 해결방법: Aging(노화) 대기시간이 길면 우선 순위를 높혀줌

- Round Robin(RR)
  - 선점형 스케줄링
  - CPU를 줄 때 동일한 시간을 할당하고 시간이 지나면 다시 Ready queue로 돌아간다.
  - 장점: 응답 시간이 빨라진다.
  - 할당 시간을 아주 크게 잡으면 FCFS와 같은 스케줄링이 됨
  - 할당 시간이 너무 짧으면 스위칭하는데 에너지를 소모한다.

- Multilevel Queue
  - 프로세스를 여러 줄로 나누어 세운다.
  - 우선 순위나 특정 기준에 따라 나눔
  - Ready queue를 여러 개로 분할
- Multilevel feedback queue
  - 프로세스가 다른 큐로 이동 가능
  - 에이징을 이와 같은 방식으로 구현할 수 있다.
-  Multiple-Processor Scheduling
  - CPU가 여러 개인 경우 스케줄링은 더욱 복잡해짐
- Real-Time Scheduling
  - Hard real-time systems
    - 정해진 시간에 반드시 끝내야하는 스케줄링
  - Soft real-time computing
    - 일반 프로세스에 비해 높은 우선순위를 갖도록 해야 함
- 스레드 스케줄링
  - Local 스케줄링
    - 사용자가 스케줄링을 결정함
  - Global 스케줄링
    - 커널의 단기 스케줄러가 어떤 스레드를 스케줄할지 결정
- 알고리즘 평가
  - Queueing models
    - 확률 분포로 주어지는 arrival rate와 service rate 등을 통해 각종 performance index 값을 계산
  - Implementation(구현) & Measurement(성능 측정)
    - 실제 시스템에 알고리즘을 구현하여 실제 작업(workload)에 대해서 성능을 측정 비교
  - Simulation(모의 실험)
    - 알고리즘을 모의 프로그램으로 작성 후 trace를 입력으로 하여 결과 비교