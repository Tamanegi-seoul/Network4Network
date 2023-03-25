# 웹/인터넷의 표준은 누가, 언제, 어디서 정하나?


## What is W3C?
`World Wide Web Consortium(W3C, 웹 표준 국제 컨소시엄)`은 팀 버너스 리를 중심으로 웹의 표준을 개발하고 장려하는 조직이다. <br>
CSS, DOM, HTML, XML 등과 같은 웹과 관련된 기술의 표준을 선언했다.<br><br>


## What is ECMA International?
`European Computer Manufactures Associaion(ECMA)`는 정보와 통신을 위한 국제적 표준화 기구를 말한다.<br>
대표적으로 ECMAScript 를 정의하며, JSON형식 및 다양한 기술들에 대한 규격을 선언했다.<br><br>

## What is RFC?
`RFC`는 Request for Comments의 약자로, 인터넷을 개발하는데 필요로 되는 절차나 기술을 적어둔 문서를 뜻한다. `Internet Engineering Task Force(IETF, 국제 인터넷 표준화 기구)`에서 이러한 통신 기술에 대해 규약을 약속하며, 새로운 기술들은 RFC 버전별로 약속된 것들을 기반으로 개발되어오고 있다. <br><br>

'https://www.rfc-editor.org/rfc-index-100a.html'에서 각 문서들을 확인할 수 있다.<br><br>


## 포트번호는 누가, 어떻게 정해졌나?

이에 대한 실마리는 RFC를 통해 알 수 있다. `RFC2616`<br>

>  3.2.2 http URL

   The "http" scheme is used to locate network resources via the HTTP
   protocol. This section defines the scheme-specific syntax and
   semantics for http URLs.

   http_URL = "http:" "//" host [ ":" port ] [ abs_path [ "?" query ]]

   If the port is empty or not given, port 80 is assumed. The semantics
   are that the identified resource is located at the server listening
   for TCP connections on that port of that host, and the Request-URI
   for the resource is abs_path (section 5.1.2). The use of IP addresses
   in URLs SHOULD be avoided whenever possible (see RFC 1900 [24]). If
   the abs_path is not present in the URL, it MUST be given as "/" when
   used as a Request-URI for a resource (section 5.1.2). If a proxy
   receives a host name which is not a fully qualified domain name, it
   MAY add its domain to the host name it received. If a proxy receives
   a fully qualified domain name, the proxy MUST NOT change the host
   name.

처음엔 HTTP의 포트에 대한 약속이 없었지만, RFC 1060에서 79,81포트는 명시하였지만 80포트는 비워져있었다. 이후 W3C에서 HTTP 0.9를 소개하면서 HTTP를 위해 80포트를 기본적으로 사용하자고 언급했다. RFC 1340에서 80포트가 World Wide Web HTTP로 공식 지정되었다.<br><br>

이처럼, 과거에는 정해진 바가 없는 카오스의 환경에서 여러 기구와 단체의 노력으로 규범(standard, protocol)으로 굳혀져 현대의 기술들이 정의되었다. <br>

- 출처
'http의 기본 포트가 80, https의 기본 포트가 443인 이유는 무엇일까?', https://johngrib.github.io/wiki/why-http-80-https-443/<br>
'ECMA internatioanl', https://ko.wikipedia.org/wiki/Ecma_%EC%9D%B8%ED%84%B0%EB%82%B4%EC%85%94%EB%84%90<br>


