# Quick Start

빠르게 플라스크 실습을 해볼게요. 

### hello.py 

{% code title="hello.py\(o\), flask.py\(x\) flask랑 충돌나요.  " %}
```text
from flask import Flask 
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__== '__main__':
    app.run()
```
{% endcode %}



1.  Flask class를 import한거에요. Flask의 인스턴스가 WSGI 어플리케이션이 될거에요. 첫번째 인자는 이 어플리케이션의 이름이다. 여러분이 단일 모듈을 사용한다면\(위의 예제처럼\),여러분은 \_\_name\_\_을 사용해야해요. 왜냐하면, 어플리케이션으로 시작되는지, 혹은 모듈로 임포트되는지에 따라 이름이 달라지기 때문이죠.\('\_\_main\_\_' 대 실제로 임포트한 이름\)  서버를 담당하는 파일이 시작점\(메인\)일 경우에 \_\_main\_\_변경되니 이점을 해결한 거에요. 

2. Flask class의 인스턴스를 생성해줘요. 인자로 모듈이나 패키지의 이름을 넣게되는데요. 플라스크에서 템플리이나 정적파일을 찾을때 필요해요. 

3. route\(\) 데코레이터를 이용해서 Flask에게 어떤 URL이 우리가 작성한 함수를 실행시키는지 알려줘요. 

4. 작성된 함수의 이름은 그 함수에 대한 URL을 생성하는데 사용되요.\(url\_for 함수\) 해당 함수는 사용자 브라우저에 보여줄 메시지를 리턴해줘요. 

5. 최종적으로 run\(\)함수를 이용해서 로컬서버로 실행되요. 

