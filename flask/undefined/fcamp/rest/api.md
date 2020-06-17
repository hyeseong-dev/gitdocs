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

## API 구조 맛보기 

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
  return jsonify()
 
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

{% tab title="\_\_init\_\_.py" %}
from flask import Blueprint

api = Blueprint\('api', **name**\)

from . import api
{% endtab %}

{% tab title="models.py" %}
from flask\_sqlalchemy import SQLAlchemy

db = SQLAlchemy\(\)

class Fcuser\(db.Model\):   
\_\_**tablename\_\_** = 'fcuser'  
id = db.Column\(db.Integer, primary\_key=True\)   
password = db.Column\(db.String\(64\)\)   
userid = db.Column\(db.String\(32\)\)   
username = db.Column\(db.String\(8\)\)
{% endtab %}

{% tab title="user.py" %}
from flask import jsonify from . import user

@api.route\('/test'\)   
def test\(\):  
  return jsonify\(\),404
{% endtab %}
{% endtabs %}

위 소스 코드를 한번 실행해 볼게요.  그럼 아래와 같이 빈 딕셔너리가 나오는걸 확인할 수 있어요. 

![](../../../../.gitbook/assets/image%20%28237%29.png)

또 404 오류코드를 임의로 입력하여 확인 하는 방법은,  return jsonify\(\), 404 부분을 만드는 거에요.   
기존 jsonify\(\)부분 뒤에 , \(콤마\)를 입력하고 404 오류코드를 입력하면 되요.  
그리고 웹브라우저에서 아래와 같이 확인할건데요.   
웹 주소는 동일하게 입력하시고, 이후 F12키를 누르고 Network항목란에 가서 Ctrl + G를 누르면 나타날거에요.

 

![](../../../../.gitbook/assets/image%20%28235%29.png)



## 회원가입 API 생성 

이제 본격적으로 회원가입 API를 만들어 볼게요.  내부 동작은 기존\(회원가입 register.html\)의 코드들과과 동일해요. 기존에 만들었던 html코드들을 끌어 올게요.   
이미 언급되었다 싶이피 API는 리소스 중심이에요.



{% tabs %}
{% tab title="기존 register.html" %}
```text
<html>
    <head>
      <meta charset="utf-8" />
      <meta name='viewport' content='width=device-width, initial-scale=1, shrink-to-fit=no' />
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
                 <!-- <label for="userid">아이디</label>
                 <input type="userid" class="form-control" id="userid" placeholder="아이디" name="userid" /> -->
                {{ form.userid.label("아이디")}}
                {{ form.userid(class="form-control", placeholder="아이디") }}
               </div>
               <div class="form-group">
                 <!-- <label for="username">사용자 이름</label>
                 <input type="text" class="form-control" id="username" placeholder="사용자 이름" name="username" /> -->
                 {{ form.userid.label("사용자 이름")}}
                 {{ form.userid(class="form-control", placeholder="사용자 이름") }}  
                </div>
               <div class="form-group">
                 <!-- <label for="password">비밀번호</label>
                 <input type="password" class="form-control" id="password" placeholder="비밀번호" name="password" /> -->
                 {{ form.userid.label("비밀번호")}}
                 {{ form.userid(class="form-control", placeholder="비밀번호") }} 
                </div>
               <div class="form-group">
                 <!-- <label for="re-password">비밀번호 확인</label>
                 <input type="password" class="form-control" id="re-password" placeholder="비밀번호확인" name="re-password" /> -->
                 {{ form.userid.label("비밀번호 확인")}}
                 {{ form.userid(class="form-control", placeholder="비밀번호 확인") }} 
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

{% tab title="기존 app.py" %}
```
import os
from flask import Flask
from flask import request 
from flask import redirect
from flask import render_template
from models import db
from flask_wtf.csrf import CSRFProtect

from models import Fcuser

app = Flask(__name__)

@app.route('/register', methods=['GET', 'POST'])
def register():
    if request.method == 'POST':                       
        userid = request.form.get('userid')
        username = request.form.get('username')
        password = request.form.get('password')
        re_password = request.form.get('re-password')

        if (userid and username and password and re_password) and password == re_password :
          fcuser = Fcuser()
          fcuser.userid = userid
          fcuser.username = username
          fcuser.password = password
  
          db.session.add(fcuser)
          db.session.commit()
          
          return redirect('/')

    return render_template('register.html',form=form)
@app.route('/')
def hello():
    return render_template('hello.html')


if __name__=='__main__':
    basedir = os.path.abspath(os.path.dirname(__file__))
    dbfile = os.path.join(basedir, 'db.sqlite')
    
    app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
    app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
    app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
    app.config['SECRET_KEY'] = 'djfdhjhuqerb1234412bjd!@#**&^#' #원래는 복잡한 시크릿 키를 넣어야함.
    
    csrf = CSRFProtect()
    csrf.init_app(app)        
    db.init_app(app)
    db.app = app
    db.create_all()
    
    app.run(host='127.0.0.1', port = 5000, debug=True)
```
{% endtab %}

{% tab title="app.py 수정 후" %}
```
import os 
from flask import Flask
from flask import render_template
from models import db
from api_v1 import api as api_v1

app = Flask(__name__)
app.register_blueprint(api_v1, url_prefix='/api/v1')

@app.route('/register')
def register():
  return render_template('register.html')

@app.route('/')
def hello():
  return 'hello world'

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['SECRET_KEY'] = 'djfdhjhuqerb1234412bjd!@#**&^#' 

db.init_app(app)
db.app = app
db.create_all()

if __name__=='__main__':
    app.run(host='127.0.0.1', port=5000, debug=True)
```
{% endtab %}

{% tab title="user.py 전" %}
```
from flask import jsonify
from . import api 

@api.route('/test')
def test():
  return jsonify()
 
```
{% endtab %}

{% tab title="user.py 수정 후 " %}
```
from flask import jsonify
from flask import request
from models import Fcuser,db
from . import api

@api.route('/users', methods=['GET', 'POST'] ) 
def users():
    if request.method == 'POST':
        userid = request.form.get('userid')
        username = request.form.get('username')
        password = request.form.get('password')
        re_password = request.form.get('re-password')

        if not(userid and username and password and re_password):
          return jsonify({'error': 'No arguments'}), 400
        
        if password != re_password: 
          return jsonify({'error': 'Wrong password'}), 400

        fcuser = Fcuser()
        fcuser.userid = userid
        fcuser.username = username
        fcuser.password = password

        db.session.add(fcuser)
        db.session.commit()
        return jsonify(), 201

    return jsonify()
```
{% endtab %}
{% endtabs %}

  **user.py**  
4번째 줄을 @api.route\( '/test' \)를 @api.route\( '/users', method=\['GET', 'POST'\] \) 로 바꾸어 줄게요.   
그리고 사용자로부터 요청 받는 DATA가 있어요.   
userid가 필요 하므로 request가 필요해요.\(이전에는 flask-WTF import해서 사용했어요.\)  
그래서 8번째 줄에 request.form.get\('userid'\)를 넣어서 html에 해당하는 &lt;label for='userid' ~~~에 착안해서 사용하게 되요. 아이디, 사용자이름, 비밀번호, 비밀번호 재확인이 각각 존재하조?  
거기에 맞게 다 넣어 줄게요.   
  
그리고 사용자로부터 요청을 받았을때\('POST'\)  8 - 11번줄까지를 if문으로 안에서 돌아가게되요.   
7번째 줄 if request.method == 'POST': 의 의미는 앞선 의미를 내포한거에요. GET이 아닌이유는   
  
첫 째로, GET으로 받을 경우  브라우저 주소창에 그대로 개인 신상이 노출되기 때문에 POST방식을 사용한거에요.   
  
두번째로는 더 많은 DATA를 브라우저에 굳이 넣지 않고 처리 하는 장점이 있기 때문이에요.   
  
13 - 14번째 줄은 db, table에서 4가지 정보중 하나라도 없다면 400오류를 발생시키게 했으며,   
16 - 17번째 줄은 비밀번호 != 비밀번호 재확인이 맞지 않을 경우 "wrong password"와 400오류를 낼거에요.   
  
19번째 줄부터는 앞선 if 구간들을 모두 지나와서 일치할 경우의 결과들을 처리해줘야합니다. fcuser = Fcuser\(\) 이렇게 두는데요.   
근데 Fcuser\(\)는 models.py에 있으니 import해줘야 겠지요?  
  
21번째 우항의 userid를 유저가 입력한 요소를 fcuser테이블의 userid컬럼에 입력하게되요. fcuser.userid = userid로써 말이지요.   
22번째 줄에는 fcuser.username = username  
23번째 줄에는 fcuser.password = password 넣어주게 됩니다.   
  
이후 db를 넣어야 해요.   
25번쨰 줄에는 db.를 우선 넣을 거에요.   
db.session.add\(fcuser\) 물론 commit도 해줄게요.   
db.session.commit\(\)  
  
이후 해당 값들의 생성에 대한 성 처리 결과를 return jsonify\(\), 201로 반환해줄게요.   
  
여기서 잘 보면 25, 26번째에 db를 사용했지만 db를 정작 import하지 안않어요.  models.py에서 가져올게요.   
일단 위의 app.py에 있는 소스코드들이 모두 가져온 예시니 잘 참고 하세요. 

```text
from models import Fcuser, db


basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['SECRET_KEY'] = 'djfdhjhuqerb1234412bjd!@#**&^#' #원래는 복잡한 시크릿 키를 넣어야함.
         
db.init_app(app)
db.app = app
db.create_all()
```

어느 정도 완성이 되었으니 실행해서 결과를 한번봐야겠조? 정상적으로 예측된다면 회원가입 화면에서 입력란 전부 다  입력하 등록버튼을 누르 201코드가 \(F12누르고 Ctrl + G\) 아래와 같이 나와야해요.

![](../../../../.gitbook/assets/image%20%28238%29.png)

지금까지 한게 바로 회원생성 API를 만든거에요.   
  


### 정리  

app.register\_blueprint\(api\_v1, url\_prefix='/api/v1/'\) 요 한줄이 app.py에서 이번시간에 배운 중추적인 역할을 하게되요.   
즉, 내가 작성한 controler 코드들이 app.py에 모여 있지 않고 분리해서 작성되도록 도와주는 역할이에요.   
  
실제로 저 코드들은 api\_v1디렉토리에 모여 있어요. 그리고 우리가 만든 코드들은 그 안의 user.py에 저장되어 있어요.  
  
그럼 user.py안의 api라는 녀석은 \_\_init\_\_.py\(api\_v1디렉토리에서 공통으로 사용할것이기에\)에 있어요. 그래서 \_\_init\_\_.py 안에서 Blueprint\('api', \_\_name\_\_\)녀석을 통해서 api라는 객체를 만들었어요.   
  
만약 user등록 기능이외에 post 글쓰기 기능을 추가한다면 \_\_init\_\_.py에 소스코드를 추가 등록 할 수 있어요.   
  
그리고 user.py의 경우는 기존에 우리가 template코드들을 반환했는것과는 다르  
 jsonify\(\)라는 함수를 통해서 리소스만 전달해 주었어요. 요청에 대한 성공여부\(201, 400과 같이\)와 데이터만 전달한거에요. 여기서 직접적인 데이터 전달은 없었지만 에러코드만 전달한거에요.   
  
다음에는 사용자 생성, 조회, 수정, 삭제 모델인 CRUD 구현해볼게요. 

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

from . import api
```
{% endtab %}

{% tab title="user.py" %}
```
from flask import jsonify
from flask import request
from . import api

@api.route('/users', methods=['GET', 'POST'] ) 
def users():
    if request.method == 'POST':
        userid = request.form.get('userid')
        username = request.form.get('username')
        password = request.form.get('password')
        re_password = request.form.get('re-password')

        if not(userid and username and password and re_password):
          return jsonify({'error': 'No arguments'}), 400
        
        if password != re_password: 
          return jsonify({'error': 'Wrong password'}), 400

        fcuser = Fcuser()
        fcuser.userid = userid
        fcuser.username = username
        fcuser.password = password

        db.session.add(fcuser)
        db.session.commit(fcuser)
        return jsonify(), 201

    return jsonify()
```
{% endtab %}
{% endtabs %}

