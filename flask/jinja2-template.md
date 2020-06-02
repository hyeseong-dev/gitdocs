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

### **JinJa2 템플릿 엔진 맛보기**

* flask 설치 시 자동으로 같이 설치된다.
* flask 템플릿 파일들은 /templates 폴더에 위치해야한다.



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
   app.run(debug=True)
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

