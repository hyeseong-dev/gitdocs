# 05 Login

회원 가입을 만든것 처럼 로그인도 만들어 볼게요. 

1\) 로그인 폼, 폼뷰로 연결 

{% tabs %}
{% tab title=" fcuser/views.py " %}
```text
from django.shortcuts import render
from django.views.generic.edit import FormView
from .forms import RegisterForm
​
def index(request):
    return render(request, 'index.html')
    
class RegisterView(FormView):
    template_name = 'register.html'
    form_class = RegisterForm
    success_url = '/'

class ListView(FormView):
    template_name = 'register.html'
    form_class = ListForm
    success_url = '/'
```

RegisterView와 같이 ListView라는 클래스를 만들고 동일하게 FormView를 상속 받고 template\_name의 값은 login.html 템플릿을 받고 form\_class의 값은 LoginForm으로 바꾸도록 할게요.  
  
그리고  login.html 템플릿을 만들도록 할게요.
{% endtab %}

{% tab title="login.html" %}
```text
{% extends "base.html" %}
{% block contents %}
<div class="row mt-5">
  <div class="col-12 text-center">
    <h1>로그</h1>   
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
        <button type="submit" class="btn btn-primary">로그</button>
      </form>
  </div>
</div>
{% endblock %}
```
{% endtab %}

{% tab title="fcuser/forms.py" %}
```
from django import forms
from django.contrib.auth.hashers import check_password
from .models import Fcuser

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
            password= make_password(password)
          )
          fcuser.save()
          
          
class LoginForm(forms.Form):
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

    def clean(self):
      cleaned_data = super.clean()
      email= cleaned_data.get('eamil')
      password = cleaned_data.get('password')
      
      if email and password:
        try: 
          fcuser = Fcuser.objects.get(email=email)
        except Fcuser.DoesNotExist:
          self.add_error('eamil', '이메일이 등록되어 있지 않았습니다.')
          return 
      
        if not check_password(password, fcuser.password):
          self.add_error('password', '비밀번호가 틀렸습니다')
        else: 
          self.email = fcuser.email
           
```

로그인 화면 구현을 위한 form을 만들건데요.  이전에 만들었던 RegisterForm 클래스를 복붙하도록할게요. 

이메일과 비밀번호 클래스 변수만 필요하겠조?   
이제 사용자가 DB에 등록되어 있는지 없는지 확인해서 로그인을 할 수 있도록 해볼게요. 

54번째 줄부터 끝까지 clean 메서드로 작성해주세요. 그리고 check\_password\(\) 메서드를 임포트해서 사용할게요.  

역할은 67번쨰 줄에서 내가 첫번쨰로 입력한 password값과, 두번째 매개변수로 등록한 encoding된 값을 서로 비교해서 일치 여부를 확인시켜줘요.   
  
그런데 우리가 회원가입시 비밀번호를 hash값으로 저장하지 않았으므로 이부분을 make\_password라는 check\_password의 친구녀석을 임포트하고 적용 시켜줘야해요.  check\_password 옆에 임프토해주고 db에 비번을 저장하는 부분이 36번째줄의 우항에 make\_password\(password\)로 바꿔주세요.   
  
{% endtab %}
{% endtabs %}



#### url 연동 

{% tabs %}
{% tab title="fc\_django/urls.py" %}
```text
from django.contrib import admin 
from django.urls import path 
from fcuser.views import index, RegisterView, LoginView

urlpatterns = [
    path('admin', admin.site.urls),
    path('/', index),
    path('register/', RegisterView.as_well() ),
    path('login/', LoginView.as_well() ),
]
```
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/image%20%28341%29.png)

로그인 기능도 거의 만들었어요. 하지만 아직 세션을 안 만들었는데 마무리 해보도록 할게요. 

## session

{% tabs %}
{% tab title="fcuser/views.py" %}
```text
from django.shortcuts import render
from django.views.generic.edit import FormView
from .forms import RegisterForm
​
def index(request):
    return render(request, 'index.html')
    
class RegisterView(FormView):
    template_name = 'register.html'
    form_class = RegisterForm
    success_url = '/'

class ListView(FormView):
    template_name = 'register.html'
    form_class = ListForm
    success_url = '/'
    
    def form_valid(self, form):
        self.request.session['user'] = form.email
        return super().form_valid(form)
```

form은 완성이 되었고 이제 form에서 유효성 검사가 끝났으면 session에 저장하면 되요. 

18번째 form\_valid메서드를 생성할건데요. 유효성 검사가 끝났을때 한다는점 다시 한번 유의해주세요. 

form.email로 저장된 값을 session의 'user'키에 값으로 다시 저장 하도록 할게요.   
그리고 super\(\)메서드를 이용해서 다시 form\_valid\(form\)를 호출하도록 할게요. 
{% endtab %}
{% endtabs %}

그리고 login한 사용자일 경우에 

#### index.html 

{% tabs %}
{% tab title="index.html " %}
```text
{% extends "base.html" %}
{% block contents %}
Hello World! 
{{ email }}
{% endblock %}
```
{% endtab %}

{% tab title="fcuser/views.py" %}
```
from django.shortcuts import render
from django.views.generic.edit import FormView
from .forms import RegisterForm
​
def index(request):
    return render(request, 'index.html', {'email':request.session.get('user') } )
    
class RegisterView(FormView):
    template_name = 'register.html'
    form_class = RegisterForm
    success_url = '/'

class ListView(FormView):
    template_name = 'register.html'
    form_class = ListForm
    success_url = '/'
    
    def form_valid(self, form):
        self.request.session['user'] = form.email
        return super().form_valid(form)
```
{% endtab %}
{% endtabs %}

여기서 email값을 전달 받기 위해서는 views에서 index메서드의 return값의 render\(\)안에 dictionary를 추가해줘야해요.  그 부분이 6번쨰 줄이에요. 

