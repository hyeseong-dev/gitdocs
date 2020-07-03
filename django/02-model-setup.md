# 02 Model Setup

3개의 앱중 우선 사용자 관련 앱, fcuser의 모델부터 우선 만들어 볼게요. 

### fcuser 앱 model 작성 

{% tabs %}
{% tab title="fcuser/models.py " %}
```text
from django.db import models

class Fcuser(models.Model):
    email = models.EmailField(verbose_name='이메일')
    password = models.CharField(max_lengh=64, verbose_name='비밀번')
    register_date = models.DateTimeField(auto_now_add=True, verbose_name='등록날')

```

1\) verbose\_name은 관리자 화면에서 출력되는 테이블의 컬럼을 개발자가 지정한 이름으로 출력해줘요.

2\) auto\_now\_add 옵션은 등록시 날짜를 자동으로 생성해줘요.
{% endtab %}
{% endtabs %}

### product 앱 model 작성

{% tabs %}
{% tab title="product/models.py " %}
```text
rom django.db import models

class product(models.Model):
    name = models.EmailField(max_lengh=256,verbose_name='상품')
    price = models.IntegerField(max_lengh=64, verbose_name='상품가')
    description = models.TextField( verbose_name='상품설명')
    stock = models.IntegerField(verbose_name='제고')
    registered_date = models.DateTimeField(auto_now_add=True, verbose_name='등록날짜')


```

1\) TextField\(\) 클래스는 max\_length 옵션을 필수로 입력할 필요가 없어요. 
{% endtab %}
{% endtabs %}



### order 앱 model 작성

{% tabs %}
{% tab title="order/models.py " %}
```text
rom django.db import models

class order(models.Model):
    fcuser = models.ForeignKey('fcuser.Fcuser', on_delete=models.CASCADE,verbose_name='사용')
    product = models.ForeignKey('product.Product', on_delete=models.CASCADE,verbose_name='상')
    quantity = models.IntegerField( verbose_name='수')
    registered_date = models.DateTimeField(auto_now_add=True, verbose_name='등록날짜')


```

1\) ForeignKey 필드 클래스는 fcuser앱의 model에 있는 Fcuser클래스를 참조하므로 'fcuser.Fcuser'라고 필수 매개변수를 지정하고 

2\) 또한 필수적으로 **on\_delete 속성이 필요해요.**   
on\_delete=models.CASCADE 라고 작성하게 되면 원래 fcuser의 값이 삭제되면 자동으로 삭제되요. 
{% endtab %}
{% endtabs %}

일단계로 모델작성은 완료되었어요. 기억날지 모르겠지만 admin에서 model사용을 편리하게 사용하기 위해 별도의 등록을 했어요. 

바로 Order, Product, Fcuser 클래스안에 Meta 클래스를 작성한거에요. 

#### Meta class

1\) order 

```text
...
상기 작성된 코드와 동
...

    class Meta: 
        db_table = 'fastcampus_order' 
        verbose_name = '주문'
        verbose_name_plural = '주문' 
```

> Meta 클래스를 정의하고 db이름과 verbose 단 복수 지정을 해주지 않으면 원하지 않는 테이블 이름과 출력이 나오게 됨.



2\) product 

```text
...
상기 작성된 코드와 동
...

    class Meta: 
        db_table = 'fastcampus_product' 
        verbose_name = '상'
        verbose_name_plural = '상' 
```



3\) fcuser 

```text
...
상기 작성된 코드와 동
...

    class Meta: 
        db_table = 'fastcampus_fcuser' 
        verbose_name = '사용'
        verbose_name_plural = '사용자' 
```

## DB 반

### 앱 등록 

3개의 앱을 settings.py에 등록 할 게요. 

```text
# settings.py

... 

INSTALLED_APPS = [
    ....., 
    .....,
    .....,
    'fcuser',
    'product',
    'order',

]


...

```

### migrate 하기 

각 앱의 model을 작성한 내용을 db파일에 적용하기 위해 장고 admin 명령어를 실행할게요. 

```text
$ python manage.py migrate
```





