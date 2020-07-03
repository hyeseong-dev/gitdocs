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

### 

