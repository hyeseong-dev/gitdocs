# 03 Admin Setup

관리자 웹 페이지에 정상적으로 앱의 모습을 출력하기 위해선 각 앱에 있는 admin.py 파일을 수정해야해요. 

실제 관리자 화면에서 무언가를 하는 경우는 드물지만 현재 실습을 하는 입장에서 TEST용도로 값을 넣고 삭제하는 기능을 위해서 admin.py 파일을 작성해 볼게요. 

## 앱별 Admin.py 파일 작성 

{% tabs %}
{% tab title="fcuser/admin.py" %}
```text
from django.contrib import admin 
from .models import Fcuser 

class FcuserAdmin(admin.ModelAdmin):
    list_display=('email',)
    
admin.site.register(Fcuser, FcuserAdmin)
```

> 주의! list\_display =\('값', \)  우항에 , \(콤마\)가 찍혀있는데 없으면 튜플로 인식되지 않아요.

admin.site.register\(클래스명, 바로위 클래스\) 으로 작성해줘요. 
{% endtab %}

{% tab title="product/admin.py" %}


```text
from django.contrib import admin 
from .models import Product 

class ProductAdmin(admin.ModelAdmin):
    list_display=('email',)
    
admin.site.register(Product, ProductAdmin)
```

> 주의! list\_display =\('값', \)  우항에 , \(콤마\)가 찍혀있는데 없으면 튜플로 인식되지 않아요.

admin.site.register\(클래스명, 바로위 클래스명\) 으로 작성해줘요.
{% endtab %}

{% tab title="order/admin.py" %}


```text
from django.contrib import admin 
from .models import Order 

class FcuserAdmin(admin.ModelAdmin):
    list_display=('fcuser','product')
    
admin.site.register(Order, OrderAdmin)
```

> order앱의 admin.py파일의 list\_display에서는 출력하고자 하는 fcuser와 product를 입력할게요.

admin.site.register\(클래스명,  바로위 클래스\) 으로 작성해줘요.
{% endtab %}
{% endtabs %}

## 관리자 페이지에서 확인\(model\)

이제까지 작성한 앱별 모델 파일과 admin파일이 어떻게 관리자 페이지에 출력되는지 확인 하려면 관리자 계정이 있어야 해요. 

### 관리자 계정 생성 

```text
$ ./manage.py createsuperuser
$ 아이디 : 
$ 이메일 : 
$ 비밀번호 : 
$ 비밀번호 확인 : 
$ ./manage.py runserver
```

![&#xAD00;&#xB9AC;&#xC790; &#xD398;&#xC774;&#xC9C0; &#xD654;&#xBA74;](../.gitbook/assets/image%20%28333%29.png)

verbose\_name 옵션이 잘 적용된게 보이네요. 



## 앱에 데이터 등록 

![&#xAC12; &#xB4F1;&#xB85D; &#xBD88;&#xAC00; ](../.gitbook/assets/image%20%28334%29.png)

현재 주문 앱에 상ㅇ자와 상품 등록이 정상적으로 불가능한 상태에요. 개선해 볼게요. 

각 모델을 문자열로 변환 했을때 표시하는 함수를  만들어 볼게요. 



{% tabs %}
{% tab title="product/models.py" %}
```text
...
    def __str__(self):
        return self.name
...
```

각 앱의 모델안에다가 \_\_str\_\_메서드를 넣어 객체를 문자로 표현할 수 있게 만들어 주세요. 

order앱의 Order클래스 안의 \_\_str\_\_메소드의 return 부분만 그냥 빈걸로 두세요.
{% endtab %}

{% tab title="fcuser/models.py" %}
```
...
        def __str__(self):
                return self.email
...
```
{% endtab %}

{% tab title="order/models.py" %}
```
...
                def __str__(self):
                                return str(self.fcuser) + ' ' + str(self.product)
...
```

str\(self.fcuser\) + ' ' + str\(self.product\) 를 작성해서 return할게요. 지금은 바로 확인되지 않아요.
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="fcuser/models.py" %}
```text
from django.db import models

class Order(models.Model):
    fcuser = models.ForeginKey('fcuser.Fcuser', on_delete=models.CASCADE, verbose_name='사용자')
    product= models.ForeignKey('product.Product', on_delete=models.CASCADE, verbose_name='상품')
    quantity = models.IntegerField(verbose_name='수량')
    register_dtate = models.DateTimeField(auto_now_add=True, verbose_name='등록날짜')
    
    def __str__(self):
        return 
    class Meta:
        db_table = 'fastcampus_order'
        verbose_name = '주문'
        verbose_name_plural = '주문'
```

> 주의! list\_display =\('값', \)  우항에 , \(콤마\)가 찍혀있는데 없으면 튜플로 인식되지 않아요.

admin.site.register\(클래스명, 바로위 클래스\) 으로 작성해줘요. 
{% endtab %}

{% tab title="product/models.py" %}


```text
from django.db import models

class Order(models.Model):
    name = models.CharField(max_length=256, verbose_name='상품명')
    price = models.IntegerField(verbose_name='상품가')
    description= models.TextField(verbose_name='상품설명')
    stock= models.IntegerField(verbose_name='재')
    register_dtate = models.DateTimeField(auto_now_add=True, verbose_name='등록날짜')
    
    def __str__(self):
        return self.name
        
    class Meta:
        db_table = 'fastcampus_product'
        verbose_name = '상품'
        verbose_name_plural = '상'
```

> 주의! list\_display =\('값', \)  우항에 , \(콤마\)가 찍혀있는데 없으면 튜플로 인식되지 않아요.

admin.site.register\(클래스명, 바로위 클래스명\) 으로 작성해줘요.
{% endtab %}

{% tab title="order/models.py" %}
```text
from django.db import models

class Order(models.Model):
    fcuser = models.ForeginKey('fcuser.Fcuser', on_delete=models.CASCADE, verbose_name='사용자')
    product= models.ForeignKey('product.Product', on_delete=models.CASCADE, verbose_name='상품')
    quantity = models.IntegerField(verbose_name='수량')
    register_dtate = models.DateTimeField(auto_now_add=True, verbose_name='등록날짜')
    
    def __str__(self):
        return 
    class Meta:
        db_table = 'fastcampus_order'
        verbose_name = '주문'
        verbose_name_plural = '주문'
```

> order앱의 admin.py파일의 list\_display에서는 출력하고자 하는 fcuser와 product를 입력할게요.

admin.site.register\(클래스명,  바로위 클래스\) 으로 작성해줘요.
{% endtab %}
{% endtabs %}

![](../.gitbook/assets/image%20%28336%29.png)



