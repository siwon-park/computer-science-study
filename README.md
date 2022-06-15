# 👩‍💻 computer-science-study 👨‍💻

[스터디 노션 페이지](https://evanescent-tuba-146.notion.site/CS-STUDY-90db0300708249e1a3e5b57082e307e5)

computer-science 발표 스터디 입니다.

- 매주 정해진 분량의 강의를 듣습니다.  
- 추가적으로 공부한 내용을 발표를 통해 공유합니다. 

<br>

## ✅ STUDY!

#### 이전 자료

| 주제                                               | 발표일   | 발표자                                      |
| -------------------------------------------------- | -------- | ------------------------------------------- |
| [패킷 네트워크 개요 / TCP vs UDP](김지수/20220613) | 22/06/15 | [김지수](https://github.com/jijisusu3)      |
| [운영체제와 컴퓨터](김형주/20220613)               | 22/06/15 | [김형주](https://github.com/brotherweekkim) |
| [NoSQL](정제희/20220613)                           | 22/06/15 | [정제희](https://github.com/jeheehee)       |



### 1) 컴퓨터-구조

| 파트 | 진행상태             | 강의내용                            | 발표자 | 발표 주제 | 발표일   |
| ---- | -------------------- | ----------------------------------- | ------ | --------- | -------- |
| 1    | :white_large_square: | 컴퓨터-구조 개요                    |        |           | 22/06/22 |
| 1    | :white_large_square: | 1장 디지털 논리 회로 및 강의소개    |        |           | 22/06/22 |
| 1    | :white_large_square: | 2장 디지털 부품                     |        |           |          |
| 1    | :white_large_square: | 3장 데이터의 표현                   |        |           |          |
| 1    | :white_large_square: | 4장 레지스터 전송과 마이크로 연산   |        |           |          |
| 1    | :white_large_square: | 5장 기본 컴퓨터의 구조와 설계-Part1 |        |           |          |
| 1    | :white_large_square: | 5장 기본 컴퓨터의 구조와 설계-Part2 |        |           |          |
| 2    | :white_large_square: | 6장 기본 컴퓨터 프로그래밍          |        |           |          |
| 2    | :white_large_square: | 7장 마이크로 프로그램               |        |           |          |
| 2    | :white_large_square: | 8장 중앙 처리 장치                  |        |           |          |
| 2    | :white_large_square: | 9장 파이프라인과 벡터 처리          |        |           |          |
| 2    | :white_large_square: | 10장 컴퓨터 산술 연산               |        |           |          |
| 2    | :white_large_square: | 11장 입출력 구조                    |        |           |          |
| 2    | :white_large_square: | 12장 메모리 구조                    |        |           |          |

---

<br>

### 2)  운영체제

| 파트 | 진행상태             | 강의내용                                    | 발표자 | 발표 주제 | 발표일 |
| ---- | -------------------- | ------------------------------------------- | ------ | --------- | ------ |
| 1    | :white_large_square: | 1, 2장 운영체제 개요 및 컴퓨터시스템의 구조 |        |           |        |
| 1    | :white_large_square: | 3장 프로세스                                |        |           |        |
| 1    | :white_large_square: | 4장 프로세스 관리                           |        |           |        |
| 1    | :white_large_square: | 5장 CPU 스케쥴링                            |        |           |        |
| 1    | :white_large_square: | 6장 프로세스 동기화                         |        |           |        |
| 1    | :white_large_square: | 7장 교착상태                                |        |           |        |
| 2    | :white_large_square: | 8장 메모리 관리                             |        |           |        |
| 2    | :white_large_square: | 9장 가상 메모리                             |        |           |        |
| 2    | :white_large_square: | 10, 11장 파일 시스템과 구현                 |        |           |        |
| 2    | :white_large_square: | 12장 디스크 관리 및 스케쥴링                |        |           |        |

---

<br>

### 3) 네트워크

| 파트 | 진행상태             | 강의내용                | 발표자 | 발표 주제 | 발표일 |
| ---- | -------------------- | ----------------------- | ------ | --------- | ------ |
| 1    | :white_large_square: | 1, 2장 네트워크와 모델  |        |           |        |
| 1    | :white_large_square: | 3장 데이터 통신         |        |           |        |
| 1    | :white_large_square: | 4장 IP 주소             |        |           |        |
| 1    | :white_large_square: | 5장 ARP 프로토콜        |        |           |        |
| 1    | :white_large_square: | 6장 IPv4, ICMP 프로토콜 |        |           |        |
| 2    | :white_large_square: | 7장 전송계층 및 포트    |        |           |        |
| 2    | :white_large_square: | 8장 UDP 비연결지향형    |        |           |        |
| 2    | :white_large_square: | 9장 TCP 연결지향형      |        |           |        |
| 2    | :white_large_square: | 10장 NAT와 포트포워딩   |        |           |        |
| 2    | :white_large_square: | 11장 HTTP 프로토콜      |        |           |        |

<br>

## ✅ GIT CONVENTION

### 1) COMMIT

- `type: 자유 `
- **type: 하고자 하는 행위를  명령문으로 적는다.** 
  - Add  Files
  - Update Files
  - Delete Files
  - Merge Files
  - etc..

```bash
git commit -m "AddFiles: 발표자료 업로드 "
```

<br>

### 2) PR 

- PR 제목: `이름 / 큰 주제 / 세부 주제`

```
박재경 / 운영체제 / 프로세스와 스레드
```

<br>

- PR 내용: 자유 
  - 다른 스터디원들이 자료를 이해하는 데 도움이 되는 설명을 간단히 적어주세요.
  - 발표자료를 만들면서 느낀 간단회고를 작성하는 것도 좋습니다.

<br>