## [제 5장 Part-2-1](https://www.youtube.com/watch?v=eoswnrO_v9g&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=12)

### 입출력과 인터럽트 (Input-Output and Interrupt)

#### 입출력(Input-Output)

- 입출력 구성
  - CPU와 IO장치의 속도 차이 제어를 위하여 Flag를 사용
    - CPU는 엄청 빠른 반면, IO장치는 느리기 때문
  - FGI
    - 1: 입력 가능 상태
    - 0: 입력 불가능 상태
  - FGO
    - 1: 출력 가능 상태
    - 0: 출력 불가능 상태
  - IEN(Interrupt Enable)
    - 1: 입출력을 할 수 있다
    - 0: 입출력을 할 수 없다
  - 인터럽트
    - 인터럽트가 곧 입출력. 인터럽트가 걸리는 원인이 바로 입출력이기 때문임
- 입출력 명령어
  - INP, OUT, SKI, SKO, ION, IOF

<br>

#### 인터럽트(Interrupt)

- 프로그램 인터럽트
  - 장치가 준비되었을 때 CPU에게 알림
  - 인터럽트 발생 시 BSA 명령어처럼 동작
  - FGI, FGO 플래그 사용 => R이 1이면 다음 명령어 사이클에 인터럽트 사이클을 실행함
- I/O 프로그램
  - 입출력 인터럽트 처리 루틴의 집합
- IVT(Interrupt Vector Table)
  - 현대의 CPU는 대부분 IVT를 사용함
  - 입출력이 발생할 때 점프해서 가야할 번지와 그 결과를 저장해야할 주소를 담고 있는 테이블
- 보통 사용자 프로그램이 돌아갈 때는 fetch와 decode 명령어를 수행하다가(명령어 사이클) 인터럽트를 받으면 인터럽트에 해당하는 명령어를 실행함(인터럽트 사이클)

<br>

## [제 5장 Part-2-1](https://www.youtube.com/watch?v=zQuOYWLbCI4&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=13)

### 컴퓨터에 대한 완전한 기술 (Complete Computer Description)

### 기본 컴퓨터의 설계 (Design of Basic Computer)

- 하드웨어 구성요소
  - 메인 메모리(16비트 4096워드 메모리)
  - 9개의 레지스터(AR, PC, DR, AC, IR, TR, OUTR, INPR, SC)
  - 7개의 플립플롭(I, S, E, R, IEN, FGI, FGO)
  - 2개의 디코더
  - 16비트 공통 버스(MUX; 멀티플렉서)
  - 제어 논리 게이트(제어 장치)
  - ALU

- 컴퓨터의 동작 흐름
  - PDP 전체 명령어를 활용하여 MRI, RRI, IO 사이클, 인터럽트 사이클 구현
  - 레지스터와 메모리에 대한 제어
  - 공통 버스에 대한 제어


### 누산기 논리의 설계 (Design of Accumulator Logic)

- AC 레지스터 관련 회로
  - LD 신호 제어, INR 신호 제어, CLR 신호 제어



### 가산 논리 회로

- 회로 요소
  - AND gate
  - Full Adder
  - Inverter
  - Shifter
  - INPR/OUTR

<br>