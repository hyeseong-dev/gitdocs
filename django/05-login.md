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
{% endtabs %}

