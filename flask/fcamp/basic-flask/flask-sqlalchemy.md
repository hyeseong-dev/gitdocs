# Flask-SQLAlchemy

## Flask-SQLAlchemy

SQL미SQLAlchemy는 모델 부분을 담당하는 라이브러리에요. 보통 ORM이라고 불려요. 

### 설치

```text
pip install flask-sqlalchemy
```

 기본적으로 sqlalchemy를 사용하는데, flask에서 손쉽게 라이브러리로 적용한거에요. 

##  실습 

```text
from flask import Flask 
from flask_sqlalchemy import SQLAlchemy
import os 

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')
app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True

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
* COMMIT : DB에 동작을 쌓은후 그 쌓인 동작들을 DB에 COMMIT 명령어를 통해서 반영되요. 

