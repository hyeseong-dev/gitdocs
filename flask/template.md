# Template

#### html 작성 

{% tabs %}
{% tab title="a.html" %}
```text
<html>
   <body>
       <ul>
           <ol>
               <li>텐서플로우 2.0</li>
               <li>자바</li>
               <li>파이썬</li>
           </ol>
       </ul>
   </body>
</html>
```
{% endtab %}
{% endtabs %}

#### HTML template render

template 디렉토릴를 만들어서 위의 a.html을 생성한 디렉토리로 이동 시켜주세요.   


{% code title="\#실습 파일 main.py " %}
```text
from flask import Flask, render_template

app = Flask(__name__) #Flask 객체 인스턴스 생성

@app.route('/')
def main():
   return render_template("a.html")

if __name__=="__main__":
   app.run()

```
{% endcode %}

첫째줄은 render\_template : Flask Term 카테고리 확인하세요.   
기본적으로 현재 프로그램 위치의 templates 폴더를 찾게되요. 

일곱번째줄은 html 파일을 요청에 응답 가능한 template로 반환하다. 

###  route에서 URI 함수란?

*  * Flask 클래스에는 test\_request\_context\(\)란 메소드가 있어요. 클라이언트가 서버에게 url접속\(즉, HTTP request\)을 테스트하는 용도로 쓰이고, 호출시에는 테스트할 수 있는 객체가 생성되요.
  * 위에서 생성된 객체를 url\_for\(\) 함수를 이용하여 요청 테스트를 해볼게요.
  * url\_for\(\) 함수는 현재는 가볍게 보세요. 

```text
from flask import Flask, url_for

app = Flask(__name__) #Flask 객체 인스턴스 생성


@app.route('/')
def hello():
   return "<h1>Hello World</h1>"

@app.route('/flask/')
def flask():
   return "<h3>Hello flask</h3>"

@app.route('/user/<userName>')
def get_userName(userName):
   return "Hello "+ userName

@app.route('/userid/<int:userId>')
def get_userId(userId):
   return "user ID : {}".format(userId)

if __name__=="__main__":
   with app.test_request_context():
       print(url_for('hello'))
       print(url_for('get_userName', userName = "park"))

```

