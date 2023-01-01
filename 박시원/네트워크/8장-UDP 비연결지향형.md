# 8장-UDP 비연결지향형

## 1. UDP 프로토콜

> 사용자 데이터그램 프로토콜(User Datagram Protocol, UDP)
>
> 유니버셜 데이터그램 프로토콜(Universal Datagram Protocol)

### UDP가 하는 일

UDP의 전송 방식은 너무 단순해서 서비스의 신뢰성이 낮고, 데이터그램 도착 순서가 바뀌거나, 중복되거나 심지어는 통보 없이 누락시키기도 한다.

UDP는 일반적으로 오류의 검사와 수정이 필요 없는 프로그램에서 수행할 것으로 가정한다.

### UDP 프로토콜의 구조

![image](https://user-images.githubusercontent.com/93081720/210170889-501c97cb-b311-4f3d-aff7-c11c05a396d6.png)

<br>

## 2. UDP 프로토콜을 사용하는 프로그램

### UDP 프로토콜을 사용하는 대표적인 프로그램들

#### DNS 서버

도메인을 물으면 IP를 알려주는 DNS 서버

- 예) www.naver.com의 IP주소를 알고자할 때 UDP프로토콜을 사용해서 알려줌

#### TFTP 서버

UDP로 파일을 공유하는 서버

#### RIP 프로토콜

라우팅 정보를 공유하는 프로토콜