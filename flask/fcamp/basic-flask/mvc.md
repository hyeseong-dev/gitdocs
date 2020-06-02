# MVC란

MVC란?

MVC는 디자인 패턴 중 하나

* Model: 데이터베이스와 연결되는 부분 
* View: 클라이언트가 보는 부분\(HTML, Javascipt code\) 
* Controller: 접근 URL에 따라 비즈니스 로직이 수행되는 부분

         

![mvc &#xAD6C;&#xC870;](../../../.gitbook/assets/image%20%28221%29.png)



@app.route\('/'\) 라우트 안쪽의 \(\)괄호안에 url주소를 썻어요. 이말은 url 주소와 연결된 코드를 실행했다는 말이에요. MVC에서 Controller로 넘어 왔다는 말이에요.   
좀더 어렵게 표현하자면 Business Logic을 실행했다는 말이에요.   
  
예를들어 https:fastcampus.co.kr로 접속했어요.  그럼 controller logic이 있을거에요.   
들어온 사람이 신규 접속자인지 이전에 접속했던 사람인지 확인하는 logic을 수행할 거에요.   
이 logic을 수행하는데에 Data가 필요할거에요.   
  
강의, 수강생, 광고등의 데이터가 DB에 있을텐데요.   
DB에 가져오는 역할이 Model이 하게되요. 그리고 Controller에 이 데이터를 다시 가공하고 끄집어내서 Controller에 전달해주게 되요. 

View 로직은 View대로 모아두고 Controller, Model 별로 모아두는데 이를 MVC 라고 하는거에요.   
큰 규모의 작업에 적합한 구조에요. 

































