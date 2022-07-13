
## [제 5장 Part-1-1](https://www.youtube.com/watch?v=vSnpYzCuwVY&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=10)

### 기본 컴퓨터(Basic Computer)

PDP-11 => 현재의 컴퓨터 구조와 같음. 비트 수만 변했을 뿐 구조는 예전과 같다

CPU 칩셋 == 컴퓨터 / 나머지 === 주변 장치

<br>

### 컴퓨터의 동작

- 레지스터 내에 저장된 데이터에 대한 마이크로 연산의 시퀀스에 의하여 정의되는 내용들
- 컴퓨터는 마이크로 시퀀스에 의해 동작함

<br>

### 명령어 코드 (Instruction Codes)

- 컴퓨터에게 어떤 특별한 동작을 수행하라는 것을 알리는 비트들의 집합
- 연산 코드로 구성되어 있음
- 각 명령어는 설계자가 미리 정의한 명령어 포맷에 따라서 정의됨
- 프로그램의 실행부분에 따라서 메모리의 다른 부분에 저장
  - **메모리에는 명령어가 들어가는 부분(Code Segment)와 데이터가 들어가는 부분(Data Segment)로 나뉨**
  - **임시로 쓰는 데이터를 위한 부분을 힙 영역(Stack Segment)라고 한다.**

- 명령어 실행결과는 가산기(AC)에 저장됨

#### 컴퓨터 명령어

- 컴퓨터에 대한 일련의 마이크로 연산
- 이진 코드로 구성 => 바이너리 코드
- 명령어는 데이터와 함께 메모리에 저장됨

#### 프로그램; 기계어 프로그램(어셈블리 프로그램)

- **명령어들의 집합**
- 사용자가 원하는 연산과 피연산자가 처리되는 순서를 기술한 컴퓨터 명령어의 집합
- 명령어 처리 과정을 제어
- 내장 프로그램
  - 제어 신호에 의하여 명령어의 이진 코드를 해석하여 실행됨
  - 명령어를 저장하여 실행하는 컴퓨터의 구동 방식

<br>

#### 간접 주소(Indirect Address) 시스템

- 대부분의 경우, 직접 주소를 사용하여 데이터를 지정함
  - 0일 경우 해당 주소로 가면 실제 오퍼랜드가 있음
- 그러나 필요한 경우에는 간접 주소로 데이터를 지정함
  - 1일 경우 해당 주소로 가면 오퍼랜드가 있는 주소가 쓰여 있음
  - 색인(인덱스)의 개념과 유사함
- 간접 주소가 필요한 이유? => 컴퓨터 부품에서 반드시 간접 주소가 필요한 경우가 있음

### 컴퓨터 레지스터 (Computer Registers)

#### 기본 레지스터

- DR; Data Register(16비트)
- AR; Address Register(12비트)
- AC; Accumulator(16비트)
- IR; Instruction Register(16비트)
- PC; Program Counter(12비트)
- TR; Temporary Register(16비트)
- INPR; Input Register => 내부의 주변 장치로 부터 데이터를 받을 때 사용(8비트)
- OUTR; Output Register => 주변 장치에게 데이터를 줄 때 사용함(8비트)

64비트 컴퓨터라고 해서 64비트의 레지스터가 있는 것이 아니라 16비트 레지스터가 4개 있는 것임 따라서 16비트 컴퓨터와도 호환이 되는 것임

<br>

#### 버스 시스템의 종류

- 내부 버스; 공통 버스 시스템
  - CPU 내부 레지스터 간 연결
- 외부 버스
  - CPU 내부 레지스터와 메모리 간 연결
- 입출력 버스
  - CPU와 주변장치(I/O)와 연결

<br>

#### 공통 버스 시스템

- 내부 버스를 통칭함
- 내부 버스의 크기(Width)로 CPU 워드 크기 결정
  - 16비트 컴퓨터 => 내부 버스/레지스터 크기가 16비트
  - 32비트 컴퓨터 => 내부 버스/레지스터 크기가 32비트
- 전송 연결 통로(Register To Register)
  - 한 순간에는 하나의 전송 신호만이 버스에 존재 가능
  - 2개 이상의 신호 발생시에는 버스 충돌 발생
  - MUX(Multiplexer)에 의해 버스를 제어함

## [제 5장 Part-1-2](https://www.youtube.com/watch?v=T2oKxvinK84&list=PLc8fQ-m7b1hCHTT7VH2oo0Ng7Et096dYc&index=11)

### 컴퓨터 명령어 (Computer Instructions)

#### 기본 컴퓨터 명령어의 종류

- MRI 명령(Memory Reference Instruction); 메모리와 관련된 명령어 - 7가지
  - AND, ADD, LDA, STA, BUN, BSA, ISZ
- RRI 명령(Register Reference Instruction); 레지스터를 다루거나 레지스터 간 이동하는 명령 - 12가지
  - CLA, CLE, CMA, CME, CIR, CIL, INC, SPA, SNA, SZA, SZE, HLT
- I/O(Input - Output Instruction) 명령; 입출력에 대한 명령 - 6가지
  - INP, OUT, SKI, SKO, ION, IOF

<br>

### 타이밍과 제어 (Timing and Control)

- (예시)

### 명령어 사이클 (Instruction Cycle)

#### 명령어 사이클 단계

- 메모리(코드 세그먼트)에서 IR 레지스터로 명령어 가져오기(Fetch)
- 명령어 디코딩
- 유효 주소(Effective Address) 계산(간접 주소의 경우 실제 오퍼랜드가 있는 주소를 찾아야함)
  - 직접 주소의 경우, 직접 주소가 유효 주소임
- 명령어 실행

#### Fetch와 Decode(=> Fetch Cycle)

- T0: AR ← PC

  - ##### 프로그램 카운터의 의의; 지금 가져와야할 명령어의 주소를 항상 기억하고 있는 레지스터

- T1: IR ← M[AR], PC ← PC + 1

  - 메모리에 있는 명령어를 IR로 가져오고, 다음 명령어를 가져올 수 있도록 프로그램 카운터의 값을 1 증가시킴

- T2: D0, D1, .... , D7 ← IR(12 - 14), AR ← IR(0-11), I(FF) ← IR(15)

  - I는 플립플롭이고, 직접 주소인지 간접 주소인지 판별함

#### 명령어의 종류 결정(유효 주소 계산 전)

- MRI 명령어, RRI 명령어, IO 명령어 여부 결정

<br>

### 메모리 참조 명령어 (Memory-Reference Instuctions)

#### AND

- D0

#### ADD

- D1

#### LDA

- D2
- AC에 데이터를 집어넣으려면 메모리로부터 데이터를 가져와서 DR에 먼저 넣고, DR에서 AC로 넣는 것임 => AC와 공통버스와 직접적인 연결이 되어 있지 않음

#### STA

- D3

#### BUN

- D4

#### BSA

- D5
- 함수, 서브루틴의 구현에 사용
- 간접 주소 사용의 전형적인 예

#### ISZ

- D6
- Loop(While문, For문) 제어문 구현에 사용
