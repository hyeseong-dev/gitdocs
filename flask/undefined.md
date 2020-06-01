# 시작하기

###  준비물 

### 파이썬 설치 

우선 파이썬을 설치해주세요.   
아래와 같이 python 명령어를 입력하면 버전3.8.3이 나오게 되요. 

```text
PS C:\Project> python
Python 3.8.3 (tags/v3.8.3:6f8c832, May 13 2020, 22:20:19) [MSC v.1925 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

### flask설치 

```text
pip install flask 
```



###  hello.py 

hello world를 출력해볼게요. 아래 소스코드를 작성하고 파일이름을 작성해주세요.   
기본적인 파이썬을 알고 있다는 가정하에서 기초적인 파이썬 내용은 생략할게요. 

{% code title="main.py" %}
```text
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello(): 
    return "Hello World!!"

if __name__ == "__main__":
    app.run() 
```
{% endcode %}

5번째 줄에 @데코레이터를 사용해요.   
그리고 app객체에 내장된 메서드인 route\(\)를 사용해 url경로를 설정해준거에요.  
보안상의 장점이크고요. 대부분의 프레임워크들이 route를 사용하기도 하고요. 예전에는 url경로에 파일명까지 모두 적었어요. 하지만 이제는 단순히 줄여서 적을수 있어요. 

6번째 줄에서는 hello\(\)를 적었는데요. 호출시 당연히 'Hello World'라는 문자가 지정된 웹페이지에 출력될거에요. 

vscode를 이용해서 파일을 실행하면 터미널에서 return 되는 메시지들이 아래와 같이 나올거에요.   
맨 마지막 http://127.0.0.1:5000/ \(Press CTRL+C to quit\) 과 같이 실행하면 웹브라우저에서 Hello World가 잘 찍혀서 나온걸 확인 할 수 있어요. 

```text
PS C:\Project\helloflask> & C:/Users/w/AppData/Local/Programs/Python/Python38-32/python.exe c:/Project/helloflask/hello.py
 * Serving Flask app "hello" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```



  






