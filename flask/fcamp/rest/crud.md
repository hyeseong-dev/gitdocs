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
    
@api.route('/user/<uid>>', methods=['GET', 'PUT', 'DELETE'])
def user_detail(uid):
    if request.method == 'GET':
        user= Fcuser.query.filter(Fcuser.id == uid).first()
        return jsonify()     
```

@api.route\('/users/&lt;uid&gt;', \) URI에서 입력값을 받을 수 있게 &lt;uid&gt; 꺽쇠 괄호로 값을 받을 수 도 있어요. 수정, 삭제, 조회를 조회 할 수 있어요.  그리고 user\_detail\(\)이라는 함수가 만들어져요.   
해당 함수안의 매개변수 uid는 route\(\)메소드의 꺽쇠 이름과 동일해야해요. 그렇지 않으면 서로 찾지를 못해서 오류가 발생해요.   
  
이제 method를 확인해서 원하는 API를 만들면 되요. 먼저 'GET'부터 만들어 볼게요.   
GET요청은 조회에요. 쿼리에서 id가 들어 왔으니깐. Fcuser.query.fileter\(Fcuser.id == uid\).first\(\)를 사용해서 모든 id정보중에서 하나만 뽑아내게 되요.   
그리고 return jsonify\(\)해주는데요. 여기서 user는 object에요. 이후 serialize하게되는데요.   
바로 실행해 볼게요. 



