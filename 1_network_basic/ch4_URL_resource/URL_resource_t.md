# URL과 리소스 - 태이
<img src="https://ifh.cc/g/6rlhdj.jpg" alt="uri이미지">

<b>URI</b> (Uniform Resource Identifier)는 하나의 리소스를 가리키는 문자열입니다. 가장 흔한 URI는 URL로, 웹 상에서의 위치로 리소스를 식별합니다.

### URL이란?
- 인터넷의 리소스를 가리키는 표준
- 리소스뿐만 아니라 인터넷에서 리소스에 도달하는 방법을 지정하는 URI유형

> 모든 <b>URL</b>은 <b>URI</b>이지만, 모든 <b>URI</b>가 <b>URL</b>은 아닙니다. 

1. URL의 구조
대부분의 URL은 다음과 같은 구조를 갖는다. 
<p align="center"><img src="https://ifh.cc/g/7h52F7.png"></p>

- <b> 스킴 또는 프로토콜</b>
   - 상호 작용하는 데 사용하는 프로토콜
  - HTTP에 해당한다. 리소스에 대해 어떻게 접근할지 알려준다.
  - HTTP 프로토콜이 아닌 다른 가용한 프로토콜을 사용할 수 있다. mailto는 이메일 주소를 가르키며, ftp는 서버에 올라가 있는 파일을 가르킨다.

- <b>서버 위치 (host)</b>
  - 리소스가 어디에 호스팅 되어 있는지 확인한다.
  - port: 리소스를 호스팅하는 서버가 열어놓은 포트번호. 많은 스킴이 기본 포트를 가지고 있다. 
  - 웹 서버가 HTTP프로토콜의 표준포트를 사용하여 리소스에 접근하는 경우엔 일반적으로 포트가 생략된다. (HTTP의 경우 80, HTTPS의 경우 443을 사용)
- <b>경로</b>
  - 웹 서버의 리소스 경로
  - 서버 위치로 이동해서 로컬 리소스 중 어떤 자원을 요청할지에 대해 명시한다.

- <b>쿼리 파라미터</b>
  - 사용자가 입력 데이터를 전달하는 방법 중의 하나 
  - 웹 개발에서 데이터를 요청하는 방식 중 대표적인 것이 GET방식과 POST방식인데, 주로 GET방식으로 데이터를 요청할 때 쓰이는 방법.
  - URL에서 ?다음에 오는 내용
  - key=value 형식으로 구성되어 있고, 여러개를 사용할 때 '&'을 붙여 사용한다. 

#### Query String에서 문자열을 가지고 오는 방법 

<b>방법 1. URL </b>
가장 기본적인 방법으로 new 키워드를 사용하여 URL객체 생성 후 searchParams 프로퍼티로 QueryString만 가져옵니다. 그 다음 get()메서드로 원하는 값을 가져옵니다. 
```javascript
  
const urlObject = new URL(`https://search.naver.com/search.naver?sm=tab_hty.top&where=nexearch&query=맛집&oquery=맛집&tqi=hz19wlprvxZsscqdQmRssssst04-255238`);

const queryString = urlObject.searchParams;

console.log(queryString.get('sm'));     // tab_hty.top
console.log(queryString.get('where'));  // nexearch
console.log(queryString.get('query'));  // 맛집
console.log(queryString.get('oquery')); // 맛집

```

<b>방법 2. URLSearchParams </b>

new 키워드를 사용하여 URLSearchParams 객체 생성 후 get() 메서드로 원하는 값을 가져 옵니다. 

```javascript
  
const urlSearchParamsObject = new URLSearchParams('https://search.naver.com/search.naver?sm=tab_hty.top&where=nexearch&query=맛집&oquery=맛집&tqi=hz19wlprvxZsscqdQmRssssst04-255238');

console.log(urlSearchParamsObject.get('where'));  // nexearch
console.log(urlSearchParamsObject.get('query'));  // 맛집
console.log(urlSearchParamsObject.get('oquery')); // 맛집

```
URL이 너무 길다면, Query String만 new URLSearchParams()에 전달할 수 있습니다. 
또한, URL에 존재하는 모든 Query String을 가져오고 싶다면, URLSearchParams에서 제공하는 keys() 메서드를 사용하여 모든 키를 추출한 뒤 반복문으로 해당 키에 해당하는 값을 가져올 수 있습니다. 

```javascript
const urlSearchParamsObject = new URLSearchParams('sm=tab_hty.top&where=nexearch&query=맛집&oquery=맛집&tqi=hz19wlprvxZsscqdQmRssssst04-255238');

for (const key of urlSearchParamsObject.keys()) {
  console.log(urlSearchParamsObject.get(key));
}
```
[실행결과]
<img src="https://ifh.cc/g/nGKDPN.png">


  >출처 : https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/Identifying_resources_on_the_Web#uriuniform_resource_identifier_%EA%B5%AC%EB%AC%B8
