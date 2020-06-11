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
첫 번째줄, 우선 flask의 Blueprint를 임포트 할게요.   
세 번째줄, Bluepirnt 클래스에 매개변수을\(api로 넣고 \_\_name\_\_ 역시 넣어 줄게요. api라는 인스턴스를 만들어 줄게요.   
  
그리고 api\_v1의 디렉토리에서\( . \) user 파일을 임포트해줄게요. 나중에게 가져올때 편리하게 구성한거에요.   


#### \_\_init\_\_.py

{% tabs %}
{% tab title="api\_v1/\_\_init\_\_.py" %}
```text
from flask import Blueprint

api = Blueprint('api', __name__) 
```
{% endtab %}
{% endtabs %}

####  user.py 

아래 코드 첫 번째줄은 현재 디렉토리의 api라는 녀석을 가져오는건데요. api라는 파일은 디렉토리 경로에서는 보이지 않을거에요. 하지만 \_\_init\_\_.py 파일 안에 Blueprint 클래스로 만든 api라는 객체가 보일거에요. 그걸 끌어다써서 임포트 한다는 말이에요.   
**즉, \_\_init\_\_.py의 api 객체 가져온거임**  


3째줄에 api.route\(\)데코레이터 보이조? 기존 메인 디렉토리 \("회원관리api생성/app.py" 파일 안에 있는 녀석들 다수와 비슷하조?   
그때는 app.route\(\) 였고 바로 아래 코드는 api.route\(\)에요.   
차이점은 app.route\(\)로 접근하냐 api로 접근하냐는 차이가 존재해요.   
  
계속해서, @api.route\('/test'\)로 만들거에요.  
그리고 바로 아래에 메서드를 만들거에요. 명칭은 route\('/?'\) 안의 매개변수 ?와 동일하게 매서드 이름을 만들어 주세요.   
여기서 return 하게 될때 html을 반환하는것이 아닌 data를 반환하게 되요.   
  
그리고 그 data는 json형태에요. 그래서 json 형태로 반환 할 수 있도록   


{% tabs %}
{% tab title="user.py" %}
```text
from . import api

@api.route('/test')
def test():
    return 
```
{% endtab %}
{% endtabs %}



그리고 그 data는 json형태에요. 그래서 json 형태로 반환 할 수 있도록   
아래 소스코드 첫번째 줄에서 flask 라이브러리의 jsonify를 가져와요.   
jsonify를 통해서 적용될 리스트, 딕셔너리 자료형을 써주면 json으로 그대로 변환해주게 되요.   
  
우선 아무것도 쓰지 않을게요. 그리고 기본 뼈대는 다 만들었어요. 

{% tabs %}
{% tab title="user.py" %}
```text
from flask import jsonify
from . import api

@api.route('/test')
def test():
    return jsonify({})
```
{% endtab %}
{% endtabs %}

#### 다시 한번 리뷰하면 

api\_v1이라는 폴더를 만들었으며 \_\_init\_\_파일에 api라는 Blueprint를 만들었으며 그리고 bluepirnt를 사용해서 user.py 파일에 view코드를 만들었어요.

{% tabs %}
{% tab title="api\_v1폴더 구조" %}
```text
회원관리api생성(폴더)
                   api_v1  1) __init__.py
                           2) user.py
```
{% endtab %}
{% endtabs %}

이후 아래 app.py파일에서는 이 blueprint 사용을 적어줘야 해요. 다른 말로는 등록한다고 하겠조?  
5번째 줄처럼 작성하고요. 3째불에 api\_v1모듈을 from에 넣어주고요. 그리고 \_\_init\_\_.py에서 정의한 api 객체를 import해주면 되요.   
as를 붙이고 이름을 다시 api\_v1이라고 바꿀게요.\(바로 직관적으로 파악하기 위함\)  
  
다시 6번째 줄의 app.register\_blueprint\(api\_v1, url\_prefix\)의 매개변수 두개를 넣을거에요. api\_v1 녀석을 첫번째로 넣고 다음 url\_prefix를 둘거고요.   
여기서 api\_v1이 의미하는 것은 api\_v1이 제공하는 view코드들 \(api.route\('?'\) 여러 코드들을 말해요.\) 다른 말로는 컨트롤러 코드들은  
아래와 같이 사용자에게 api.route의 매개변수 /test처럼 **URI**를 제공할 것이지

> from . import api  
>   
> @api.route\('/test'\)  
> def test\(\):  
>     return jsonify\(\)

실제 내부적으로는 **url\_prefix='/api/v1'**과 같이 작성되어 진거에요. 



{% tabs %}
{% tab title="app.py" %}
```text
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

