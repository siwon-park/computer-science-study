# 5장-CPU-스케줄링

[강의 링크](http://www.kocw.net/home/search/kemView.do?kemId=1046323)

<br>

## 1. CPU Scheduling의 필요성

### 1) CPU burst, I/O burst

![image-20220906183630032](https://raw.githubusercontent.com/JaeKP/image_repo/main/img/image-20220906183630032.png)



- 프로그램 실행 중 주어진 명령문의 종류에 따라 구분한다.
  - I/O burst: I/O를 실행하고 있는 단계
  - CPU burst: CPU만 연속적으로 사용하면서 명령어를 실행하는 단계
- CPU burst와 I/O burst를 번갈아가면서 프로그램을 실행한다. 

<br>

### 2) CPU -burst Time

![image-20220906183732999](https://raw.githubusercontent.com/JaeKP/image_repo/main/img/image-20220906183732999.png)

- 여러 종류의 job(=process)이 섞여 있기 때문에 CPU 스케쥴링이 필요하다.
  - CPU과 I/O 장치 등 시스템 자원을 골고루 효율적으로 사용해야 한다. 
- I/O bound job
  - interactive한 job이 많다. (interative job에게 적절한 response 제공 요망)
  - CPU를 잡고 계산하는 시간 보다 I/O에 많은 시간이 필요한 job이다. 
  -  I/O 요청이 주를 이루어 CPU를 사용하는 시간은 짧지만 많은 명령을 수행한다.(빈도가 높다)
  - many short CPU bursts (large number of short CPU bursts)
- CPU bound job
  - 계산위주의 job이다.
  - few very long CPU bursts (small number of long CPU bursts)

<br>

## 2. CPU Scheduler

### 1) 기본 개념

> Ready 상태의 프로세스 중에서 이번에 CPU를 줄 프로세스를 고른다.

CPU를 누구에게 줄 지 결정했으면, Dispatcher를 통해 CPU제어권을 CPU Scheduler에 의해  프로세스를 넘긴다. 이 과정을 문맥 교환이라고 한다.

CPU 스케줄링이 필요한 경우는 프로세스에게 다음과 같은 상태 변화가 있는 경우이다. 

- Running =>  Blocked (예: I/O 요청하는 시스템 콜) `nonpreemptive (자발적)`
- Running => Ready (예: 할당시간 만료로 timer interrupt) `preemptive (비자발적)`
- Blocked => Ready (예: I/O 완료 후 인터럽트) `preemptive(비자발적)`
- Terminate `nonpreemptive(자발적)`

 <br>



