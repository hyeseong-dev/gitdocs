# 04 View - Register

회원가입을 만들어 보도록 할게요.   


## 들어가기 앞서

### Bootstrap 

### Base 템플릿 생성 

### Index 템플릿 생성 



{% tabs %}
{% tab title="fcuser/views.py" %}
```text
from django.shrtcut import render

def index(request):
    return render(request, 'index.html')
```

사실 모델과 상관 없는 별도의 app을 만들기도 해요. 지금은 일단 fcuser앱 안에 생성하도록 할게요.   


index함수가 호출될때 request 매개변수가 들어가고 render\(\)메서드를 통해서 request 요청이 index.html 템플릿으로 전달되게 되요. 
{% endtab %}
{% endtabs %}



### 템플릿 생성 

#### 1\) base.html

> fcuser앱 안에 templates 폴더를 만들어 주세요. 영어 스펠링 단 한글자도 안틀리게 주의하세요.   
> templates 1\) base.html  2\) index.html 3\)register.html을 일단 생성해 볼게요.

```text
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css" integrity="sha384-9aIt2nRpC12Uk9gS9baDl411NQApFmC26EwAOH8WgZl5MYYxFfc+NcPb1dKGj7Sk" crossorigin="anonymous">
  <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
  <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js" integrity="sha384-OgVRvuATP1z7JjHLkuOU7Xw704+h835Lr+6QL9UvYjZE3Ipu6Tp75j7Bh/kR0JKI" crossorigin="anonymous"></script>

  <title>홈페이지</title>

</head>
<body>
  <div class="container">
    {% block contents %}
    {% endblock %}
  </div>
</body>
</html>
```

#### bootstrap 적

5~9번째줄은 bootstrap 홈페이지에서 css와 js를 복붙해주세요. 

#### 템플릿 문법 적용 

> ```text
>     {% block contents %}
>     {% endblock %}
> ```

#### 2\) index.html 

```text
{% extends 'base.html' %}
{% block contents %}
Hellow world
{% endblock %}
```

임시로 화면이 정상 출력되는지 hello world 문자를 입력할게요. 

### URL 연결 

#### 1\) fc\_django/fc\_django/urls.py

```text
from django.contrib import admin 
from django.urls import path 
from fcuser.views import index

urlpatterns = [
    path('admin', admin.site.urls),
    path('/', index),
]
```

웹브라우저의 홈페이지를 출력하면 이전에 생성한 index.html페이지를 출력하기 위해서 '/' 슬래쉬 하나만 입력하고 -&gt; fcuser앱안의 view로 넘어가서 index 메서드를 호출하고 -&gt; templates안의 index.html을 다시 찾아서 요청에 대한 응답으로 돌려주게되요. 

## 회원가입 페이지 

### 1\) form 생성 

{% tabs %}
{% tab title="fcuser/forms.py" %}
```text
from django import forms

class RegisterForm(form.Form):
    email = forms.EmailField(
        error_message={
            'required' : '이메일을 입력해주세요'
        }, 
    max_length=64, label='이메일'
    )
    password= forms.CharField(
        error_message={
            'required' : '비밀번호 입력해주세요'
        },
        widget=forms.PasswordInput, label='비밀번호'
    )
    re-password= forms.CharField(
        error_message={
            'required' : '비밀번호 입력해주세요'
        },
        widget=forms.PasswordInput, label='비밀번호 확인'
    )
```

1번째 줄은 django 라이브러리 안의 form 메서드를 임포트할게요. 
{% endtab %}
{% endtabs %}

### 2\) view작성 

#### fcuser/views.py

{% tabs %}
{% tab title="fcuser/views.py" %}
```text
from django.shortcuts import render
from django.views.generic.edit import FormView
from .forms import RegisterForm

def index(request):
    return render(request, 'index.html')
    
class registerview(FormView):
    template_name = 'register.html'
```

아래 7번째줄에 class를 만들었는데요. 

이전 회원가입시 만들었던 forms.py 기억하나요? 유효성 검사, session, 회원가입 버튼을 누르면 다른 페이지로 이동하는등의 로직을 작성 했어요.   
우선 FormView를 상속 받고 변수 이름을 작성해 볼게요.   
template\_name을 만들건데, 그렇다면 템플릿도 만들어야 겠조? 

그리고 form\_class변수에 앱의 forms.py의 RegisterForm 값을 복사해야해요.\(그럴려면 임포트해야겠조? 3번째줄에 임포트 할게요.\)  
  
그리고 url에 지정해둘게요.
{% endtab %}

{% tab title="fcuser/templates/register.html" %}
```
{% extends "base.html" %}
{% block contents %}
Register
{% endblock %}
```

#### register.html 

base.html을 상속 받고 템플릿 문법을 써서 가볍게 만들게요. 내용은 테스트로 register라는 문자만 넣고 임시로 확인해볼게요. 
{% endtab %}

{% tab title="fc\_django/urls.py" %}
```text
from django.contrib import admin 
from django.urls import path
from fcuser.views import index, RegisterView

urlpatterns = [
    path('admin', admin.site.urls),
    path('',index),
    path('register', RegisterView.as_view() ),
]
```

register url을 등록하고 fcuser앱 views의 RegisterView클래스를 추가해주면 되요. 

> 단, 클래스를 사용 할 경우 .as\_view\(\)라는 함수를 마지막에 붙여야하는점 유의하세요.
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/image%20%28340%29.png)

 이제 템플릿이 정상 출력되는 것을 확인했습니다. 하지만 form을 입혀야해요. 회원가입 페이지에 form이 없으면 안되겠조? 

### form 입히기 

템플릿에 form을 출력해보도록 할게요.  {{ form }}

{% tabs %}
{% tab title="fcuser/templates/register.html" %}
```
{% extends "base.html" %}
{% block contents %}
Register {{ form }}
{% endblock %}
```
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/image%20%28337%29.png)

꼴랑 괄호 몇개랑 단어 하나 썻는데 form이 출력된게 보이네요.   
미리 준비된 템플릿을 적용할게요. 단 문자만 바꿔주세요. 

```text
{% extends "base.html" %}
{% block contents %}
<div class="row mt-5">
  <div class="col-12 text-center">
    <h1>회원가입</h1>   
  </div>
</div>
  <div class="row mt-5">
   <div class="col-12">
    {{ error }}
   </div>
  </div>
  <div class="row mt-5">
    <div class="col-12">
      <form method="POST" action=".">
        {% csrf_token %}
        {% for field in form %}
        <div class="form-group">
          <label for="{{ field.id_for_label }}">{{ field.label }}</label>
          <input type="{{ field.field.widget.input_type }}" class="form-control" id="{{ field.id_for_label }}" 
          placeholder="{{ field.label }}" name="{{ field.name }}" />
        </div>
        {% if field.errors %}
        <span style="color: red">{{ field.errors }}</span>
        {% endif %}
        {% endfor %}
        <button type="submit" class="btn btn-primary">등록</button>
      </form>
  </div>
</div>
{% endblock %}
```

![](../.gitbook/assets/image%20%28335%29.png)

출력 결과 잘 나오는걸 확인 할 수 있네요. 

#### form 개선과 에러메시지 정상 출력

현재 validation이 없는데 추가 작성하도록 할게요.  

{% tabs %}
{% tab title="fcuser/forms.py" %}
```text
from django import forms


class RegisterForm(forms.Form):
  email = forms.EmailField(
      error_messages={
        'required': '이메일을 입력해주세요.'
      },
      max_length = 64, label='이메일'
  )
  password = forms.CharField(
      error_messages={
        'required': '비밀번호를 입력해주세요.'
      },
      widget=forms.PasswordInput, label='비밀번호'
  )
  re_password = forms.CharField(
      error_messages={
        'required': '비밀번호를 입력해주세요.'
      },
      widget=forms.PasswordInput, label='비밀번호 확인'
  )
    def clean(self):
      cleaned_data = super.clean()
      password = cleaned_data.get('password')
      re_password = cleaned_data.get('re_password')
      
      if password and re_password:
        if password != re_password:
          self.add_error('password', '비밀번호가 서로 다릅니다')
          self.add_error('re_password', '비밀번호가 서로 다릅니다.)
```

비밀번호 일치여부를 확인하는 로직부터 먼저 clean메서드를 생성해서 구성해보도록 할게요. 
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/image%20%28339%29.png)



{% tabs %}
{% tab title="fcuser/views.py" %}
```text
from django.shortcuts import render
from django.views.generic.edit import FormView
from .forms import RegisterForm

def index(request):
    return render(request, 'index.html')
    
class registerview(FormView):
    template_name = 'register.html'
    success_url = '/'
```

success\_url 변수를 통해서 회원가입이 성공적으로 되면 이후 자동으로 url을 index화면으로 넘겨주게 설정 할 수 있어요. 
{% endtab %}

{% tab title="forms.py" %}
```text
from django import forms


class RegisterForm(forms.Form):
  email = forms.EmailField(
      error_messages={
        'required': '이메일을 입력해주세요.'
      },
      max_length = 64, label='이메일'
  )
  password = forms.CharField(
      error_messages={
        'required': '비밀번호를 입력해주세요.'
      },
      widget=forms.PasswordInput, label='비밀번호'
  )
  re_password = forms.CharField(
      error_messages={
        'required': '비밀번호를 입력해주세요.'
      },
      widget=forms.PasswordInput, label='비밀번호 확인'
  )
    def clean(self):
      cleaned_data = super.clean()
      password = cleaned_data.get('password')
      re_password = cleaned_data.get('re_password')
      
      if password and re_password:
        if password != re_password:
          self.add_error('password', '비밀번호가 서로 다릅니다')
          self.add_error('re_password', '비밀번호가 서로 다릅니다.)
        else: 
          fcuser = Fcuser(
            email = email, 
            password=password
          )
          fcuser.save()
```

28번째줄에서는 비밀번호 입력란과 비밀번호 확인 입력란에 user가 입력했는지 확인하고 29번째 줄에는 두개의 입력란에 입력된값이 일치한지 확인하게 되요. 만약 일치하게 되면 회원가입 버튼 클릭시 db에 저장해야하므로 32번째 줄에 else 조건을 쓰고 아래에 Fcuser\(\)클래스에 각각 email=email, password=password 매개변수를 넣고 fcuser의 객체를 저장하는것으로 마무리합니다. 
{% endtab %}
{% endtabs %}



