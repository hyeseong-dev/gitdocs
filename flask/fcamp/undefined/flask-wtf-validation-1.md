# Flask-WTF 활용을 통한 Validation -1

### Flask-WTF 패키지 

  
이 번 시간에는 Flask-WTF라 패키지를 설치하여 진행해 볼게요.   
   
Flask는 micro framework이므로 기본적으로 많은 기능을 갖추고 있지 않아요.   
그럼 다른 패키지를 끌어다와서 사용해야하는데 그 중에서 html의 form태그 기능을 좀더 편리하고 간결하고 빠르게 설정하고 구동시키기 위한 녀석이 Flask-WTF 패키지에요.   
  
결국, Form관리를 담당하는 것이 Flask-WTF입니다.  


### Flask-WTF 패키지 설치 

```text
pip install Flask-WTF
```

  
이제 이 패키지가 어떤 역할을 하고 기존에 갖추고 있던 Form태그에 어떤 변화를 줄것인지가?! 관건이겠조?   
Flask-WTF패키지를 갖추고 아래 register.html을 파이썬을 이용해서 forms.py 파일을 생성하여 이를 register.html에 data를 다시 재전달하는 방식으로 모듈화하 좀더 짧고 임펙트있게  바꿀거에요.  


#### 장

* CSRF라는 보호기법을 사용 할 수 있음 
* Validation! 즉, 값에 대한 검증도 수월하게 할 수 있음.

{% tabs %}
{% tab title="register.html 수정전" %}
{% code title="templates/register.html \# 바꾸기전 " %}
```text
<html>
    <head>
      <meta charset="utf-8" />
      <meta name='viewport' content='width=device-width, initial-scale=1, shrink-to-fit=no' />
      <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
      <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>
    </head>

    <body>
      <div class="container">
        <div class="row mt-5">
          <h1>회원가입</h1>
        </div>
        <div class="row mt-5">
          <div class="col-12">
            <form method="POST">
               <div class="form-group">
                 <label for="userid">아이디</label>
                 <input type="userid" class="form-control" id="userid" placeholder="아이디" name="userid" />
               </div>
               <div class="form-group">
                 <label for="username">사용자 이름</label>
                 <input type="text" class="form-control" id="username" placeholder="사용자 이름" name="username" />
               </div>
               <div class="form-group">
                 <label for="password">비밀번호</label>
                 <input type="password" class="form-control" id="password" placeholder="비밀번호" name="password" />
               </div>
               <div class="form-group">
                 <label for="re-password">비밀번호확인</label>
                 <input type="password" class="form-control" id="re-password" placeholder="비밀번호확인" name="re-password" />
               </div>
               <button type="submit" class="btn btn-primary">등록</button>
            </form>
          </div>
        </div>
      </div>
    </body>
</html>
```
{% endcode %}
{% endtab %}

{% tab title="" %}
```

```
{% endtab %}
{% endtabs %}

### forms.py 작성 

목적 : Flask\_WTF패키지를 사용하여 register.html 전통적이었던 파일을 파이썬 라이브러리\(Flask-WTF\)방식에 맞추어 가볍고 간편한 모듈화를 하기 위함임.

```text
from flask_wtf import FlaskForm
from wtforms import StringField
from wtforms import PasswordField
from wtforms.vaildators import DataRequired

class RegisterForm(FlaskForm): 
    userid = StringField('userid', validators=[DataRequired()])
    username= StringField('username', validators=[DataRequired()])
    password = PasswordField('password', validators=[DataRequired()])
```

1번째 줄에 page들을 가져올거에요. 우리가 만들 FlaskForm을 상속 받아야 하기에 Flaskform을 임포트 해줍니다.   
  
2번째 줄의 wtforms안에서 사용할 필드를 가져올 수 있어요.\(여기선 StringField\)  
  
3번째 줄에는 비밀번호도 사용해야하기에 PasswordField도 임포트해줍니다.   
  
1,2,3번줄을 왜 넣냐고요? 회원가입시 아이디, 비밀번호를 작성하기 때문입니다.

4번째 줄에 validators를 가져와서 DataRequired를 임포트해줘요. 데이터의 유효성을 검사하기 위해서에요.   
  
6번째 줄부터 Form을 만들도록 할게요. 회원가입 from이니 이름을 알기 쉽게 RegisterForm이라고 클래스명을 만들었어요. 그리고 FlaskForm을 상송 받아요.   
그리고  내가 입력 받고자 하는 필드들을 이 클래스 안에서 만들어 주면 되요. 

마치 models.py를 만들었던과 유사한 걸 알 수 있어요.   
일단 기존의 form 배치구조나 작용 순서를 인지하고 작성할 게요.   
  
7째 줄에 userid가 먼저 오게되요. 그리고 우리가 사용할 validators를 리스트 형식으로 넣어주면 되요.   
8째 줄에 username, password 각각 아래 줄에 작성할게요.   
일단 forms.py파일은 다 만들었어요.   


### 활용

forms.py를 만들었다면 이제 맘껏 활개치개 만들어 줘야해요.   
그 전에 설정해야 할 부분이 있으니 그것부터 진행할게요.   


### 설정하기 

forms.py를 굴리기 전에 CSRF를 설정해줄거에요. 일단 CSRF가 무엇인지 간단하게 말하자면 **사이트간 요청위조**라고 해요. 

> 사이트 간 요청 위조는 특정 [웹사이트](http://wiki.hash.kr/index.php/%EC%9B%B9%EC%82%AC%EC%9D%B4%ED%8A%B8)가 사용자의 웹 [브라우저](http://wiki.hash.kr/index.php/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80)를 신용하는 상태를 노린 것이다. 일단 사용자가 웹사이트에 로그인한 상태에서 사이트 간 요청 위조 공격 코드가 삽입된 페이지를 열면, 공격 대상이 되는 웹사이트는 위조된 공격 명령이 믿을 수 있는 사용자로부터 발송된 것으로 판단하게 되어 공격에 노출된다. 사이트 간 요청 위조는 개별 링크와 폼이 사용자 별로 예측 가능한 토큰을 사용할 때 발생하는데, 예측 불가능한 토큰이 있다면 공격자는 요청 메시지를 변조할 수 없지만 예측 가능한 토큰이 있다면 공격자는 요청 메시지를 변조할 수 있다. 인증이나 세션, 쿠키 등 모든 웹사이트에서 인증된 사용자가 보내는 데이터는 정상적인 경로를 통한 파라미터 요청으로 판단한다. 즉, 정상적인 요청과 비 정상적인 요청을 구분하지 못한다.  
>   
> 예를들면 실제로 내가 A사이트에서 요청을 하고  있지만 B사이트에 있으면서 A사이트에 있는 척 하면서 서버에 요청을 할 수 있게 되요.   
> 즉 위조를 하게 되는거에요.   
>   
> 이를 방지하기 위해 암호화된 해쉬키를 넣어 내가 직접 만든 웹사이트 안에서 만든 요청인지 아닌지를 판단하게 하는 방법이 csrf보호법이에
>
> 출처: 구글

###  

  


