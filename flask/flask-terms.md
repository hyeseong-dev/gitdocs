# Flask Terms

##  용어 

### **1. render\_template\(\) :** 템플릿을 렌더링함.  여기서 템플릿은 = HTML이에요.  평상시 우리가 보는 웹페이지는 HTML 코드가 웹브라우저에 의해서! 렌더링 된 결과를 보는것이에요. 즉 이런 요청을 하느 함수그 render\_template\(\)입니다. 

### 2. redirect\(\) : 

현재 요청된 연결을 특정 주소로 재연결을 시켜요. 예를 들어 [http://localhost/a](http://localhost/a) 라는 요청에서 redirect\('b.html'\) 을 설정하면 [http://localhost/b](http://localhost/b) 로 접속이 되게 됩니다. 보통 /a 주소에서 데이터를 처리하는 과정만 거치고 결과를 b 에서 보여주거나 할때 응용되기도 합니다.

