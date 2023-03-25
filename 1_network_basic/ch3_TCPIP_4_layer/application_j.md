# TCP/IP 4계층 (응용) - 준우

<br>

<img src="/assets/images/ch3/osi_tcp_ip.png">

OSI 7계층의 최상위 응용, 표현, 세션 계층은 인터넷 모델(TCP/IP 4계층)의 `응용(application) 계층`에 해당하며, 하위 계층인 전송 계층의 TCP/UDP프로토콜을 기반으로 한다.<br>
각기 다른 기기에서 동작하는 어플리케이션 사이에 통신이 가능하도록 한다. 각 기기가 서로 다른 OS, 프로그래밍 언어, 하드웨어를 사용하더라도 전송 계층의 프로토콜을 기반으로 통신이 가능하도록 한다.<br>
즉, 응용 계층의 프로토콜과 프로그램 및 서비스는 전송 계층을 기반으로 `어떻게 어플리케이션이 동작하게 할지 정의하는 것`이다.<br>

<br>

---

<br>



## UDP 프로토콜 기반

- DHCP(Dynamic Host Configuration Protocol):67 server, 68 client
- BOOTP(Bootstrap Protocol) :67 server, 68 client
    - 두 프로토콜은 IP를 할당할때 사용되며, DHCP는 동적으로 할당하며 BOOTP는 정적으로 할당한다.

- RTP(Real Time Protocol) :5004
    - 실시간으로 특정 파일을 전송할 때 사용되며, 스트리밍 오디오/비디오를 전달하기 위해 사용된다.

- SIP(Session Initation Protocol) : 5060, 5061
    - 전화나 멀티미디어 세션을 설정/수정/종료 할 수 있고, 방송 등에서 사용된다.

- DNS(Domain Name Service) :53
    - 호스트에 대한 이름/도메인에 대한 IP주소를 결정

<br>

---

<br>


## TCP 프로토콜 기반

- FTP (File Transfer Protocol) :20 데이터, 21 제어
    - 파일 전송을 위한 프로토콜

- POP (Post Office Protocol) :109 POP2, 110 POP3
    - 클라이언트가 메일 서버로부터 데이터를 받기 위해(검색) 사용되는 프로토콜

- SMTP (Simple Mail Transfer Protocol) :25
    - 메일 서버 간 데이터 전송을 위한 프로토콜

- IMAP (Internet Message Access Protocol) :993

- HTTP (Hypertext Transfer Protocol) :80
    - 서버/클라이언트 모델에 따라 데이터(하이퍼텍스트)를 송수신하는데에 사용되는 프로토콜

- HTTPS :443
    - HTTP에 데이터 암호화가 추가된 프로토콜

- Telnet :23
    - 인터넷/LAN을 통해 CLI기반으로 다른 컴퓨터와 통신하기 위한 프로토콜. 서버 뿐 만 아니라 라우터, 스위치 등의 네트워크 기기들에 대한 설정, 트러블슈팅, 유지관리를 위해 사용된다.

- SSH(Secure Shell) :22 
    - 원격 호스트에 접속하기 위해 사용되는 보안 프로토콜. Telnet의 보안 취약점을 보완하기 위해 소개되었다.

**Shell**: 명령어와 프로그램을 사용할 때 쓰이는 OS의 커널과 유저 사이의 인터페이스로, 사용자로부터 명령을 받아 해석하고 이를 실행한다. <br>
**PuTTY**: SSH, Telnet 등을 위한 클라이언트 프로그램으로, 윈도우에서 사용하기 위해 소개되었으나 다른 OS에서도 사용될 수 있도록 소개되었다.<br><br>

<br>

---

<br>

## SMTP, POP3, IMAP의 차이
`SMTP`는 이메일을 보내기 위해 사용되는 프로토콜로, 서버-서버 & 서버-클라이언트 모두 사용될 수 있고 텍스트를 기반으로 메시지가 전송된다. 7bit의 ASCII 기반으로 되어있으며, 8bit 이상의 첨부파일 같은 경우, MIME이라는 7bit기반 포맷으로 변환되어 전달된다.<br>
`POP3`는 원격 서버로부터 TCP 연결을 통해서 이메일을 가져오는데에 사용된다. POP은 원격 서버에서 이메일을 가져온 후, 해당 이메일을 서버에서 삭제한다.<br>
`IMAP`는 POP3와 달리 서버에서 메일을 가져오더라도 서버에 메일이 그대로 남아있다. 또한, 중앙 메일 서버에서 동기화가 이루어지기 때문에 모든 장치에서 동일한 이메일을 볼 수 있다. 반면, 서버 트래픽이 그만큼 많이 사용된다.<br><br>

### How these works? How we can utilize it on Application?

다음은 IMAP 기반으로 이메일의 inbox에 있는 모든 메일을 가져오며, 각 메일의 제목과 발송인을 출력하는 예시 코드이다.<br>

```Python
import imaplib

# Connect to IMAP server
imap_server = imaplib.IMAP4_SSL('imap.example.com')
imap_server.login('username', 'password')

# Select mailbox and search for messages
imap_server.select('inbox')
typ, data = imap_server.search(None, 'ALL')

# Loop through messages and print subject and sender
for num in data[0].split():
    typ, msg_data = imap_server.fetch(num, '(RFC822)')
    for response_part in msg_data:
        if isinstance(response_part, tuple):
            msg = email.message_from_bytes(response_part[1])
            subject = msg['subject']
            sender = msg['from']
            print('Subject: {}\nFrom: {}\n'.format(subject, sender))

# Logout from server
imap_server.close()
imap_server.logout()
```

<br><br>

다음은 SSH를 통해 AWS의 EC2에 접속하여 원격 제어하는 스크립트의 예시이다.<br>

```Shell
Kenneth 🚀   ~  ssh comeet-back

Last login: Sun Mar 26 00:23:37 2023 from 122.43.141.139

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/


[ec2-user@comeet-back ~]$ ls
app  appspec.yml  install

[ec2-user@comeet-back ~]$
```

<br>

- 참조
'SSH Secure Shell', 정보통신기술용어해설, http://www.ktword.co.kr/test/view/view.php?m_temp1=2524<br>
'SMTP POP3 IMAP이란?', https://sambalim.tistory.com/60<br>
'SSH 명칭부터 접속까지 한번에 이해하기', https://library.gabia.com/contents/infrahosting/9002/<br>
