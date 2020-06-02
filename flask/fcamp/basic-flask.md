# Basic Flask

이 내용들은 패스트 캠퍼스 daily challenge로 인해 작성 드려요.  

## 시작하기 앞서 

 사전 작업을 할게요.   


#### 1. 디렉토리 구성 

* Flask\_기본 -&gt; project  

#### 2. 가상환경 생성 

```text
# 윈도우 사용자 기준 
# 방법1.
virtualenv 가상환경이름1 
source 가상환경이름1/Scripts/activate (혹은 activate.bat 혹은 activate.ps1)

# 방법2 
# 방법1이 안될 경우 powershell을 관리자 모드로 실행해 주세요. 
python -m venv 가상환경이름2
Set-ExecutionPolicy Unrestricted # 보안 설정을 꺼버리는거에요. 
Y(yes)눌러주세요. 
cd 가상환경이름2/Scripts.\activate 

```

가상환경은 OS별 python 혹은 아나콘다 별로 다르니 구글링 통해서 해결하는게 최고에요. 

#### 3. flask 설치 

```text
pip install flask  
```

## 바로 실습 

{% code title="app.py " %}
```text
from flask import Flask 
app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello world'


```
{% endcode %}

```text
# 터미널 환경(vscode라면 ctrl+j)가셔서 

(venv) C:\Project\helloflask>flask run # flask run 명령어 실행 

 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 
 # 127.0.0.1:5000 ctrl + c 눌러서 실행 시켜 주세요. 
```

 실제 터미널 환경에서는 FLASK\_APP=app.py flask run 명령어인데 실행이 안되서 삽질을 몇시간씩 했네요. -.- fastcampus는 QnA 게시판이라도 만들어두면 좋았을텐데....휴~~~~~\(이메일 보내도 답변 언제 올지 모른다는\)



