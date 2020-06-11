# 회원 생성 API 만들기



{% tabs %}
{% tab title="app.py" %}
```text
# 회원관리api생성/app.py

from flask import Flask
from flask import render_template
from api_v1 import api as api_v1

app = Flask(__name__)
app.register_blueprint(api_v1, url_prefix='/api/v1')

@app.route('/register')
def register():
  return render_template('register.html')

@app.route('/')
def hello():
  return 'hello world'

if __name__=='__main__':
    app.run(host='127.0.0.1', port=5000, debug=True)
```
{% endtab %}

{% tab title="models.py" %}
```
# 회원관리api생성/models.py

from flask_sqlalchemy import SQLAlchemy 

db = SQLAlchemy()

class Fcuser(db.Model):
  __tablename__ = 'fcuser'
  id = db.Column(db.Integer, primary_key=True)
  password = db.Column(db.String(64))
  userid = db.Column(db.String(32))
  username = db.Column(db.String(8))
```
{% endtab %}

{% tab title="\_\_init\_\_.py" %}
```
# 회원관리api생성/api_v1/__init__.py

from flask import Blueprint


api = Blueprint('api', __name__)

from . import user
```
{% endtab %}

{% tab title="user.py" %}
```
# 회원관리api생성/api_v1/user.py

from flask import Blueprint


api = Blueprint('api', __name__)

from . import user
```
{% endtab %}
{% endtabs %}

