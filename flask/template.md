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

* url\_for\(\)함수는 나중에 

