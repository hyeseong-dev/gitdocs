# Part \| 6 Checkout

## 들어가기 앞서

이번 파트는 2가지에 초점을 맞춰봤어요. 

1. checkout page에서 checkout이 완료되면 homepage로 redirect하여 cart에 있는 쿠키를 지워버리게 할게요.
2. data를 backend로 전달하고 customer와 order를 db에 생성하도록할게요.

## Step 1 \| Clear Cart

checkout.html에서 결제가 마무리되면 cart 딕셔너리를 빈 딕셔너리로 바꿔버릴게요. 

![](../../../../.gitbook/assets/image%20%28543%29.png)

## Step 2 \| Guest Checkout Logic

비로그인 유저가 payment button을 클릭했을때 로직 처리를 해볼게요. 지금은 로그인 유저만 처리되도록 되어있어요.

![](../../../../.gitbook/assets/image%20%28427%29.png)



### Get cookie cart

cookie cart함수를 이용해서 cart data를 만들어 보도록 할게요. items 쿼리와 실제 order를 build해보도록 할게요.  
processOrder view의 else 뒷 부분을 아래와 같이 작성해주세요.



![](../../../../.gitbook/assets/image%20%28454%29.png)

### Create customer & Order

customer 처리를 위한 get\_or\_create\(\)메서드를 사용할 거에요.

![](../../../../.gitbook/assets/image%20%28520%29.png)

### Create Items

![](../../../../.gitbook/assets/image%20%28442%29.png)

### Move actions/Fix Indentation

views.py - processOrder\(\)에서 아래 5줄의 코드뿐만 아니라 if order.shipping ==True: 부분의 마지막 zipcode 변수를 정의하는 부분까지 모두 긁어다가 마지막  화살표 방향으로 옮기도록 할게요. 이러면 로그인 유저/비로그인 유저 공통으로 적용되는 로직이 되요.

![](../../../../.gitbook/assets/image%20%28509%29.png)

![](../../../../.gitbook/assets/image%20%28444%29.png)

## Step 3 \| Create guest checkout function

비로그인 유저의 주문 로직이 views.py의 각 view에 있는 만큼 이를 효율적으로 처리하기 위해서 utils.py에 function을 만들어서 코드 효율을 갖춰보도록 할게요. 

### Create function\(utils.py\)

메서드 이름은 guestOrder로 하고 중요한게 기존의 request를 넣은것 뿐만 아니라 data 인자값도 2번째로 넣도록 할게요. 

![](../../../../.gitbook/assets/image%20%28528%29.png)

### Copy/paste 

이제 각 view에 있던 else의 공통 부분을 복사하고\(이후 지워주세요\) guestOrder\(request, data\)메소드 내부에 붙여넣어주세요.

![](../../../../.gitbook/assets/image%20%28441%29.png)



## Step 4 \| Clean up processOrder View

### Import function\(views.py\)

```text
from .utils import cookieCart, cartData, guestOrder
```

### Clean up view

기존 else에는 저렇게 빨간줄로 guestOrder\(requst, data\)를 이용해서 customer, order변수를 정의하는 한문장만 넣도록 할게요.

![](../../../../.gitbook/assets/image%20%28475%29.png)

