# 회원 생성 API 만들기



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
원관리api생성/register/register.html
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

