# 모델 만들기 - 회원

 기능 구현중 회원 관련 모델을 만들어 볼게요

회원 관련된 기능\(CRUD\)을 말합니다.   
- 생성  
- 조회  
- 갱신   
- 삭제

###  실습 

우선 model.py 파일을 생성하여 DB와 관련된 소스코드를 작성해 볼게요.   
기존에 작성된 소스코드부터 옮겨 둘게요.   
app.py -&gt; model.py

{% tabs %}
{% tab title="app.py" %}
```
from flask import Flask 
from flask import render_template
from flask_sqlalchemy import SQLAlchemy
import os 

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')
app = Flask(__name__)

db = SQLAlchemy(app)

class Test(db.Model):
        __tablename__ = 'test_table'
        id =db.Column(db.Integer, primary_key=True)
        name = db.Column(db.String(32), unique=True)

db.create_all()

@app.route('/')
def hello():
    return 'Hello world'
```
{% endtab %}

{% tab title="models.py" %}
```
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)
```
{% endtab %}
{% endtabs %}

 근데 app을 쓸려니깐 뜬금없이 app.~~으로 쓸순 없겠조?

그래서 



{% tabs %}
{% tab title="models.py" %}
```
import os 
from app import app
from flask_sqlalchemy import SQLAlchemy

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')

app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

class webUser(db.Model): 
    __tablename__ = 'webuser'
    id = db.Column(db.Integer, primary_key=True)
    pwd = db.Column(db.String(64))
    userid= db.Column(db.String(32))
    username = db.Column(db.String(8))  
```
{% endtab %}

{% tab title="app.py" %}
```
from flask import Flask
from flask import render_template

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello world'
```
{% endtab %}
{% endtabs %}

models.py 파일에 필요한 db 소스코드들을 app,py 파일 안에서 가져왔어요. 

회원 정보를 만들어 볼게요. 

14째줄 webUser라는 클래스 이름을 지어서 db.Model을 상속 받도록 할게요. 

15번째 줄은 테이블의 이름을 webuser라고 지었어요. 

16~19번째 줄까지는 테이블 컬럼의 Id, pwd, userid, username을 각 줄마다 만들어 볼게요.  
  
여기서 models.py가 실행되어야 db가 만들어지는데요.   더불어 app.py가 실행되는데 models.py 역시 연결되어야 서로 잘 맞물려 돌아 갈거에요.   
  
기존에는 Flask 명령어를 터미널에서 실행했는데\(fastcampus에서는 FLASK\_APP=app.py flask run로 보여줬지만, 전 안되더군요.\)   
이젠 파이썬 명령어로 실행 되도록  개선해 볼거에요.   


{% tabs %}
{% tab title="app.py" %}
```text
from flask import Flask
from flask import render_template

app = Flask(__name__)

@app.route('/')
def hello():
    return render_template('hello.html')
    
if __name__=='__main__':
    app.run(host=127.0.0.1, port = 5000, debug=True)
```

10번째 줄이 파이썬으로 app.py를 구동시키는 거에요.   
11번째 줄에는 로컬 서버인 127.0.0.1을 매개변수로 넣고 포트 번호 역시 넣습니다. 그리고 개발 서버이기 때문에 debug 변수를 넣어서 즉각적인 서버의 변화를 확인하도록 매개변수로 둔거에요. 
{% endtab %}

{% tab title="" %}
```

```
{% endtab %}
{% endtabs %}

