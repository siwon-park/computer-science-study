# 9장-TCP 연결지향형

## 1. TCP 프로토콜

> 전송 제어 프로토콜(Transmission Control Protocol, TCP)

### TCP가 하는일

인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 통신을 **안정적으로, 순서대로, 에러 없이** 교환할 수 있게 한다.

TCP는 UDP보다 안전하지만 느리다.

### TCP 구조

20 Bytes ~ 60 Bytes

![image](https://user-images.githubusercontent.com/93081720/210171254-43077f87-acdb-4977-b394-6ba7c00836a5.png)

#### Offset

헤더의 길이를 의미

IP와 마찬가지로 4로 나눠서 표현

#### Reserved

#### Window

데이터를 줄 때, 얼마만큼 더 보내야하는지 기록하는 곳

남아 있는 TCP 버퍼 공간

#### Sequence Number

#### Acknowledgement Number

<br>

## 2. TCP 플래그

TCP가 계속해서 통신하면서 연결 상태를 나타내는 값

C E **U A P R S F**

![image](https://user-images.githubusercontent.com/93081720/210171553-cb9a977e-b800-4aa9-ad04-955a0678cfc9.png)

### Urgent Flag

긴급 비트

급한 데이터가 있어서 처리 우선순위가 있음

Urgent Pointer와 세트

- Urgent Pointer: 긴급 비트의 위치가 어디서부터 시작하는지 알려주는 포인터

### Ack Flag

물어본 것에 대한 응답을 승인하는 플래그

### Push Flag

원래대로라면 TCP 버퍼에 공간을 채운 다음에 데이터를 전송해야하는데, Push Flag가 켜져있으면 그것과 상관없이 데이터를 밀어 넣겠다는 의미임

### Reset Flag

상대방과 연결이 되어 있는 상태에서 그 상태를 초기화하고자 할 때 사용하는 비트

### Sink Flag

동기화 비트

상대방과 연결을 시작할 때 무조건 사용하는 플래그로서, 서로의 상태를 계속해서 동기화하는 플래그

### Fin Flag

종료 비트

데이터를 다 주고 받은 다음에 연결을 끊을 때 사용하는 플래그

<br>

## 3. TCP를 이용한 통신과정

### TCP 3 Way Handshake(연결 수립 과정)

1. 클라이언트가 서버에게 요청 패킷을 보냄
2. 서버가 클라이언트의 요청을 받아들이는 패킷을 보냄
3. 클라이언트는 이를 최종적으로 수락하는 패킷을 보냄

항상 요청은 클라이언트가 서버로 보내는 것임(서버가 먼저 응답을 하지 않음)

해당 과정은 '연결 수립 과정'이기 때문에 연결 수립 이후에 다시 클라이언트가 서버로 요청을 보내야함

![image](https://user-images.githubusercontent.com/93081720/210171996-022130c6-1687-4c37-bf1d-1c3c72d61bb4.png)

### 데이터 송수신 과정

페이로드를 포함한 패킷을 주고받을 때 규칙

1. 보낸 쪽에서 또 보낼 때는 SEQ 번호와 ACK 번호가 그대로다.
2. 받는 쪽에서 SEQ 번호는 받은 ACK 번호가 된다.
3. 받는 쪽에서 ACK 번호는 받은 SEQ 번호 + 데이터의 크기다.

<br>

## 4. TCP 상태 전이도

![image](https://user-images.githubusercontent.com/93081720/210172542-239d7a1d-46a8-4103-b4a0-f36c22465547.png)