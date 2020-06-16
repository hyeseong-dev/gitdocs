# 회원 상세 읽기,수정,삭제 완성하기 \(CRUD 완성하기\)

CRUD를 완성해 보겠습니다.   
사용자에 대한 상세보기 조회와 수정 삭제를 구현해볼게요. 이미 serialize함수를 만들었기에 기본적인 부분은 만들어 졌어요.   


```text
from flask import jsonify
from flask import request
from models import Fcuser,db
from . import api


@api.route('/users', methods=['GET', 'POST'] ) 
def users():
    if request.method == 'POST':
        userid = request.form.get('userid')
        username = request.form.get('username')
        password = request.form.get('password')
        re_password = request.form.get('re-password')

        if not(userid and username and password and re_password):
          return jsonify({'error': 'No arguments'}), 400
        
        if password != re_password: 
          return jsonify({'error': 'Wrong password'}), 400

        fcuser = Fcuser()
        fcuser.userid = userid
        fcuser.username = username
        fcuser.password = password

        db.session.add(fcuser)
        db.session.commit()
        
        return jsonify(), 201

    users = Fcuser.query.all()
    return jsonify([user.serialize for user in users])
```



