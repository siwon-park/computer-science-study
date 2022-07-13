# 제5장 기본 컴퓨터의 구조와 설계

## [Part-2-1](https://www.youtube.com/watch?v=eoswnrO_v9g&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=12)

### 입출력과 인터럽트 (Input-Output and Interrupt)

#### 1) 입출력 구성

- CPU와 IO 장치의 속도 파이 제어를 위해 FLAG 사용

  - Buffer overrun
  - Buffer underrun

- FGI

  1: 입력가능

  0: 입력불가

- FGO

  1: 출력가능

  0: 출력불가 (장치사용중)

- 인터럽트

  - IEN 플래그에 의하여 제어
  - 입출력 전체를 제어



#### 2) 프로그램 인터럽트

플래그를 사용한 통신 방법(프로그램 제어 전송)은 프로세서와 입출력 장치와의 속도 차이 때문에 매우 비능률적

- 장치가 준비되었을때 CPU에게 알림
- 인터럽트 발생시 BSA 명령어처럼 동작
- FGI, FGO 플래그 사용
- IEN



#### 3) 인터럽트 사이클

- 인터럽트 플립플롭 R은 IEN=1이고 FGO나 FGI가 1일 때, 1
- 타이밍신호 T0, T1, T2 외의 어떤 시간에서도 수행

T0` T1` T2` (IEN)(FGI+FGO) : R ← 1



## [Part-2-1](https://www.youtube.com/watch?v=zQuOYWLbCI4&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=13)

### 컴퓨터에 대한 완전한 기술 (Complete Computer Description)

- 컴퓨터 동작 흐름도
  - MRI, RRI, IO 명령 사이클 구형
  - 인터럽트 사이클 구현

![image-20220713193556885](C:\Users\jemm0\AppData\Roaming\Typora\typora-user-images\image-20220713193556885.png)



### 기본 컴퓨터의 설계 (Design of Basic Computer)

- 레지스터와 메모리에 대한 제어

- 단일 플립플롭에 대한 제어

- 공통 버스에 대한 제어

  

### 누산기 논리의 설계 (Design of Accumulator Logic)

- AC 레지스터 관련 회로

  - LD
  - INR
  - CLR

  

- 가산 논리회로

  회로요소

  - AND gate
  - Full Adder
  - Inverter
  - Shifter
  - INPR/OUTR