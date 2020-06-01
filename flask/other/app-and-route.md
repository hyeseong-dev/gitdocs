# App & Route

### main.py - hello world 

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



