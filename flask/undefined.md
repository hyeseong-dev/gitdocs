# 시작하기

### Flask?

###  **플라스크**\(Flask\)는 [파이썬](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%B4%EC%8D%AC)으로 작성된 마이크로 [웹 프레임워크](https://ko.wikipedia.org/wiki/%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC)의 하나로, Werkzeug 툴킷과 [Jinja2](https://ko.wikipedia.org/w/index.php?title=Jinja&action=edit&redlink=1) 템플릿 엔진에 기반을 둔다. [BSD 라이선스](https://ko.wikipedia.org/wiki/BSD_%ED%97%88%EA%B0%80%EC%84%9C)이다.

플라스크의 최신 안정판은 2017년 5월 기준으로 1.1.1이다.[\[3\]](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC_%28%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%29#cite_note-3) 플라스크 프레임워크를 사용하는 애플리케이션에는 [핀터레스트](https://ko.wikipedia.org/wiki/%ED%95%80%ED%84%B0%EB%A0%88%EC%8A%A4%ED%8A%B8),[\[4\]](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC_%28%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%29#cite_note-4) [링크드인](https://ko.wikipedia.org/wiki/%EB%A7%81%ED%81%AC%EB%93%9C%EC%9D%B8),[\[5\]](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC_%28%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%29#cite_note-5) 플라스크 자체를 위한 공동체 웹 페이지를 포함한다.[\[6\]](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC_%28%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%29#cite_note-6)

플라스크는 특별한 도구나 라이브러리가 필요 없기 때문에 마이크로 프레임워크라 부른다.[\[7\]](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC_%28%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%29#cite_note-7) 데이터베이스 추상화 계층, 양식 유효성 확인, 기타 기존의 서드파티 라이브러리가 공통 기능을 제공하는 구성 요소가 없다. 그러나 플라스크는 플라스 자체에서 구현된 것처럼 애플리케이션 기능을 추가할 수 있는 확장 기능을 지원한다. 확장 기능은 객체 관계 매퍼, 양식 유효성 확인, 업로드 관리, 다양한 개방형 인증 기술, 여러 공통 프레임워크 관련 도구들을 위해 존재한다. 확장 기능들은 코어 플라스크 프로그램에 비해 훨씬 더 정기적으로 업데이트된다.[\[8\]](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC_%28%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%29#cite_note-8)

출처: [https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC\_\(%EC%9B%B9\_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC\)](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9D%BC%EC%8A%A4%ED%81%AC_%28%EC%9B%B9_%ED%94%84%EB%A0%88%EC%9E%84%EC%9B%8C%ED%81%AC%29)

### 준비물 

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



  






