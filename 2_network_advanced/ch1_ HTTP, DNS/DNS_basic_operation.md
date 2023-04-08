## DNS (Domain Name System)란?
- 호스트의 도메인네임 (www.example.com)을 네트워크주소 (192.168.10)로 변환하거나, 그 반대의 역할을 수행하는 시스템이다. 
- 이 DNS를 운영하는 서버를 `네임서버`라고 한다. 
- DNS 서버는 사용자가 도메인 이름을 브라우저에 입력하면, 사용자를 어떤 서버에 연결할 것인지 제어한다. 이러한 요청을 쿼리라고 한다. 
<p><img src="https://ifh.cc/g/rL5cod.png" alt="img"></p>

1. 도메인 주소 naver.com을 브라우저에 입력하면, 도메인 주소들을 가지고 있는 <b>네임서버(DNS 서버)</b>에 접속한다.
2. 네임서버에 접속한 도메인 (naver.com)과 연결된 <b>IP정보(223.130.192.200)를 확인</b>하고, IP를 사용자 PC에 전달한다. 
3. 사용자 PC는 전달받은 서버의 IP주소로 접속한다.
4. 서버의 IP로 연결된 브라우저에 서버의 내용(홈페이지)을 출력한다. 

<p><img src="https://ifh.cc/g/86fjrP.png"></p>

1. 웹 브라우저에 www.naver.com을 입력하면 먼저 PC에 저장된 local DNS (기지국 DNS서버)에게 "www.naver.com"이라는 hostname에 대한 IP주소를 요청한다.
  1-1. local DNS에는 www.naver.com의 IP주소가 있을 수도 있고, 없을 수도 있다.  
  만일 전에 네이버에 접속했던 이력이 있다면, local DNS에 접속정보가 캐싱되어 있어 바로 pc에 ip주소를 주고 끝난다. (1번에서 바로 7번으로)
2. 요청받은 local DNS는 www.naver.com의 ip주소를 찾아내기 위해 다른 DNS서버들과 통신(DNS 쿼리)을 시작한다.
3. <b>Root DNS 서버</b> 에게 요청 -> ip주소 없음 -> local DNS 서버에게 ip를 찾을수 없다고 다른 DNS서버에게 물어보라고 응답.
4. <b>TLD DNS서버 (최상위 도메인 서버)</b>에게 요청
5. <b>Authoritative DNS서버</b>에게 요청
> Authoritative DNS sever?
> 실제 개인 도메인과 ip주소의 관계가 기록/ 저장/ 변경 되는 서버.
> 일반적으로 도메인/ 호스팅 업체의 `네임서버`를 말하지만, 개인이나 회사 DNS서버 구축을 한 경우에도 여기에 해당하게 된다. 
6. local DNS서버에 www.naver.com에 대한 ip주소를 전달.
7. 이를 수신한 local DNS는 www.naver.com의 ip주소를 캐싱하고 이후 다른 요청이 있을시 응답할 수 있도록 ip주소 정보를 단말(pc)에 전달해준다. 

### Root DNS 서버
- Root DNS는 최상위 DNS서버로 해당 DNS부터 시작해서 아래 딸린 node DNS 서버에게로 차례차례 물어보게 되는 구조로 짜여져 있다. 
<p><img src="https://ifh.cc/g/HW083t.png"></p>
- 모든 DNS 서버들은 이 Root DNS server의 주소를 기본적으로 가지고 있다. 

### TLD DNS 서버  (Top-Level Domain, 최상위 도메인 서버)
- 국가 코드 최상위 도메인(Country Code Top-Level Domain, ccTLD)
  - (ex, .kr, .jp, .CN, .US 등.....) 

- 일반 최상위 도메인(generic top-level domain, gTLD)
  - (ex, .com, .net, .org 등.....)

- 신규 일반 최상위 도메인, 국제화 일반 최상위 도메인 등
> 참고 : ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7_%EC%B5%9C%EC%83%81%EC%9C%84_%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%AA%A9%EB%A1%9D#%EA%B5%AD%EC%A0%9C%ED%99%94_%EC%9D%BC%EB%B0%98_%EC%B5%9C%EC%83%81%EC%9C%84_%EB%8F%84%EB%A9%94%EC%9D%B8

### Second-level DNS 서버 (2차 도메인)
위에서 Root DNS 서버에서 return해준 TLD 서버주소를 기지국 DNS 서버에서 받아서 다시 TLD 서버에 요청을 했었다.

그리고 TLD 서버에서는 Second-level DNS 서버를 return 해준다.

만일 naver.com 이나 google.com을 요청했다면, TLD 서버에서 .com을 파악하고 그 앞에 달린 문자열을 보고 네이버나 구글 서버에게 요청을 하는 것이다.

그렇게 요청 받은 Second DNS 서버는 자체적으로 sub 도메인 서버로 또 넘기게 된다.

### Sub DNS 서버 (최하위 서버)
서브 도메인 서버는 www. dev. mail. cafe. 등등 을 구분하는 최하위 서버를 말한다.

naver 서버라도 그 안에서 네이버 홈, 메일, 블로그, 카페 등 여러 서비스가 있다. 이 서비스들을 구분하는 도메인 네임이라고 보면 된다.

### DNS 문자열 구조
<p><img src="https://ifh.cc/g/1qztfF.png"></p>
모든 Computer들은 Root domain DNS server의 IP 주소는 알고있다.

그리고 Root domain을 담당하는 DNS 서버는 TLD(Top-level domain)을 담당하는 서버 목록과 IP를,
TLD(Top-level domain)을 담당하는 DNS 서버는 Second-level domain을 담당하는 서버 목록과 IP를,
Second-level domain을 담당하는 DNS 서버는 SUb domain을 담당하는 서버 목록과 IP를 알고 있는것이고,

결국, blog.example.com.의 IP주소는 Sub domain을 전담하고 있는 DNS 서버가 알고 있는 것이다.

1. Host가 Root에 IP를 물어봄
2. com으로 끝나니까, com을 전담하는 DNS server를 알려줌
3. example.com을 전담하는 DNS server를 알려줌
4. Sub domain DNS server를 알려줌
5. 해당 Domain에 대한 IP 주소를 Host에게 보냄 
6. IP 주소 get!