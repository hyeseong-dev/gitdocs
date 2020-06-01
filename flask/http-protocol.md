# HTTP Protocol

###  Resource 

* resource : Web에서 쓰이는 모든 자원들\( 상품목록, 강좌, 이미지, 동영상등\) 
* 이런 resource를 client\(user\)가 워하는 request에 맞는 resource를 제공하는 형식을 갖추고 있음
* 위 자원들은 사전에 Web server에 저장되어서, 적합한 요청이 왔을 때 Web브라우저를 통해서 return\(보여줌\)해주게되는데, 이 부분이 바로 웹 브라우자가 이해 할 수 있는 html 형태 등을 이용해서 txt, image, video등을 사용자가 볼 수 있게 만들어 주게 되요. 

![](https://k.kakaocdn.net/dn/lAJjf/btqyV5aqzxl/F0vrIFZWEwufClkpGJ0iTk/img.png)



* 단순한 html파일, 동영상, 이미지 등은 정적\(static\) 파일이라고 할 수 있다. 정적이란 고정이나 변하지않음을 뜻하며, 이러한 정적 파일로 구성된 웹페이지는 클라이언트에게 uri를 통해 자원 위치만 확인해서 반환하면 된다.
* 그런데 다소 복잡한 웹 프로그램 경우는 클라이언트\(사용자\)가 보낸 요청에 따라서 데이터를 처리하는 과정이 필요하고 응답 과정도 정적 파일과 조금 다르다.

![](https://k.kakaocdn.net/dn/brC0vD/btqyYoM6ESc/ErKfwpsRm4adHZG9FZgZik/img.png)

* 경우에 따라서는 아래처럼 Database와 웹 프로그램간의 데이터 확인이 필요할 수도 있다.

![](https://k.kakaocdn.net/dn/bqwQyI/btqyU86dpTD/V3hIQbNt0h7cqeLyN1O3O0/img.png)

### HTTP 메세지

* 웹 브라우저가 웹 서버가 요청할 때의 메시지를 HTTP 메시지 라고 한다.
* HTTP\(HyperText Transfer Protocol, 하이퍼본문전송규약\)는 WWW 상\(웹상\)에서 정보를 주고받을 수 있는 프로토콜이다. 주로 HTML 문서를 주고받는 데에 쓰인다.
* 위 그림에서는 1, 4에서 주고 받는다.
* 정확하게는 1은 HTTP 요청\(request\) 메시지, 2는 HTTP 응답\(response\) 메시지라 하며 서로 조금 차이가 있다.

#### HTTP 메시지의 구조\(축약\)

* HTTP 메시지는 헤더\(Header\)와 바디\(Body\)부분으로 나누며 기본적으로 각각 담고있는 정보는 다음과 같다.
  * 헤더 : 요청측의 기본 정보와 현재 요청의 종류\(GET, POST, PUT, DELETE, OPTIONS 등\)
  * 바디 : 헤더에 담긴 요청에 필요한 데이터 본문\(예: 블로그 글쓰기 경우, 제목과 내용\)

#### HTTP 요청 메시지

* 첫행\(순차\) : 메서드\(GET, POST 등\), HTTP버전\(HTTP/1.1\), 호스트명
* 어떤 웹 브라우저?\(User\_Agent\), 처리가능한 언어\(ko\_KR, en-US 등\)/자원\(gzip 등\)

#### HTTP 응답 메시지

* 첫행\(순차\) : HTTP버전\(HTTP/1.1\), HTTP상태코드\(200:성공\), 상태코드에 대한 문자열\(OK\)
* 날짜, 서버 종류, 사용자정의 헤더\(X-로 시작하는 정보들\)

#### 요청 메시지와 응답 메시지 그림 설명

* HTTP 요청 메시지와 HTTP 응답 메시지 차이를 간단하게 아래에 표현하였으며, 각 정보들은 key : value 형태로 구성되있다.

![](https://k.kakaocdn.net/dn/ckzLVf/btqyXwEBW71/AIJEpnkXBJVbIkhq56kfM1/img.png)![](https://k.kakaocdn.net/dn/bhWmDi/btqyWWRnDai/4RXdTRbwY9vOBaMDGjUPN0/img.png)

* HTTP를 구경해보려면 크롬 개발자 도구에서 Network 탭을 사용해보자.
* 더 구체적인 내용은 [보러가기](http://withbundo.blogspot.com/2017/07/http-10-http.html)

![](https://k.kakaocdn.net/dn/bMxOHo/btqyWVx58gm/vnS9tYLi8INDLsCgLSOS41/img.png)

### 웹 서버와 웹 브라우저간의 콘텐츠 협상\(contents negotiation\)

* 전달내용에서는 제외
* 웹 서버와 웹 브라우저간 발생하는 요청에 대한 자원 반환 단계\(위 그림 4번\)에서는 콘텐츠 협상\(contents negotiation\)을 거친 후 웹 브라우저에 응답데이터를 반환한다.
* 이 단계는 “웹 브라우저가 무엇을 처리할 수 있는가?” 웹 서버와 협상하는 단계 [https://developer.mozilla.org/ko/docs/Web/HTTP/Content\_negotiation](https://developer.mozilla.org/ko/docs/Web/HTTP/Content_negotiation)
* 콘텐츠 협상은 총 3가지로 분류된다.
  1. 서버 기반의 협상
     * 웹 서버가 웹 브라우저에 보낼 반환할 데이터의 형태를 직접 결정
     * 웹 서버가 웹 브라우저에 대한 정보를 활용해야하므로 요청 당시에 웹 브라우저에 대한 기본정보를 HTTP 헤더에 넣어 웹 서버에 보낸다.
  2. 에이전트\(캐시서버\) 기반의 협상
     * 웹 서버가 응답할 데이터 처리 형태를 결정하기위해서 당시 요청보다 앞서 첫 번째 수신을 처리한 에이전트\(캐시서버\)를 참고하는 방법.
  3. 투명한 협상 : 1과 2를 혼합한 협상
* 위의 협상이 제대로 이루어지지않으면 웹 브라우저가 이해할 수 없는 데이터를 응답받거나, 응답 데이터 처리과정에서 문제가 발생할 수 있다.

### 협상에 필요한 HTTP 메시지 헤더

* 전달 내용에서는 제외
* Accept : 브라우저가 처리할 수 있거나 선호하는 데이터 형태. text/html; 등
* Accept-Language : 브라우저가 수용할 수 있거나 선호하는 응답결과의 언어
* Accept-Encoding : 브라우저가 수용할 수 있거나 선호하는 응답 인코딩 형태. zip 파일 등

### 파이썬을 위한 웹프로그램 통신 규약

![](https://k.kakaocdn.net/dn/7eJdL/btqyXwSaqtn/4PDKdWz8z7kDkq7dSQbknk/img.png)

* 웹 프로그램은 클라이언트\(사용자\)가 보낸 요청\(2번\)과 처리 결과\(3번\)을 웹 서버를 경유하여 주고 받는다. 이 때 웹 서버와 웹 프로그램간의 메시지를 주고받기위한 약속\(규칙\)을 정할 필요가 있었다.
* 이는 웹 서버와 웹 프로그램이 서로 종속성없이 독립적으로 수행 또는 개발되기 위해서였다.\(그렇지 않다면 한 쪽 구조나 코드가 바뀌면 다른 쪽도 바꿔야 하기 때문이다.\)
* 그래서 정한 규약을 **CGI 규약**이라고 한다.
* 파이썬은 cgi모듈이 존재해서 CGI 규약에 맞는 환경변수와 표준 입출력에 직접 액세스하도록 웹 프로그램을 개발할 수 있다. 또한 파이썬은 WSGI표준을 지켜놔서 웹 서버와 웹 프로그램간의 독립성을 구현해준다.\(WSGI 표준을 따른다면 웹 서버 종류와 상관없이 웹 프로그램이 동작된다.\)
* 우리가 사용하는 플라스크는 **벡자이그\(Werkzeug 독일어\) 기반으로 작성되며, 위에서 말한 WSGI 코어와 URL라우팅을 지원하고있다.**

공유하기글 요소  






