# Untitled

아이디, 패스워드를 입력하고 그 결과를 다시 받아서 출력하도록 해볼게요.   
아래 소스코드를 일단 입력할게요. 

```text
from flask import Flask, redirect, url_for, request
app = Flask(__name__)

@app.route('/')
def home():
   return '''
   <html>
   <body>
   <form action="/login2">
      <input type="text" name="name">
      <input type="text" name="password">
      <input type="submit">
   </form>
   </body>
   </html>
   '''

@app.route('/login2')
def login3():
   name = request.args.get('name');
   pwd = request.args.get('password');   
   return '<html><body>welcome %s, %s</body></html>' % (name, pwd)
   


if __name__ == '__main__':
   app.run(debug = True)
```



