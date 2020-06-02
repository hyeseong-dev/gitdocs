# Jinja2

##  실습 

html 파일을 만들어서 Hello world를 출력하도록 해볼게요. 

```text
import os 
from flask import Flask
from flask import render_template 
from flask_sqlalchemy import SQLAlchemy
import os 

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)


@app.route('/')
def hello():
    return render_template('hello.html')
```

 19번째이 기존에는 return 'hello world라고 작성되었는데요. 그 의미는 app.py라는 이 Control안에서 View코드까지 작성한거였어요.

그런데 이번에 바뀐 19번째줄은 return render\_template\('hello.html'\)로 작성해서 control와 view가 구분되게 되는거에요. 

아래와 같이 templates 폴더를 생성해주세요.   
그리고 이번에 app.py를 재실행하면 hello.html 에 작성한 Hello world를 볼 수 있을 거에요.

```text
C:.
│  app.py
│
├─templates
│      hello.html
```

사실 우리는 Jinja라는 템플릿 라이브러리를 사용하고 있지만 진짜 우리가 Jinja라이브러리를 사용하지 않고 flask가 내부적으로 알아서 사용하고 있기 때문에 flask가 제공하는 함수를 통해서 jinja를 사용하게 되요. 

