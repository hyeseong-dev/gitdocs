# Flask-SQLAlchemy

## Flask-SQLAlchemy

SQLAlchemy는 모델 부분을 담당하는 라이브러리에요. 보통 ORM이라고 불려요. 

### 설치

```text
pip install flask-sqlalchemy
```

 기본적으로 sqlalchemy를 사용하는데, flask에서 손쉽게 라이브러리로 적용한거에요. 

##  소스코드 작성 1  sqlite 설정 

```text
from flask import Flask 
from flask_sqlalchemy import SQLAlchemy
import os 

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

class Test(db.Model):
        __tablename__ = 'test_table'
        id =db.Column(db.Integer, primary_key=True)
        name = db.column(db.String(32), unique=True)

@app.route('/')
def hello():
    return 'Hello world'


```

2번째 줄에서 flask\_sqlalchemy 라이브러리를 가져오고 거기서 SQLAlchemy라는 패키즈를 써게되요.  
그리고 데이터베이스는 sqllite라는 db를 사용할거에요. 

장점 

* 별도의 설치가 필요없음 
* 파일로 지정하고 그 파일을 db로 사용함. 

이 프로젝트 경로를 절대 경로로 사용하기 위해서   
3째줄에 os 패키지를 가져오게되요.   
5째줄에 절대 경로를 basedir이라는 변수에 저장하게 되요.   
6째줄에는 dbfile 변수도 만들게 되요. 첫번째 매개변수는 프로젝트 절대 경로인 basedir 뒤에 db.sqlite파일을 붙여서 데이터를 가져오는 경로+db파일을 만든거라고 보면되요. 

####  SQLAlchemy 설정값

8번째 줄에 내가 사용할 데이터베이스의 URI 값을 할당 한다는 말이에요.   
제가 사용할 db가 sqlite이기 때문에 할당 연산자\(=\) 오른쪽에 sqlite라는 이름이 오는데요.   
  
만약 다른 db를 사용할 경우 그 이름이 바뀌게 되요.   
\(예. mysql을 쓰게 되면 id와 password를 필요로 하기 때문에 추가적인 작업 필요\)   
sqlite는 파일에 정보를 저장하지만 다른 db의 경우 아이디, 비번이 필요하고 db가 어디에서 실행중인지도 코딩해야해요. 여기서는 그 작업들을 DATABASE\_URI라는 값 한줄로 표현해요.   
  
이렇게해도 DB에 연결은 되었지만 몇가지 설정을 더 해 볼게요.   
9번째 줄에 app.config\['SQLALCHEMY\_COMMIT\_ON\_TEARDOWN'\] = True   
TEARDOWN과 COMMIT이 있는데 알아볼게요. 

* TEARDOWN : 사용자가 만약 HELLO WORLD에 접속\(요청\)했어요. 이후 HELLO WORLD에서 사용자가 원하는 정보를 전달 했을때  순간을 TEARDOWN이라고 해요.  즉, 사용자 요청의 끝을 의미함. 그리고 TEARDOWN 이후에는 COMMIT을 한다는 말인데요.  
* COMMIT : DB에 동작을 쌓은후 그 쌓인 동작들을 DB에 COMMIT 명령어를 통해서 반영되요.  결국 DB에 내가 원하는 정보들을 실제로 반영하는 역할이라고 보면 되요.  
* ```text
  @app.route('/')
  def hello():
      return 'Hello world'
  ```

 이 business logic인 hello에 접속하게 되면 만약 내가 놓친 부분이 없게 다 반영 해달라는 소스코드가 app.config\['SQLALCHEMY\_COMMIT\_ON\_TEARDOWN'\] = True 에요.   
  
10번째 줄의 app.config\['SQLALCHEMY\_TRACK\_MODIFICATIONS'\] = False는 Flask 2.0버전 이상부터 들어오게 되었는데요.   
참고로 이 값을 True 또는 False든 설정하지 않으면 Warning message가 출력되기에 지정해 둘게요. 

 12번째 줄 

```text
db = SQLAlchemy(app)
```

그리고 여러 데이터베이스에 관한 클래스나 함스를 사용할텐데요. 그때 필요한 최상위 변수를 db라는 이름으로 만들었어요.   
이제 이 db라는 변수로 데이터를 넣기도 하고 모델을 만들기도 하고 여러 군데에서 사용해요. 

### 소스코드 작성 1  Test용 db작성 

클래스를 만들어서 db 테스트를 해볼게요.   


```text
from flask import Flask 
from flask_sqlalchemy import SQLAlchemy
import os 

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

class Test(db.Model):
        __tablename__ = 'test_table'
        id =db.Column(db.Integer, primary_key=True)
        name = db.column(db.String(32), unique=True)

db.create_all()

@app.route('/')
def hello():
    return 'Hello world'
```

14번째 줄에 Test라는 클래스 이름을 만들고요 db.Mode이라는 클래스를 상속받게되요.   
  
이후 Test는 하나의 Model이 되는거에요. 데이터를 넣고 빼는게 가능하다는 말이기도 해요.   
넣고 뺴는 모습을 일반적으로 schema라고 하는데 그 schema의 모습은 Test클래스안의 변수로 만들게 되는거에요.   
이 속성 값들은 id와 name이 있는데요.   


15번째 줄 우측항에서는 테이블 이름을 지정 한거에요.   
16~17번째 줄은 SQL 지식이 필요한데요. db.Column 메소드는 말그대로 컬럼이에요. 그 컬럼의 특성을 정수로 할지, 문자로 할지 첫번째 매개변수로 지정했고요. 두번째 매개변수는 key값을 설정해준거에요. 

19번째 줄 db.create\_all\(\) 메서드로 db를 생성하게 되요. 반드시 모델 설정&모델 등록이 사전에 진행되고 db를 만드는거에요. 



![db.sqlite&#xAC00; &#xC0DD;&#xC131;&#xB41C; &#xBAA8;&#xC2B5;](../../../.gitbook/assets/image%20%28223%29.png)

 정상적으로 db.sqlite가 생성된걸 확인했나요?  
터미널에서 

```text
cat db.sqlite # 작성했던 내용들이 보일거에요.
```

