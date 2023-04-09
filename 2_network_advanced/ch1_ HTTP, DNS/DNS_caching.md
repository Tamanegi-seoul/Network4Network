# 캐싱을 통한 DNS 성능 향상

인터넷 주소: 의미있는 문자열로 IP주소를 추상화!<br><br>
`DNS서버`가 해당 치환과정을 처리해준다.<br>
매번 DNS서버에 IP주소를 요청하는 것은 굉장히 낭비적인 작업이다. 따라서 이를 극복하기 위해, 임시 저장소 `cache`를 사용하게 된다. 캐싱은 CS의 거의 모든 분야에서 사용되는 기술을 뜻한다. 빈번히 사용되는 것들을 저장해서 작업효율을 증대시키는 것이다.<br>


## DNS 계층 구조

<img src="/assets/images/ch1/DNS-hierachy.png">

- 1단계 도메인
    kr, com과 같이 등록인의 목적에 따라 사용되는 일반 도메인(generic Top Level Domain)

- 2단계 도메인
    co, go, ac와 같은 조직의 속성을 구분하는 서브 도메인
- 3단계 도메인
    조직이나 서비스의 이름을 나타내는 도메인.
- 호스트(Host)
    www과 같이 해당 서비스의 호스트를 나타내는 도메인.


## DNS 서버

- 로컬 DNS 서버 by ISP(KT,SKT,U+)
- Root NS
    국제인터넷주소관리기구(ICANN)에서 관리
- Top-level DNS (TLD)
    도메인 등록 기관(Registry) 
- Sub Domain NS
    가비아, AWS's Route53같은 도메인 판매 업체(Registar)


## 도메인 네임 캐싱

<img src="/assets/images/ch1/DNS-overview.png">


1. 로컬의 브라우저
    클라이언트에서 다른 서버에 대한 매핑 정보를 보관하고 직접 사용하여 주소 해석 속도 향상<br>
    단, 잘못된 도메인에 대한 요청을 캐싱해서 불필요한 트래픽과 지연을 줄이는 네거티브 캐싱을 사용<br>
2. OS의 hosts파일(/etc/hosts)
    도메인/호스트명과 IP주소에 대한 매핑정보를 저장하며, 리눅스와 맥 기준으로 etc/hosts에 저장된다.
3. 공유기(router)
    라우터에 따라 DNS 캐싱을 지원하는 경우가 있다.
4. ISP




## 캐싱 되어있는 DNS정보 직접 확인해보자

### 브라우저
- 크롬
    - 주소창에 `chrome://net-internals/#dns`를 입력

- MS Edge
    - 주소창에 `edge://net-internals/#dns`를 입력

- Safari
    - 사파리의 develop - Show Web Inspector - Storage - Caches - Images

<br>

### Windows
- Command Prompt를 관리자 권한으로 실행
- ipconfig/displaydns 명령을 실행
- DNS 정보를 확인

<br>


### Linux
- Terminal에 sudo systemd-resolve --statistics
- DNS 캐싱 통계와 기록 확인.

<br>


### MacOS
- Terminal에 dscacheutil -cachedump -entries dns 캐싱정보 확인 가능

<br>


### 내 컴퓨터의 DNS서버는?
본인은 MacOS를 사용하고 있으며, 집에서 공유기로 확인해보았다.<br>
Mac기준으로, Network-Advanced-DNS에서 관련 정보를 확인할 수 있었다.<br>

<img src="/assets/images/ch1/macos-wifi-dns.png">

위의 정보에서 `111.118.0.1`이 등록되어 있는 것을 확인할 수 있다.<br>
😮무슨의미..? 난 등록한적이 없다.<br><br>

앞서 ISP에서 DNS서버를 운영한다고 소개했다.<br>
통신사별로 DNS서버의 주소가 다르며, 위의 주소는 HNS의 DNS서버 주소이다.<br>
즉, 우리집에서 공유기를 통해 접속하게 되면 기본 DNS서버로 HNS의 DNS가 등록되어 있는 것이다.<br>


### DNS 요청 확인하기
`dig [@nameserver] 도메인` bash command를 통해 DNS 정보를 확인할 수 있다.<br>

<img src="/assets/images/ch1/dns-search-google.png">

<br>

<img src="/assets/images/ch1/dns-search-holaworld.png">


## 그래서, DNS 캐싱을 통해 얼마나 성능이 향상되나?
실제 생활수준에서 체감할정도로 DNS성능 향상을 기대하기 어렵다.<br>
새로운 사이트에 접속하기 위해 ISP에 DNS질의 하는데에 0.01~3초(10ms)가 걸린다고 한다.<br>
하지만 대부분의 사용자는 완전 새로운 사이트에 접속하는 일이 잘 없으며, 해당 지역에서 자주 사용되는 사이트는 이미 ISP 등에 등록되어있다.<br>



- "How much faster could running a local DNS server make my internet?", Quora, https://www.quora.com/How-much-faster-could-running-a-local-DNS-server-make-my-internet
- "[10분 테코톡]엘리의 DNS", 우아한테크, https://www.youtube.com/watch?v=sDXcLyrn6gU
- "IP주소 목록", IPSHU, https://ko.ipshu.com/ip_d_list/111.118.0
- "통신사별 DNS 주소", JJangFree, https://jjangfree.tistory.com/2223
- "DNS란?", 피망IT, https://peemangit.tistory.com/52
- "쉽게 이해하는 네트워크", Sam 3, https://better-together.tistory.com/128
