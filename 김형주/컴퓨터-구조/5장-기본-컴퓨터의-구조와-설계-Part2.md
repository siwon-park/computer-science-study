## [제 5장 Part-2-1](https://www.youtube.com/watch?v=eoswnrO_v9g&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=12)

### 입출력과 인터럽트 (Input-Output and Interrupt)

- 입출력 구성

  - CPU와 IO 장치의 속도 차이 제어를 위하여 Flag 사용
    - Buffer overrun 상태
    - Buffer underrun 상태
  - FGI
    - 1: 입력 가능한 상태
    - 0: 입력 블럭킹
  - FGO
    - 1: 출력 가능한 상태
    - 0: 출력 장치 사용중
  - 인터럽트
    - IEN flag에 의하여 제어
    - 입출력 전체를 제어

- 입출력 명령어

  - INP
  - OUT
  - SKI
  - SKO
  - ION
  - IOF

- 프로그램 인터럽트

  - 장치가 준비되었을 때 CPU에게 알림
  - 인터럽트 발생시 BSA 명령어처럼 동작
  - FGI, FGO 플래그 사용
    - 플래그가 set되면 $ R \leftarrow 1 $
    - R = 1 이면 다음 명령어 사이클에 인터럽트 사이클 실행
  - IEN
    - 인터럽트 enable/ disable 제어

- I/O Program

  - 입출력 인터럽트 처리 루틴의 집합

- IVT(Interrupt Vector Table)

  - 각 인터럽트에 벡터번호 부여
  - 벡터번호와 인터럽트 처리 루틴 시작번지를 Table로 유지
  - 시스템 부팅 시에 IVT는 0번 segment에 load
  - 현대의 대부분의 CPU가 IVT 사용

- 인터럽트 사이클(IC)

  - IC로 분기되는 조건

  $T_0'T_1'T_2'(IEN)(FGI+FGO): R \leftarrow 1$

  - 인터럽트 사이클의 실행

  $RT_0: AR \leftarrow 0, TR \leftarrow PC$

  $RT_1: M[AR] \leftarrow TR, PC \leftarrow 0$

  $RT_2: PC \leftarrow PC + 1, IEN \leftarrow 0, R \leftarrow 0, SC \leftarrow 0$

  

  

## [제 5장 Part-2-2](https://www.youtube.com/watch?v=zQuOYWLbCI4&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=13)

### 컴퓨터에 대한 완전한 기술 (Complete Computer Description)

- 기본 컴퓨터의 전체 명령어 set

![img](./기본 컴퓨터의 전체 명령어 set.png)

### 기본 컴퓨터의 설계 (Design of Basic Computer)

- 하드웨어 구성요소

  - 16bit 4096워드 메모리
  - 9개의 레지스터
    - AR, PC, DR, AC, IR, TR, OUTR, INPR, SC

  - 7개의 플립플롭
    - I, S, E, R, IEN, FGI, FGO

  - 2개의 디코더
    - 3* 8(Opcode), 4 * 16(타이밍)

  - 16bit 공통버스
  - 제어 논리 게이트
  - AC 입력 연결 논리회로(ALU)

- 컴퓨터의 동작 흐름

  - MRI, RRI, IO명령 사이클 구현
  - 인터럽트 사이클 구현

- 레지스터와 메모리에 대한 제어

  - AR 제어 논리 게이트의 예

  - $$
    R'T_0: AR \leftarrow PC\\
    R'T_1: AR \leftarrow IR(0-11)\\
    D'_7IT_3: AR \leftarrow M[AR]\\
    RT_0: AR \leftarrow 0\\
    D_5T_4: AR \leftarrow AR + 1\\
    $$

  - 설계 순서

    - AR에 대한 LD, CLR, INC 동작의 경우 수집
    - 각 동작들을 OR로 연결


  $$
  LD(AR) = R'T_0 + R'T_2 + D'_7IT_3\\
  CLR(AR) = RT_0\\
  INR(AR) = D_5T_4
  $$

  - 메모리 READ 제어 게이트의 예

  $$
  READ = R'T_1 + D'_7IT_3 + (D_0 + D_1 + D_2 + D_6)T_4
  $$

- 단일 플립플롭에 대한 제어

  - IEN에 대한 제어 게이트 예

    $pB_7 : IEN \leftarrow 1 $

    $pB_6 : IEN \leftarrow 0 $

    $pB_2 : IEN \leftarrow  1$

  

### 누산기 논리의 설계 (Design of Accumulator Logic)

- AC 레지스터 관련 회로
  - AC를 변경하는 경우 수집
  - LD, CLR, INC

- AC 레지스터에 대한 제어
  - LD 신호 제어
    - MRI 명령 : AND, ADD, LDA
    - RRI 명령: COM, SHR, SHL
    - IO 명령: INPR

  - INR 신호 제어
    - MRI 명령 : none
    - RRI 명령: INC
    - IO 명령: none
  - CLR 신호 제어
    - MRI 명령 : none
    - RRI 명령: CLR
    - IO 명령: none

- 가산 논리 회로
  - 회로 요소
    - AND gate
    - Full Adder
    - Inverter
    - Shifter
    - INPR/OUTR



### 수행 과제

-