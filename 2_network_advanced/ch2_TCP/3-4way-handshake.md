## 3,4way handshake

### Transport Layer

![images_averycode_post_01f46d6e-a577-41e7-b99f-31d67a512ce0_image](https://user-images.githubusercontent.com/100752008/230778456-66c7954b-583e-4354-87b9-1093d61410ba.png)

OSI 7 레이어중 Transport(전송) 계층은 상위 계층들이 데이터 전달의 유효성이나 효율성을 생각하지 않도록 해주며 , 사용자들이 데이터를 주고 받을 수 있도록 해주는 계층이다.  

전송 프로토콜 중 잘 알려진 것이 바로 **TCP**와 **UDP**가 있다.


### TCP
- 인터넷상에서 데이터를 메시지 형태로 보내기 위해 IP와 함께 사용하는 프로토콜 

- 애플리케이션에게 신뢰적이며, 연결형 서비스를 제공

- 3way h 과정을 통해 연결을 설정하고, 4way h 과정을 통해 해제한다

- UDP보다 속도가 느리다(데이터의 흐름제어와 혼잡제어 하기 때문)


### UDP

- 데이터를 단위로 처리하는 프로토콜(비연결형)

- 할당되는 경로가 없이 각각의 패킷이 다른 경로로 전송되고 독립적인 관계를 지님

- 연결 설정과 해제하는 과정이 존재하지 않음(3/4 way handshake X)

- 흐름제어 혼잡제어를 하지 않아 속도가 빠르며 네트워크 부하가 적다(=>데이터 전송 신뢰성 낮음)

![images_averycode_post_7ced087c-a2f1-4a0a-a00e-c1c65391e30c_image](https://user-images.githubusercontent.com/100752008/230778415-7d2f7b9a-c2ec-40b8-8b47-21388f9bc689.png)

## 3-way handshake

3-way handshake는 **TCP 연결 설정** 과정을 의미한다.

![images_averycode_post_cd53e336-a624-4f8a-b7e5-20fe62eb6648_image](https://user-images.githubusercontent.com/100752008/230778480-e704ae9f-284b-4073-a683-aa7bb8f03fd2.png)


### 작동방식

Client는 서버와 연결하기 위해 3-way handshake를 통해 연결 요청을 하게 된다

Client가 연결을 먼저 시도한 요청자, 연결 요청을 받은 수신자를 Server라고 생각하자

>플래그(특정 동작을 수행할지 말지 결정하는 변수)정보 

> SYN : 연결 설정. 시퀸스 넘버를 랜덤으로 설정하여 세션을 연결하는데 사용
> ACK : 응답 확인. 패킷을 받았다는 것을 의미


#### No.1 [Client -> SYN -> Server]

클라이언트는 서버와 연결을 위해 `SYN` 연결 요청

#### No.2 [Server -> SYN + ACK -> Client ]

서버가 SYN을 받고, 받았다는 신호인 `ACK`, `SYN`패킷을 Server => Client로 전송

#### No.3  [Client -> ACK -> Server]

클라이언트는 서버의 응답 `ACK`와 `SYN` 패킷을 받고, `ACK`을 서버로 전송 후 연결 성립이 된다 

이 과정에서 클라이언트와 서버 사이에 3번의 핸드쉐이킹을 거쳐 3번의 Segment가 교환되는 것을 확인할 수 있는데 이것을 3-way handshake 기본 매커니즘이다.

## 4-way handshake
4-way handshake는 **TCP 연결 해제** 과정을 의미한다. 

![다운로드 (1)](https://user-images.githubusercontent.com/100752008/230778515-ee561877-b467-4706-b627-3374098f61b6.jpeg)


### 작동방식

> 플래그 정보

> FIN : 연결 해제. 세션 연결을 종료시킬 때 사용, 더 이상 전송할 데이터가 없음을 의미

#### No.1 [Client -> FIN -> Server]

Client는 연결을 종료하겠다는 `FIN` 플래그를 전송

#### No.2 [Server-> ACK -> Client]

Server가 `FIN`을 받고, 받았다는 신호인 `ACK`을 Client로 전송

#### No.3 [Server -> FIN -> Client]

Close준비가 다 된 후 Server는 Client에게 `FIN` 플래그를 전송

#### No.4 [Client -> ACK-> Server]

Client는 해지 준비가 되었다는 `ACK`을 Server로 보내준다

#### 요약

연결을 해제하려는 한쪽에서 FIN (Finish) 패킷을 보내면, 상대방은 ACK 패킷을 보내고, 자신도 FIN 패킷을 보내고, 상대방은 마지막으로 ACK 패킷을 보내서 연결을 해제합니다. 이렇게 4번의 통신으로 연결이 해제되기 때문에 4-way handshake라고 부른다.

#### Q&A

Q1. TCP의 연결 설정 과정(3단계) 연결 종료 과정(4단계) 차이나는 이유?

Client가 데이터 전송을 마쳤다고 하더라도 Server는 아직 보낼 데이터가 남아 있을 수 있기 때문에

일단 FIN에 대한 ACK만 보내고, 데이터를 모두 전송한 후에 자신도 FIN 메세지를 보내기 때문이다

