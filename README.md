# Network4Network

| 일자 | 내용 |
|:--:| :--:|
| 2023-03-12 | 스터디 OT<br> 진행방향 및 레퍼런스 선정 |
| 2023-03-22 | OSI7계층, 네트워크 기기 및 처리범위, 응용계층, 전송계층 |
| 2023-03-26 | 네트워크 계층, 네트워크 접속 계층, URL과 리소스 |
| 2023-04-02 | TCPIP 4계층, URL과 리소스 |
| 2023-04-09 | Network Advanced 진입, ch1.HTTP&DNS,ch2.FTP |

- 일요일 오전10시 세미나 진행

## 참가자
| 김태이 | 박준우 | 심세영 | 정경훈 | 진형욱 |
| :-:  | :-:   | :-:  | :-:  | :-:   |



## 진행 방식
- Github Repository에 목차에 따른 패키지 분리
- Markdown으로 해당 개념 정리 및 예시코드 작성
- 레퍼런스를 한정하지 않으며, 신용할 수 있는 자료를 기반으로 함

<br>

- 결원 생기면 상황에 따라 조율
- 발표 시 담당자 간 협의 하에 진행.
- 발표자 외 나머지 4명이 ‘반드시’ 최소 질문 1개.

<br>

- Git의 brach 전략을 적극적으로 따른다.
    - main repo fork 후, 각자 맡은 부분 작업 후 main에 merge한다.
    - 적절치 못하거나 부족한 표현, 설명 및 예시는 Issue를 통해 공유한다.




# Table of Contents

[노션 정리](https://walnut-pan-628.notion.site/338fa3da4eb44e9e9bf53ba7e53b6cc7)

## Network Basic

- ch01. OSI 7계층 (간략히) - 형욱, 태이

- ch02. 네트워크 기기 및 처리범위 - 준우
    - LAN카드, 허브, 스위치, 브리지, 게이트웨이, 중계기, 라우터
    각 장비별로 처리하는 범위 정도만!

- ch03. TCP/IP 4계층 (응용/전송/인터넷/네트워크 액세스)
    - 응용계층 - 형욱, 준우
        - 응용프로그램 프로토콜
            - SMTP, FTP, Telnet, HTTP, SSH, DNS
    - 전송계층 - 경훈
        - TCP/UDP 간략히
    - 네트워크 계층 - 세영, 준우
        - IP, 패킷
        - 네트워크 프로토콜 표준화(ICMP, IGMP, ARP, RARP)
    - 네트워크 접속 계층 - 세영, 준우
        - 이더넷, 토큰링

- ch04. URL과 리소스 - 태이, 경훈

---

## Network Advanced

- ch01. HTTP, DNS
    - http
        - 메세지 구조(1.1 기준) - 경훈
        - 버전별 차이 0.9, 1.0, 1.1, 2.0, 3.0 - 세영
    
    - dns
        - DNS서버의 기본 동작 - 태이
        - 캐싱을 통한 DNS 성능 향상 (ISP, 브라우저, OS단 캐싱 등) - 준우
    
- ch02. UDP와 TCP 
    - UDP - 
        - UDP 체크섬 - 태이
    - TCP 
        - 패킷 교환 방식 3,4 way handshake - 형욱
        - TCP 커넥션 - 경훈
        - 지연 시간 및 패킷 손실 - 형욱
    - Go Back N이란? (전송 후 대기 프로토콜) - 세영
    - 파이프라인 프로토콜 - 준우
    - Selective repeat
    - Congestion Control
    - Flow Control

- ch03. IP address
    - subnet, subnet mask
    - gateway, DHCP


- ch04. 쿠키, 세션, 토큰
    - 쿠키
    - 세션
    - 토큰, JWT
    - 인증, 인가(개념)
        - 기본인증, 보안결함
        - 다이제스트 인증
    
- ch05. 네트워크 보안
    - CORS
    - CSRF
    - XSS
    - DDOS
    - SQL Injection

- ch06. HTTPS
    - TLS/SSL (OPTIONS, TRACE, CONNECT 메소드 추가)
    - 대칭키, 공개키 방식
    - 디지털 서명과 인증서
    - TCP/IP통신에 추가되는 과정


- ch07. 실무 네트워크 지식
    -  SOAP, REST API (추가 API 패러다임)
    - 웹 서버 - How Web Server works?
        - 웹 서버, WAS의 역활과 동작과정
        - 커넥션 수락, 메시지 수신, 요청처리, 리소스 매핑/접근, 응답 만들기, 응답 보내기의 과정

- ch08. 웹 캐시
    - 캐시 기본 동작
    - 검증 헤더와 조건부 요청
    - 프록시 캐시
    - 캐시 무효화

-  ch9. 프록시 서버
    - 프록시를 쓰는 이유?
        - 프록시 요청 특징
    - 메시지 추적
    - 프록시 인증

---

- 게이트웨이, 터널, 릴레이 - 중요도 낮음
- 네트워크에서 게이트웨이의 역할
    - 프로토콜 게이트웨이
    - 리소스 게이트웨이
    - 어플리케이션 인터페이스와 웹 서비스
        - 터널, 릴레이
- 웹 로봇 - How Serach Engine works?
    - 크롤러와 크롤링
    - 봇의 HTTP
    - 봇 차단 및 에티켓
    - 간략한 검색엔진 원리

- HTTP 2.0 - 1.0과의 차이 및 성능개선, How?
    - 2.0 등장 배경과 특징
    - 구조와 동작원리

- 엔터티와 인코딩
    - TBD

- 국제화
    - TBD

- 웹 호스팅
    - TBD

- 배포 시스템
    - TBD

- 리다이렉션 & 부하 균형
    - TBD

Reference List
- [네트워크 개론](https://www.hanbit.co.kr/store/books/look.php?p_code=B7721595096)

- [쉽게 배우는 데이터 통신과 컴퓨터 네트워크](https://www.hanbit.co.kr/store/books/look.php?p_code=B3980824801)

- [리얼월드 HTTP](https://www.hanbit.co.kr/store/books/look.php?p_code=B7009240426)

- [HTTP 완벽 가이드](http://www.yes24.com/Product/Goods/15381085)

- [1%의 네트워크 원리](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=437756)

