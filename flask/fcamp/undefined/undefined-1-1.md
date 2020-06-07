# 컨트롤러만들기-회원

이제는 회원과 관련된 모델,템플릿, 뷰가  준비 되었기 때문에 컨트롤러를 직접 개발해서 회원 가입 기능을 완성할게요.   


{% tabs %}
{% tab title="app.py" %}
```text
import os
from flask import Flask
from flask import render_template
from models import db

app = Flask(__name__)

@app.route('/register')
def register():
    # 이곳에 먼저 비즈니스 로직이 만들어짐.
    return render_template('register.html')

@app.route('/')
def hello():
    return render_template('hello.html')

    
if __name__=='__main__':
    basedir = os.path.abspath(os.path.dirname(__file__))
    dbfile = os.path.join(basedir, 'db.sqlite')
    
    app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
    app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
    app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
    
    db.init_app(app)
    db.app = app
    db.create_all()
    app.run(host='127.0.0.1', port = 5000, debug=True)
    
    @app.route('/register')
```

@app.route\('/register'\)   
def register\(\):  
 비즈니스 로직이 이 부분부터 삽입되요. 
{% endtab %}
{% endtabs %}



회원 가입의 경우 get, post 요청 두 가지가 존재해요.

* get요청의 경우 - 페이지만 나오게됨 
* post요청의 경우 - 회원가입 화면에서 등록 버튼을 누르게 되면 데이터를 가져오는 요청이에요.   


  ```text
  import os
  from flask import request
  생략 

  @app.route('/register')
  def register():        # 이함수에서 비즈니스 로직이 만들어짐.
      print(request.method)
      return render_template('register.html')

  ```

  
  def register\(\): 함수에서 어떤 요청이 들어왔는지 확인하기 위해서,  그리고 데이터를 가져오기 위해서 request라는 object를 사용해야해요.   
  object 객체를 요하기 위해 2번째 줄에 flask패키지에서 가져와서 import하게 됩니다.   
  
  즉, request를 사용해서 요청 정보를 다 확인 할 수 있어요.   
  하지만 위 7번째 줄을 작성하고 print\(request.method\) 요청하면 Error가 발생할거에요.   
  이유는 기본적으로  @app.route\('/register'\) 주소를 썻는데, 이 주소에 대한 허용하고자하는 메소드가 get밖에 되지 않아요.  
  
  그리고 만약 이 상태에서 "등록"버튼을 누르게 되면 

> **Method Not Allowed**  
> The method is not allowed for the requested URL.

라는 오류가 뜨게되요. 

 그래서 추가적인 작업을 해야해요.  
  
또한 요청이 루트로 갔어요. 

{% tabs %}
{% tab title="register.html 수정 전" %}
```text
<html>
    <head>

생략
            <form method="POST" action=".">
               <div class="form-group">
생략
    </body>
</html>
```
{% endtab %}

{% tab title="register.html 수정 후" %}
```
<html>
    <head>

생략
    
            <form method="POST" > # 기존 action='.' 삭제
               <div class="form-group">
생략
    
    </body>
</html>
```
{% endtab %}
{% endtabs %}

  
이제 결국 post를 활성화 시켜줘야해요.   
아래 5번째 줄에서 route\(\)안에 method인자값을 만들어서 'GET', 'POST'값을 넣어줍니다.  
이렇게 되면 두 가지 방식이 허용되요. 

```text
import os
from flask import request
생략 

@app.route('/register', methods=['GET', 'POST'] ) # 인자값생성
def register():        
    print(request.method)
    return render_template('register.html')

```

