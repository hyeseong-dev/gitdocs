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

@app.route('/register') # form태그에 대한 더미 컨트롤러에요.
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



2번째~9번째 줄까지 head정보를 나타낸답니다.   
  
다음은 body를 만들거에요. body를 통해서 회원가입 페이지의   
아이디, 사용자이름, 비밀번호, 비밀번호 확인, 등록버튼을 구현할거에요.   

16번째 줄의 &lt;div class="row mt-5"&gt; 가로 5줄을 의미해요. 이렇게 class이름을 지정하면 bootstrap이 약속된 이름이란걸 인식해서 표를 만들어 주는거에요. 

 17번째 줄에서 &lt;div class="col-12"&gt; 세로 12줄을 의미해요.  
html의 form태그를 18번째줄에서 만들어 줍니다.   
  
18번째 줄에서 &lt;form method="POST" action="."&gt;

> form 태그는  웹상에서 사용자 정보를 입력하는 여러\(text, button, checkbox, file, hidden, image, password, radio, reset, submit\)방식의 영역을 제공하며, 사용자로부터 할당된 데이터를 서버로 전송하는 역활을 담당  
>   
> 출처: [https://mohwaproject.tistory.com/entry/FORM-객체란](https://mohwaproject.tistory.com/entry/FORM-%EA%B0%9D%EC%B2%B4%EB%9E%80) \[무하프로젝트\]

19번째 줄부터 34번째 줄까지 form에 들어갈 필드들입니다. 

> 참고로 bootstrap은 class="form-group",  class="form-control"이 있어야 가능해요.   
> 기존에 가지고 있던 css와 javascript기능을 구현한 UI를 가져올 수 있어요.  그러니 head부분에 bootstramp을 박아버린만큼 꼭 규칙을 따라야 겠조?





