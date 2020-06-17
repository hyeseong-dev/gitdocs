# Jinja2 Template 엔진

### 파이썬의 웹 프레임워크

1. Flask\(Micro Framework\)
   * 비슷한 예 : Bottle, 시나트라\(Sinatra, Ruby, 시초\)
   * 웹 프로그래밍에 있어서 가장 핵심적인 요소만을 포함하고 있다.
   * 자유도가 높다.
   * WSGI 구현체인 Werkzueg와 템플릿 JinJa2를 사용
2. Django\(Full Stack Framework\)
   * 비슷한 예: Web2py, Turbogear, Spring\(Java\), Rails\(Ruby\)
   * 웹 프로그래밍에 필요한 대부분의 것을 이미 갖추고 있다.
   * 인증권한, ORM, 템플릿 라이브러리, 국제화와 지역화, 관리자, 보안 등의 여러요소를 갖춤
   * 자유도가 떨어진다.

### JinJa2 템플릿 엔진 맛보기

* 플라스크 설치 시 자동으로 같이 설치된다.
* 플라스크의 템플릿 파일들은 /templates 폴더에 위치해야한다.

![](https://k.kakaocdn.net/dn/cgjTvF/btqyV6mNMAx/GApjNtmPtMyW351dS3KLR1/img.png)

### 예제 03/templates/a.html

```text
<html>
   <body>
       <h1>Hello,{{name}}</h1>
   </body>
</html>
```

### 예제 03/01.py

```text
from flask import Flask, render_template

app = Flask(__name__) #Flask 객체 인스턴스 생성

@app.route('/')
def main():
   return "<h1>Hello~!</h1>"

@app.route('/user/<userName>')
def user(userName):
   return render_template("a.html",name=userName)

if __name__=="__main__":
   app.run()
"""설명
1 : render_template()은 애플리케이션(프로그램)과 JinJa 템플릿 엔진을 통합하는 역할을 한다.

11 : 템플릿에 전달할 변수도 지정할 수 있다.
"""
```

### JinJa2 템플릿 표현식

* 템플릿은 기본적으로 그냥 보여지는 역할을 수행하는데, 프로그래밍적 연산 등이 필요한 경우에 아래 기호들이 쓰인다.

  | 표현 | 이름 | 의미 |
  | :--- | :--- | :--- |
  | {% | block start string | 프로그래밍 영역 시작 기호 |
  | %} | block end string | 프로그래밍 영역 끝 기호 |
  | {{ | variable start string | 변수 출력 시작 기호 |
  | }} | variable end string | 변수 출력 끝 기호 |
  | {\# | comment start string | 주석 시작 기호 |
  | }\# | comment end string | 주석 끝 기호 |

### 예제 03/02.py - JinJa 변수 출력

* 현재 html을 따로 안만들었기 때문에 Template 객체로 직접 html코드를 넣어주고 있다.
* 나중에는 Template에서 사용하는 {{ }} 등의 표현을 사용한 html파일을 만들면된다.

```text
from jinja2 import Template

template = Template("Hello {{userName}}")
result = template.render(userName="반원")

print(result)
print(type(result))

"""설명
3 : 템플릿 인스턴스를 하나 만든다. 그리고 userName변수를 출력할 자리 지정
4 : userName 값을 "반원"으로 넣어서 렌더링 한다.

6 : 마치 파이썬 format 함수처럼 작동한다.
7 : 타입을 확인하면 문자열이다.
"""
```

### 03/03.py - JinJa2 반복 표현

```text
from jinja2 import Template

template = Template("숫자 출력을 해봅니다 : {% for i in range(10) %} {{i}} {% endfor %} ")
result = template.render()

print(result)
print(type(result))
"""설명
3 : 템플릿 인스턴스를 하나 만든다.
3 : 반복문의 끝에는 endfor를 적어준다.
3 : 반복문은 프로그래밍 영역이므로 {% 와 %}를 사용한다.
3 : 변수 i는 반복문에서 사용한 i이다.
3 : {{i}} 앞뒤에 띄어쓰기나 \n, \t을 넣으면 출력도 변한다

4 : 딱히 매개변수로 넣을 것이 없다.
"""
```

![](https://k.kakaocdn.net/dn/wXFA4/btqyXxDwj5X/I8q9KG1JKLadEyE6ZTuX01/img.png)

### 03/templates/04.html - JinJa2 엔진 html 파일에 적용

```text
<!DOCTYPE html>
<html>
   <head>
       <title>03/04.html</title>
       <meta name="viewport" content="width=device=width, initial-scaile = 1.0">
       <style type="text/css">
           .container{
               max-width : 500px;
               padding-top : 10px;
               padding-left : 10px;
               border:solid 5px black;
           }
       </style>
   </head>

   <body>
       <div class="container">
           <p> 사용자 : {{userName}} </p>
           <p> 3번째 상품 : {{goodsList[2]}}  </p>
           <p> 전체 상품 목록</p>
           <ul>
               {% for goods in goodsList %}
               <li>{{goods}}</li>
               {% endfor %}
           </ul>
       </div>
   </body>

</html>
<!--
설명
5 : 뷰포트(viewport) : 사용자에게 보여지는 웹페이지 영역 속성.
주로 모바일 웹페이지 레이아웃 제어를 위해 meta 태그를 이용한다.
- width = device-width : 현재 기기의 너비로 페이지의 너비를 설정한다.
- initial-scale = 1.0 : 처음 페이지 로딩시 확대/축소 비율 설정이다.
                       원래 크기는 값 1이고, 값은 0~10까지 가능하다.
- minimum-scale : 줄일 수 있는 최소 크기 지정. 0~10. 0.5면 50% 축소.
- maximum-scale : 늘릴 수 있는 최대 크기 지정. 0~10. 2면 200% 확대.
- user-scalable : yes 또는 no 값. 화면 확대/축소 가능여부 지정.

6 : 웹 페이지에 적용될 스타일 정의 영역
-내부 선언(internal css) : HTML문서 내부에서 <head>와 </head>사이에 스타일을 정의하는 방법
<head> <style type="text/css"> 스타일 정의 </style> </head>

7 : 특정 class를 가진 요소의 스타일을 정의할 때 .클래스명을 적는다.
- max-width = 500px; 최대너비 500px
- padding-top = 10px; 내부 위쪽 여백 10px
- padding-left = 10px; 내부 왼쪽 여백 10px
- border = solid 5px black; 테두리 실선 5px 검정

-외부 선언(external css) : 외부 css파일을 불러오는 방법.
<link rel="stylesheet" type="text/css" href="style.css" />

19 : 인덱스를 사용하여 특정 value를 가져오도록 작성한다.

22~24 : 반복문을 이용하며, 하나하나씩 꺼내오는 goods를 <li>태그로 감싼다.
-->
```

### 03/04.py - templates폴더의 html

```text
from flask import Flask, render_template

#앱 생성
app= Flask(__name__)

#라우트
@app.route('/')
def temp_test():
   return render_template('04.html',userName="반원",goodsList=['밤','호박','사과','배'])

if __name__=="__main__":
   app.run()
"""설명
9 : 매개변수로 html 파일명과 그곳에 쓰일 변수들을 넣어 전달한다.
“""
```

### 템플릿 상속

* 기본\(base\)가 되는 html 을 가져와 적용시킬 수 있다.

```text
{% extends “<부모 템플릿의 이름>” %} 
{% block %} <대체할 코드> {% endblock %}
```

![](https://k.kakaocdn.net/dn/O5ttq/btqyV4Jkik8/pSaJvF5DAuaSlPLSFnMVgk/img.png)

### 예제 03/templates/05layout.html

```text

<!DOCTYPE html>
<html>
   <head>
       <title>03/04.html</title>
       <meta name="viewport" content="width=device=width, initial-scaile = 1.0">
       <style type="text/css">
           .container{
               max-width : 500px;
               padding-top : 10px;
               padding-left : 10px;
               border:solid 5px black;
           }

           h4 {
               color:blue
           }
       </style>
   </head>

   <body>
       <div class="wrap">
           <h4> 기본 템플릿 시작 </h4>
           {% block content %} {% endblock %}
           <h4> 기본 템플릿 마침</h4>
       </div>
   </body>

</html>
<!--설명
base(부모, parent)템플릿이 될 html이다. 틀 역할을 하며 여기저기 불려질 것이다.
block 과 endblock 부분은 이 05layout.html을 호출한 다른 템플릿(html)에서
설정한 대로 채워질 것이다.

23: block의 이름을 넣을 수 있다.
-->
```

### 03/templates/05chidren.html

```text
{% extends "05layout.html" %}
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
<!--
설명
1 : 부모 템플릿을 상속 받음. 부모 템플릿은 05layout.html
2 : block을 지정하며, 이 block의 이름은 content
3 ~ 13 : 대체할 코드를 넣는다.
14 : block 의 끝
-->
```

### 03/05.py

```text
from flask import Flask, render_template

#앱 생성
app= Flask(__name__)

#라우트
@app.route('/')
def temp_test():
   return render_template('05children.html',userName="반원",goodsList=['밤','호박','사과','배'])

if __name__=="__main__":
   app.run(debug=True)

"""설명
9 : 매개변수로 html 파일명과 그곳에 쓰일 변수들을 넣어 전달한다.
"""
```

기본 base인 05layout.html의 스타일이 자식격인 05children.html에 적용된다.

