# 컨트롤러만들기-회원

## 컨트롤러 개발

  
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



### GET, POST 방식

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



### GET, POST 처리 방식 

```text
import os
from flask import Flask
from flask import request 
from flask import render_template
from models import db

app = Flask(__name__)

@app.route('/register', methods=['GET', 'POST'])
def register():
    if request.method == 'GET':
        return render_template('register.html')
    else: 
        # 회원정보 생성 
        return redirect('/')

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

12번째 줄에서 'GET' 방식이 도달하게 되면 그냥 화면을 보여주면 되요.   
13번째 줄처럼 return render\_template\('register.html'\) 말이에요.   
  
그럼 여기서 데이터를 가져와서 회원 가입을 하고  15번째에서 redirect를 시키면\(from flask import redirect를 맨 윗 부분에 import시켜 주세요. \)   
그안에 인자가\(/\) 루트페이지로 되어있조? 즉, 홈페이지로 이동하게 되요.   


### 모델 사용을 통한 회원 정보 생성

  
이제 그럼 모델을 사용해서 회원정보를 생성하는것 까지 해볼까요?  
클래스만 사용해서 데이터를 저장할 수 있어요. 

그렇기 때문에 모델에 있는 클래스를 가져와야 해요.   
7번째 줄에 from models import Fcuser 작성해서 말이지요.   
  
자~ POST방식으로 들어온 16번째 줄에서 사용자 생성을하고 redirection을 하면 되겠조. 하지만 클래스 변수로 생성하기 이전에 입력 받은 값을 확인해 봐야해요.   
userid = request.form.get\('userid'\)  
request안에 from이라는 변수가 있고 그 안에서 하나씩 꺼낼수 있어요.

결국 아래와 같이 작성하는 이유는 값을 전달해주기 위함이에요. 

> userid = request.form.get\('userid'\)   
> username = req0uest.form.get\('username'\)   
> password = request.form.get\('password'\)   
> re\_password = request.form.get\('re\_password'\)
>
> print\(userid\)

```text
import os
from flask import Flask
from flask import request 
from flask import render_template
from models import db

from models import Fcuser

app = Flask(__name__)

@app.route('/register', methods=['GET', 'POST'])
def register():
    if request.method == 'GET':
        return render_template('register.html')
    else: 
        userid = request.form.get('userid')
        return redirect('/')

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



print\(userid\) 부분을 넣게 되면 터미널창에 값이 찍혀서 출력되게되조.   
값이 잘 들어 오는 걸 확인했으면 print\(userid\)는 지워주세요. 

```text
ㅁㄴㅇㄹ
127.0.0.1 - - [08/Jun/2020 01:32:54] "POST /register HTTP/1.1" 302 -
127.0.0.1 - - [08/Jun/2020 01:32:54] "GET / HTTP/1.1" 200 -
```

 몇 가지 검증만 해보겠습니다.   
첫째, 모든값의 존재 유무 확인   
둘쨰, 비밀번호가 서로 일치 여부 확인  
  
  
첫번째 검증은 if문을 사용해서 모든 변수값이 존재하는지 안하는지 and 로 묶고 소괄호로 모두 묶은 다음에 not을 앞에다가 두면 된답니다.   
결국 모든 값이 존재하지 않는다면 return 한값을 register.html로 랜더링해서 회원가입 페이지로 다시 돌아가게 만드는거조. 

```text
if not (userid and username and password and re_password):
    return render_template('register.html')
```

또한 만약 비밀 번호가 다른 경우에도 위의 return결과와 동일하게 회원가입 페이지로 render처리 하면 된답니다. 

```text
if password != re_password
    return render_template('register.html')
```

정상적으로 확인했으면 이제 유저를 생성해볼게요.    
일단 클래스 변수를 만들거에요. 빈 클래스 변수를 들때 넣어도 되고 생성할때 넣어도 되는 2가지 옵션이 있어요. 

우선 따로 따로 해볼게요. 

```
fcuser = Fcuser()
fcuser.userid = userid
fcuser.username = username
fcuser.password = password

db.session.add(fcuser)
db.session.commit()
```

 클래스 변수를 다 만들었어요. 그럼 얘를 추가 시켜줘야해요.   
추가 시키는 방법에는 db를 사용하게 되요. !!!  
  
db.session.add\(fcuser\) fcuser가 add\(\)로 session에 추가되게 되면~~~   
사실 db에 넣겠다는 동작은 다 한건데요. 중요한게 남았어요. 바로 commit을 해야해요.   
사실 commit을 안해도 되는 이유가! 앞전에 환경설정에서 

> app.config\['SQLALCHEMY\_COMMIT\_ON\_TEARDOWN'\] = True

이렇게 소스 코드를 입력한 적이 있어요.   
하지만 의도적으로 commit해주는 습관을 들이기 위해서   
db.session.commit\(\)를 해준답니다.   
  
그럼 정상적으로 값을 입력했다면 db에 값이 저장이 될거에요.  
일단 값을 직접 넣어보고 db에 가서 진짜값이 들어 있는지 확인도 해볼게요.  



{% tabs %}
{% tab title="app.py" %}
```text
import os
from flask import Flask
from flask import request 
from flask import redirect
from flask import render_template
from models import db

from models import Fcuser

app = Flask(__name__)

@app.route('/register', methods=['GET', 'POST'])
def register():
    if request.method == 'POST':                       
        userid = request.form.get('userid')
        username = request.form.get('username')
        password = request.form.get('password')
        re_password = request.form.get('re_password')

        if (userid and username and password and re_password) and password == re_password :
          fcuser = Fcuser()
          fcuser.userid = userid
          fcuser.username = username
          fcuser.password = password
  
          db.session.add(fcuser)
          db.session.commit()
          
          return redirect('/')

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

{% tab title="models.py" %}
```
import os 
from flask_sqlalchemy import SQLAlchemy


db = SQLAlchemy()

class Fcuser(db.Model): 

    __tablename__ = 'Fcuser'
    id = db.Column(db.Integer, primary_key=True)
    password = db.Column(db.String(64))
    userid= db.Column(db.String(32))
    username = db.Column(db.String(8))  
```
{% endtab %}
{% endtabs %}

