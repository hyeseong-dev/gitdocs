# 부트스트랩 이용한 JinJa2 템플릿

#### 

### 간단한 네비게이션 바 만들기\(부트스트랩\)

* 이전 프로젝트를 복사하여 다음처럼 정리했다.

![](https://k.kakaocdn.net/dn/V6dp9/btqyV5uLgT9/QzQXkef5xJeMqQIfIvzIqK/img.png)![](https://k.kakaocdn.net/dn/5ZQa4/btqyUJZ6g1I/uYir9MkG7V9ImDFxxZ0kB0/img.png)

### 예제 04/templates/layout.html

```text
<!DOCTYPE html>
<html>
   <head>
       <title>03/04.html</title>
       <meta name="viewport" content="width=device=width, initial-scaile = 1.0">
       <link href = "http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel = "stylesheet" media="screen">
       <style type="text/css">
           .container{
               max-width : 500px;
               padding-top : 10px;
               padding-left : 10px;
               border:solid 5px black;
           }

           h3 {
               color:blue
           }
       </style>
   </head>

   <body>
   <nav class="navbar navbar-inverse" role="navigation">
       <div class = "container">
           <div class = "navbar-header">
               <a class="navbar-brand" href="/">Logo 영역</a>
           </div>
       </div>
   </nav>
       <div class="wrap">
           <h4> 기본 템플릿 시작 </h4>
           {% block content %} {% endblock %}
           <h4> 기본 템플릿 마침</h4>
       </div>
   </body>

</html>
<!--설명
6 : 부트스트랩 호출
22~28 : nav 태그로 상단바 영역을 지정한다. class명은 부트스트랩에서 지정하는 값을 똑같이 사용한다.
여기서 사용한 container, navbar, navbar-inverse, navbar-header, navbar-brand 모두 포함된다.

8 ~13, 23 : 원래 부트스트랩의 디자인이 적용되야하나, 8~13때문에 테두리등이 적용된다.
23 : container-fluid 로 대체하면 왼쪽 여백이 없다.
-->
```

### 예제 04/templates/children.html

```text
{% extends "layout.html" %}
{% block content %}
   <h4>자식 템플릿의 시작</h4>

   <p> 사용자 : {{userName}} </p>
   <p> 3번째 상품 : {{goodsList[2]}}  </p>
   <p> 전체 상품 목록</p>
   <ul>
       {% for goods in goodsList %}
       <li>{{goods}}</li>
       {% endfor %}
   </ul>

{% endblock %}
```

### 예제 04/01.py

```text
from flask import Flask, render_template

#앱 생성
app= Flask(__name__)

#라우트
@app.route('/')
def temp_test():
   return render_template('children.html',userName="반원",goodsList=['밤','호박','사과','배'])

if __name__=="__main__":
   app.run(debug=True)
```

### \(추가 예제\) - layout.html 수정

* 만일 layout.html에서 container 스타일을 주석처리하면 다음처럼 나온다.

![](https://k.kakaocdn.net/dn/R11Bm/btqyU8ZDQC2/xnVHn3GpaXea1O7Xhm1LvK/img.png)

```text
<!DOCTYPE html>
<html>
   <head>
       <title>03/04.html</title>
       <meta name="viewport" content="width=device=width, initial-scaile = 1.0">
       <link href = "http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel = "stylesheet" media="screen">
       <style type="text/css">
           <!--.container{-->
               <!--max-width : 500px;-->
               <!--padding-top : 10px;-->
               <!--padding-left : 10px;-->
               <!--border:solid 5px black;-->
           <!--}-->

           h3 {
               color:blue
           }
       </style>
   </head>

   <body>
   <nav class="navbar navbar-inverse" role="navigation">
       <div class = "container">
           <div class = "navbar-header">
               <a class="navbar-brand" href="/">Logo 영역</a>
           </div>
       </div>
   </nav>
       <div class="wrap">
           <h4> 기본 템플릿 시작 </h4>
           {% block content %} {% endblock %}
           <h4> 기본 템플릿 마침</h4>
       </div>
   </body>

</html>
<!--설명
6 : 부트스트랩 호출
22~28 : nav 태그로 상단바 영역을 지정한다. class명은 부트스트랩에서 지정하는 값을 똑같이 사용한다.
여기서 사용한 container, navbar, navbar-inverse, navbar-header, navbar-brand 모두 포함된다.

8 ~13, 23 : 원래 부트스트랩의 디자인이 적용되야하나, 8~13때문에 테두리등이 적용된다.
23 : container-fluid 로 대체하면 왼쪽 여백이 없다.
-->
```

### 추가 주석부분을 확인하며 부트스트랩 활용을 연습해보자.

![](https://k.kakaocdn.net/dn/buEElv/btqyU8egSQJ/EjHopmrONuNkDiZu6V8vk0/img.png)

```text

<!DOCTYPE html>
<html>
   <head>
       <title>03/04.html</title>
       <meta name="viewport" content="width=device=width, initial-scaile = 1.0">
       <link href = "http://netdna.bootstrapcdn.com/bootstrap/3.0.0/css/bootstrap.min.css" rel = "stylesheet" media="screen">
       <style type="text/css">
           <!--.container{-->
               <!--max-width : 500px;-->
               <!--padding-top : 10px;-->
               <!--padding-left : 10px;-->
               <!--border:solid 5px black;-->
           <!--}-->

           h3 {
               color:blue
           }
       </style>
   </head>

   <body>
   <nav class="navbar navbar-inverse" role="navigation">
       <div class = "container-fluid"> <!--수정-->
           <div class = "navbar-header">
               <a class="navbar-brand" href="/">Logo 영역</a>
           </div>
       </div>

       <!--추가-->
       <div class = "collapse navbar-collapse">
           <ul class = "nav navbar-nav">
               <li class="active"><a href="#">메뉴 1</a></li>
               <li><a href="#">메뉴 2</a></li>
               <li><a href="#">메뉴 3</a></li>
               <li><a href="#">메뉴 4</a></li>
           </ul>

           <form class = "navbar-form navbar-left" role="search">
               <div class="form-group">
                   <input type="text" class="form-control" placeholder="키워드 검색">
               </div>
               <button type="submit" class = "btn btn-default">검색</button>
           </form>

           <ul class="nav navbar-nav navbar-right">
               <li><a href="#">회원가입</a></li>
               <li class ="dropdown">
                   <a href="#" class="dropdown-toggle" data-toggle="dropdown">사용자<b class="caret"></b></a>
                   <ul class="dropdown-menu">
                       <li><a href="#">로그인</a></li>
                       <li><a href="#">고객센터</a></li>
                       <li class="divider"></li>
                       <li><a href="#">전원끄기</a></li>
                   </ul>
               </li>
           </ul>
       </div>


   </nav>
       <div class="wrap">
           <h4> 기본 템플릿 시작 </h4>
           {% block content %} {% endblock %}
           <h4> 기본 템플릿 마침</h4>
       </div>

       <!--추가-->
       <script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
       <script src="http://netdna.bootstrapcdn.com/bootstrap/3.0.0/js/bootstrap.min.js"></script>
   </body>

</html>
```

