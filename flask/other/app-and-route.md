# App & Route

## 실습1 - hello world 

```text
from flask import Flask 

app = Flask(__name__) #Flask 객체 인스턴스 생성

#라우트 작업
@app.route('/')
def hello():
    return "Hello World"
    
if __name__=='__main__':
    app.run()

```

 1째 줄에서 flask 클래스를 가져와요. 

3번째 줄에서 인스턴스를 만들게되요. 인자는 \_\_name\_\_을 넣어주세요.   
여기서 \_\_name\_\_이 의미하는건 main.py\(파이썬 파일\)로 정해져요. 서버 담당하는 파일이 시작점\(메인\)일 경우에 \_\_main\_\_으로 변경되니 이점을 해결한 것이에요. 

6번째 줄은 데코레이터를 이용해서 라우터를 이용   
라우트를 이용한 url 정의는 보안상 매우 좋다고해요. 대부분의 웹프레임워크에서 route\(\)메소드를 사용해요. 

7번째 줄은 route\(\)의 View\(\)함수에 해당되요. 문법 규칙인데요. View함수의 위치는 @, 데코레이터 아래에 위채해 있어야 해요. 

### Workflow 

![](../../.gitbook/assets/image%20%28220%29.png)



###  Routing? 

*  URL & URI를 간단하게 처리하게 해주는 기능 
* route\(\)epzhfpdlxj\(@\) 사용 

> **Warning!!   
> 2개의 서버를 띄울수 없어요.   
> 새로운 파일을 만들어서 서버를 돌릴때는 이전 서버는 종료시켜주세요.**

\*\*\*\*

## 실습2 - Hello flask 

이번엔 라우트를 한개 더 추가해볼게요.

```text
from flask import Flask 
app = Flask(__name__) # 인스턴스 생성 

@라우트 작
@app.route('/')
def hello():
   return "Hello World"

@app.route('/flask/')
def flask():
   return "Hello flask"

if __name__=="__main__":
   app.run()
```

라우트 패턴은 반드시 /\(슬래시\)로 시작해서 /\(슬래시\)로 끝나야해요.   
만약 없는 경우 파일로 인식해요. ex.index.txt 

##  실습3 - Route 매개변수 전달\(문자열\) 

```text
from flask import Flask

app = Flask(__name__) #Flask 객체 인스턴스 생성

#라우트 작업
@app.route('/')
def hello():
   return "Hello World"

@app.route('/flask/')
def flask():
   return "Hello flask"

@app.route('/user/<userName>')
def get_userName(userName):
   return "Hello "+ userName

if __name__=="__main__":
   app.run()
```

14 번째줄을 보게 되면 인자값에 &lt;userName&gt;이라는 것이 보이나요?   
동적 움직임을 url에서 보여주고 있는 거에요. 또한 View함수\(get\_userName의 매개변수 username\)와 동일 해야해요. 

## 실습4 - string말고 다른 data 전달 

```text
from flask import Flask

app = Flask(__name__) #Flask 객체 인스턴스 생성

#라우트 작업
@app.route('/')
def hello():
   return "Hello World"

@app.route('/flask/')
def flask():
   return "Hello flask"

@app.route('/user/<userName>')
def get_userName(userName):
   return "Hello "+ userName

@app.route('/userid/<int:userId>')
def get_userId(userId):
   return "user ID : {}".format(userId)

if __name__=="__main__":
   app.run()



```



18번째줄에서 &lt;int:userId&gt; 부분은 &lt;타입:매개변수명&gt;과 같은 형태로 적는데요.   
실수는 float, 정수는, int에요.   


### 실습5 -View 함수 return에 html문법 적용

```text
from flask import Flask

app = Flask(__name__) #Flask 객체 인스턴스 생성

#라우트 작업
@app.route('/')
def hello():
   return "<h1>Hello World</h1>"

@app.route('/flask/')
def flask():
   return "<h3>Hello flask</h3>"

@app.route('/user/<userName>')
def get_userName(userName):
   return "Hello "+ userName

@app.route('/userid/<int:userId>')
def get_userId(userId):
   return "user ID : {}".format(userId)

if __name__=="__main__":
   app.run()
```

> 8번째줄, 12번째줄의 html에서 h태그는 제목의 크기를 h1\(젤큼\)~h6\(젤작음\)까지 나태내요.

