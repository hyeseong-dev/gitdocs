# Flask Terms

##  용어 

### **1. render\_template\(\) :**

템플릿을 렌더링함.   
여기서 템플릿은 = HTML이에요.   
평상시 우리가 보는 웹페이지는 HTML 코드가 웹브라우저에 의해서! 렌더링 된 결과를 보는것이에요. 즉 이런 요청을 하느 함수그 render\_template\(\)입니다. 

### 2. redirect\(\) : 

현재 요청된 연결을 특정 주소로 재연결을 시켜요. 예를 들어 [http://localhost/a](http://localhost/a) 라는 요청에서 redirect\('b.html'\) 을 설정하면 [http://localhost/b](http://localhost/b) 로 접속이 되게 됩니다. 보통 /a 주소에서 데이터를 처리하는 과정만 거치고 결과를 b 에서 보여주거나 할때 응용되기도 합니다.

### 3. URI V.s URL 차이 

 Uniform Resource Identifier \(URI\) consists of a string of characters used to identify or name a resource on the Internet  
[http://en.wikipedia.org/wiki/URI](http://en.wikipedia.org/wiki/URI)  
  
URI는 인터넷 상의 자원을 식별하기 위한 문자열의 구성쯤으로 해석 될 수 있겠다.  
  
[http://en.wikipedia.org/wiki/URL](http://en.wikipedia.org/wiki/URL)  
URI의 한 형태인 URL은 인터넷 상의 자원 위치를 나타낸다.  
  
URL는 URI의 한 형태로, 바꿔 말하면 URI는 URL을 포함 하는 개념이다.  
\(URI &gt; URL\)  
  
인터넷 상의 자원의 위치와 식별자.  
언듯 보면 같은 것을 의미하는 듯 하다.  
하지만 '자원의 위치'라는 것은 결국은 '하나의 파일 위치'를 나타내는 것임을 명심하자.  
  
[http://img0.gmodules.com/ig/images/korea/logo.gif](http://img0.gmodules.com/ig/images/korea/logo.gif)  
이와 같은 형식은 logo.gif라는 인터넷상의 자원 위치를 의미 한다.  
이는 URI이면서도 URL라고 말할 수 있다.  
  
다음은 어떠한가.  
[http://endic.naver.com/endic.nhn?docid=1232950](http://endic.naver.com/endic.nhn?docid=1232950)  
http://endic.naver.com/란 서버에 위치한 endic.nhn파일은 query string인 docid의 값에 따라 여러가지 결과를 나타낸다.  
  
여기서 URL은 endic.nhn의 위치를 표기한 http://endic.naver.com/endic.nhn 까지이다.  
내가 원하는 정보에 도달 하기위해서는 ?docid=1232950라는 식별자\(Identifier\)가 필요한 것이다.  
  
결국 위의 [http://endic.naver.com/endic.nhn?docid=1232950](http://endic.naver.com/endic.nhn?docid=1232950) 주소는 URI이긴 하지만 URL은 아니다.  
  
또다른 예를 들면,  
http://endic.naver.com/endic.nhn?docid=1232950  
http://endic.naver.com/endic.nhn?docid=1232690  
위 두 주소는 같은 URL이고 다른 URI라고 할 수 있다.  
\(이건 좀 억지긴 하지만 개념을 이해하기 바란다.\)  
  


