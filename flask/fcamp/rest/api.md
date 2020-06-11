# 회원 생성 API 만들기

## 시작하기 앞서

준비 되어야 할 코드입니다. 



```text
# 회원관리api생성/app.py

from flask import Flask
from flask import render_template


app = Flask(__name__)


@app.route('/register')
def register():
  return render_template('register.html')

@app.route('/')
def hello():
  return 'hello world'

if __name__=='__main__':
    app.run(host='127.0.0.1', port=5000, debug=True)
```

  
api만 개발해서 웹사이트에 제공하지 않을거고요. render\_template처럼  
사용자에 대한 요청으로 html코드를 전달하는 uri도 있으며 api로 리소스만 전달하는 uri도 만들거에요.   
이 두가지를 구분하여 만들거에요. 

#### 요약 

1. 사용자에 대한 요청으로 html코드를 전달하는 uri
2. api로 리소스만 전달하는 uri 

사실 7번째 줄에서 쓰여진 @app.route\('/api/v1'\)처럼 만들수 있지만 이렇게 하면 한 파일에 모든 코드가 들어가기 때문에 코드의 가독성과 코드 효율성이 떨어짐으로 모듈화를 할거에요.  


```text
#회원관리api생성/app.py
from flask import Flask
from flask import render_template

app = Flask(__name__)

@app.route('/api/v1')

@app.route('/register')
def register():
  return render_template('register.html')

@app.route('/')
def hello():
  return 'hello world'

if __name__=='__main__':
    app.run(host='127.0.0.1', port=5000, debug=True)
```

그래서 flask에서 제공하는 blueprint를 이용해서 이 view코드도  분리하도록 할게요.  
그러기 위해선 폴더를 만들거에요. 위치는 "회원관리api생성" 폴더 바로 아래에 "api\_v1"이라는 폴더를 만들어 주세요. 

{% tabs %}
{% tab title="api\_v1폴더 구조" %}
```text
회원관리api생성(폴더)
                   api_v1(폴더)   1) __init__.py
                                  2) user.py
```
{% endtab %}
{% endtabs %}

> 참고로 실제 프로젝트에서는 버전업이 많이 발생해요.   
> 서비스들이 제공하는 api를 많이 사용해봐도 여러가지가 있고 새로운 버전이 나온다고 해서 이전 버전을 지우진 않아요.   
>   
> 즉, 버전별로 코드를 분리해서 관리하는 것이 중요해요.  
> 그래서 굳이 v1이라는 명칭을 말미에 붙였어요.

 user.py는 사용자와 관련한 api에요.   
그리고 우선 \_\_init\_\_.py  코드를 아래와 같이 작성해 볼게요.   
우선 flask의 Blueprint를 임포트 할게요. 

{% tabs %}
{% tab title="api\_v1/\_\_init\_\_.py" %}
```text
from flask import Blueprint

api = Blueprint('api', __name__) 
```
{% endtab %}
{% endtabs %}







{% tabs %}
{% tab title="app.py" %}
```text
# 회원관리api생성/app.py

from flask import Flask
from flask import render_template
from api_v1 import api as api_v1

app = Flask(__name__)
app.register_blueprint(api_v1, url_prefix='/api/v1')

@app.route('/register')
def register():
  return render_template('register.html')

@app.route('/')
def hello():
  return 'hello world'

if __name__=='__main__':
    app.run(host='127.0.0.1', port=5000, debug=True)
```
{% endtab %}

{% tab title="models.py" %}
```
# 회원관리api생성/models.py

from flask_sqlalchemy import SQLAlchemy 

db = SQLAlchemy()

class Fcuser(db.Model):
  __tablename__ = 'fcuser'
  id = db.Column(db.Integer, primary_key=True)
  password = db.Column(db.String(64))
  userid = db.Column(db.String(32))
  username = db.Column(db.String(8))
```
{% endtab %}

{% tab title="register.html" %}
```
회원관리api생성/register/register.html
<html> 
  <head>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
  </head>
  <body>
    <div class="container">
      <div class="row mt-5">
        <h1>회원가입</h1>
      </div>
      <div class="row mt-5">
        <div class="col-12">
          <form method="POST">
              <div class="form-group">
               <label for="userid">아이디</label>
               <input type="userid" class="form-control" id="userid" placeholder="아이디" name="userid" />
              </div>

              <div class="form-group">
               <label for="username">사용자 이름</label>
               <input type="text" class="form-control" id="username" placeholder="사용자 이름" name="username" />
              </div>

              <div class="form-group">
               <label for="password">비밀번호</label>
               <input type="password" class="form-control" id="password" placeholder="비밀번호" name="password" />
              </div>

              <div class="form-group">
               <label for="re-password">비밀번호 확인</label>
               <input type="password" class="form-control" id="re-password" placeholder="비밀번호확인" name="re-password" />
              </div>

             <button type="submit" class="btn btn-primary">등록</button>
          </form>
        </div>
      </div>
    </div>
  </body>

</html>
```
{% endtab %}

{% tab title="\_\_init\_\_.py" %}
```
# 회원관리api생성/api_v1/__init__.py

from flask import Blueprint


api = Blueprint('api', __name__)

from . import user
```
{% endtab %}

{% tab title="user.py" %}
```
# 회원관리api생성/api_v1/user.py

from flask import Blueprint


api = Blueprint('api', __name__)

from . import user
```
{% endtab %}
{% endtabs %}

