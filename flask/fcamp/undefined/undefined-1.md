# 뷰 만들기 - 회원

 회원 가입 뷰를 Bootstrap을 통해 만들어 볼게요. 

###  실습 

1. template 폴더 안에 register.html 파일을 생성해 주세요. 
2. bootstrap 사용을 위한 기본적인 metatag를 사용할거에요. 

{% tabs %}
{% tab title="register.html" %}
{% code title="C:\\Project\\templates\\register.html" %}
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
            <form method="POST" action=".">
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
                 <label for="re-password">비밀번호확인</label>
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
{% endcode %}
{% endtab %}

{% tab title="app.py" %}
```
import os
from flask import Flask
from flask import render_template
from models import db

app = Flask(__name__)

@app.route('/register')
def register():
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
```
{% endtab %}
{% endtabs %}



