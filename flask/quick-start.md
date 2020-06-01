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





