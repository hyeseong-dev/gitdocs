# 회원 목록 API 만들기

## 이전 시간 소스 코드들 

{% tabs %}
{% tab title="app.py" %}
```text
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

{% tab title="models.py" %}
```
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

{% tab title="templates/register.html" %}
```
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
          <form method="POST" action="/api/v1/users">
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

{% tab title="ap1\_v1/user.py" %}
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

{% tab title="api\_v1/\_\_init\_\_.py" %}
```
from flask import Blueprint


api = Blueprint('api', __name__)

from . import user
```
{% endtab %}
{% endtabs %}

이번 시간에는 회원 목록을 조회하는 api를 만들어 볼게요.   
REST API에서 리소스에 대한  아래 7번째 줄의 "GET"을 하가되면, 데이터에 대한 조회에요.  
\(반대로 "POST"는 생성이에요. \) 

> ```
> from flask import jsonify
> from flask import request
> from models import Fcuser,db
> from . import api
>
>
> @api.route('/users', methods=['GET', 'POST'] ) 
> def users():
>     if request.method == 'POST':
>         userid = request.form.get('userid')
>         username = request.form.get('username')
>         password = request.form.get('password')
>         re_password = request.form.get('re-password')
>
>         if not(userid and username and password and re_password):
>           return jsonify({'error': 'No arguments'}), 400
>         
>         if password != re_password: 
>           return jsonify({'error': 'Wrong password'}), 400
>
>         fcuser = Fcuser()
>         fcuser.userid = userid
>         fcuser.username = username
>         fcuser.password = password
>
>         db.session.add(fcuser)
>         db.session.commit()
>         
>         return jsonify(), 201
>
>     users = Fcuser.query.all()
>     return jsonify()
> ```

/users 라는 루트에 "POST"요청이 오면 회원 생성을 하는 코드들을 이전 시간에 만들어 본거에요.   
그리고 만약 '/users'에 "GET"하게 될 경우 모든 사용자를 가져오는 API가 될거에요. 그래서 이 API까지 만들어 볼게요.   
  
참고로 이미 9번째 줄부 \( if request.method == 'POST': \) 29번째 줄\( return jsonify\(\), 201\) 까지 이미 만들어져 있기에 이 소스코드를 그대로 쓰고 반대로 "GET"에 대한 코드를 작성해야 해요.   
  
바로 아래 31번째 줄부터 작성해 볼게요.   
일단 모든 사용자를 가져 올 것이기에 users = Fcuser.query.all\(\) 단순히 모델.query.all\(\)을 하게되면 해당 모델의 모든 쿼리를 가져온다는 말이에요.   
  
바로 아래 return jsonify\(users\)로 작성하고 나서 실행해 보면 Serializable이라는 오류가 떠요.   


> 기본적으로 Json 은 직렬화가 되어야해요.

즉, 파이썬이 문자열을 클래스 변수로 표현하기 어렵다는 말이라는 거조. 그래서 우리는 이를 파이썬에게 직접 알려줘야해요.   
어떻게 써야하는지, 어떻게 보여줘야 하는지 말이죠.

#### 방법1 : 

실제 딕셔너리를 아래 같이 만들어 주는거에요. 하지만 당연히 이렇게 하면 비효율적이겠조? 코드들을 다 때려박는거기 때문이조.

```text
users = Fcuser.query.all()
return jsonify({
'id': aaa,

})
```

### 방법2 

모델안에 직렬화 하는 함수 or 변수를 넣어둬서 이후 그 안에서 진행형 리스트를 만들어서 반환할거에요. 물론 진행형 리스트를 쓰지 않고 반환할수 있지만 일단 써보도록 할게요. 

#### 2.1 직렬화 

models.py 파일 Fcuser 클래스 안에서 12번째 줄에 "@property" 속성 값을 만들거에요.   
사실 함수로 해도 상관은 없어요.   
  
설명 이어 갈게요. @&lt;-- 데코레이터를 property와 붙여서 사용하게 되면, 실제로 함수로 만들지만 함수처럼 사용하는  것이 아닌 변수처럼 사용 할 수 있게 되요. 

```text
from flask_sqlalchemy import SQLAlchemy 

db = SQLAlchemy()

class Fcuser(db.Model):
  __tablename__ = 'fcuser'
  id = db.Column(db.Integer, primary_key=True)
  password = db.Column(db.String(64))
  userid = db.Column(db.String(32))
  username = db.Column(db.String(8))
  
  @property
  def serialize(self): 
    return {
      'id': self.id,
      'password': self.password,
      'username': self.username
    }
```

12번쨰줄부터 18번째 줄까지 직렬화 소스코드를 작성하게 되면, models.py에서 serialze라는 변수!가 나오게 되면 그 이후 딕셔너리 값들이 나오게 되는 거에요. 

결국 그 모델에서 직렬화 하는 함수나 변수를 만들어 놓고 이를 활용하여 API결과로 전달할때 리스트를 만들어 주거나 여러 사용자를 반환 할 수 있게되요.   
  
혹은 리스트를 직접 만들수도 있어요.   
  
예시 app.py 아래 처럼 리스트를 만들고 for문을 돌리고 리스트 변수에 직렬화한 변수를 넣어 줄수도 있어요. 이렇게 해도 동작은 해요. 

```text
users = Fcuser.query.all()
res_user = []
for user in users: 
    res_uses.append(user.serialize)
return jsonify(res_user)
    
```

하지만 위 예시 이전에 앞서서 진행형 리스트를 만들 목적이었으므로 계속 가도록 해볼게요.   




> ```
> from flask import jsonify
> from flask import request
> from models import Fcuser,db
> from . import api
>
>
> @api.route('/users', methods=['GET', 'POST'] ) 
> def users():
>     if request.method == 'POST':
>         userid = request.form.get('userid')
>         username = request.form.get('username')
>         password = request.form.get('password')
>         re_password = request.form.get('re-password')
>
>         if not(userid and username and password and re_password):
>           return jsonify({'error': 'No arguments'}), 400
>         
>         if password != re_password: 
>           return jsonify({'error': 'Wrong password'}), 400
>
>         fcuser = Fcuser()
>         fcuser.userid = userid
>         fcuser.username = username
>         fcuser.password = password
>
>         db.session.add(fcuser)
>         db.session.commit()
>         
>         return jsonify(), 201
>
>     users = Fcuser.query.all()
>     return jsonify([user.serialize for user in users])
> ```

위 소스코드 32번째 줄의 매개 변수가 한줄로써 손쉽게 표현된걸 볼수 있어요. 

