# Part 1 \| Models

## 들어가기 앞서

User\(not including the built in Django User model\)모델을 제외하고 5가지 모델을 만들어 볼게요.

 [![](https://github.com/osori-magu/osori-gitdocs/raw/master/.gitbook/assets/image%20%28392%29.png)](https://github.com/osori-magu/osori-gitdocs/blob/master/.gitbook/assets/image%20%28392%29.png)

## Step 1 \| Import User Model

장고에서 기본적으로 만들어주는 모델이 있는데 이 모델을 stote/models.py 파일에 import하도록 할게요. 

```text
from django.contrib.auth.models import User
```

## Step 2 \| Customer Model

1. User - 1:1 관계를 User model과 갖게됨
2. Name - CharField
3. Email - CharField

```text
class Customer(models.Model):
	user = models.OneToOneField(User, null=True, blank=True, on_delete=models.CASCADE)
	name = models.CharField(max_length=200, null=True)
	email = models.CharField(max_length=200,null=True)

	def __str__(self):
		return self.name
```

## Step 3 \| Product, Order & OrderItem Models 

### Product Class

여기서 눈여겨 볼게 digital 클래스 변수인데요. 제품중에 배달이 필요없고 온라인에서 소비되는 제품을 말해요. 게임앱, 동영상, 온라인 컨텐츠등을 말한답니다.

```text
class Product(models.Model):
	name = models.CharField(max_length=200)
	price = models.FloatField()
	digital = models.BooleanField(default=False,null=True, blank=True)

	def __str__(self):
		return self.name

```

### Order Class

customer변수는 ForeignKey를 이용하는데요. Customer 모델과 연결하게되요.

```text
class Order(models.Model):
	customer = models.ForeignKey(Customer, on_delete=models.SET_NULL, null=True, blank=True)
	date_ordered = models.DateTimeField(auto_now_add=True)
	complete = models.BooleanField(default=False)
	transaction_id = models.CharField(max_length=100, null=True)

	def __str__(self):
		return str(self.id)
```

### OrderItem Class

quantity, 해당 item이 added된 날짜가 cart안에 더해지게 되요. 

```text
class OrderItem(models.Model):
	product = models.ForeignKey(Product, on_delete=models.SET_NULL, null=True)
	order = models.ForeignKey(Order, on_delete=models.SET_NULL, null=True)
	quantity = models.IntegerField(default=0, null=True, blank=True)
	date_added = models.DateTimeField(auto_now_add=True)

	@property
	def get_total(self):
		total = self.product.price * self.quantity
		return total
```

## Step 4 \| Shipping Model

이 모델은 Customer, Order 모델을 상속받는데요.  적어도 orderitem이 하나라도 있게될 경우 인스턴스가 만들어 지게 되요.

```text
class ShippingAddress(models.Model):
	customer = models.ForeignKey(Customer, on_delete=models.SET_NULL, null=True)
	order = models.ForeignKey(Order, on_delete=models.SET_NULL, null=True)
	address = models.CharField(max_length=200, null=False)
	city = models.CharField(max_length=200, null=False)
	state = models.CharField(max_length=200, null=False)
	zipcode = models.CharField(max_length=200, null=False)
	date_added = models.DateTimeField(auto_now_add=True)

	def __str__(self):
		return self.address
```

## Step 5 \| Migrate Database

```text
CLI

$ python manage.py makemigrations

$ python manage.py migrate
```

## Step 6 \| admin.py

관리자 페이에서 우리가 앞서 만든 모델들을  확인하기 위해선 admin.py에 모델 등록을 해주어야해요.

```text
///File: store/admin.py

from django.contrib import admin
from .models import *


admin.site.register(Customer)
admin.site.register(Product)
admin.site.register(Order)
admin.site.register(OrderItem)
admin.site.register(ShippingAddress)
```

### Create User

유저 생성을 통해서 관리자 페이지에 접속하여 모델이 잘 생성 되었는지 확인할 수 있어요.   
기본적인 CRUD 기능을 관리자 페이지에서 구현 할수도 있어요.

```text
CLI

$ python manage.py createsuperuser
```

### Create Products

관리자 페이지에서 제품 몇가지를 등록하도록 할게요. 

![](../../../../.gitbook/assets/image%20%28427%29.png)

* products \#1
  * Name : Headphones
  * Price : 179.99
  *  Digital : false



* products \#2
  * Name : Mount of Olives book
  * Price : 14.99
  *  Digital : false



* products \#3
  * Name : Project Source Code
  * Price : 19.99
  *  Digital : true



* products \#4
  * Name : Watch
  * Price : 259.00
  *  Digital : false



* products \#5
  * Name : Shoes
  * Price : 89.99
  *  Digital : false



* products \#6
  * Name : T-Shirt
  * Price : 25.99
  *  Digital : false



