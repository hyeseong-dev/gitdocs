# Part 3 \| Shipping Address

## 들어가기 앞서 

checkout page에서는 digital 아이템만 결제되는 경우와 그렇지 않은 경우 둘로 나뉘게 되는데요. digital item만 있는  경우에는 shipping information이 필요 없게 되요.  
이를 반영해서 코딩을 해보도록 하조. 

![](../../../../.gitbook/assets/image%20%28533%29.png)

## Step 1 \| Shipping Method

 우선 'Order' model에서 digital 항목이 포함 유무를 확인해주어야해요.   
이는 for문을 돌려서 digital True, False 상태를 확인 할 수  있어요.

![](../../../../.gitbook/assets/image%20%28419%29.png)

## Step 2 \| Order Shipping Status

지금 당장 view에다가 {{order.shipping}}을 template에 심으면 작동하지만   
문제는 비로그인 유저가 checkout 페이지에서 오류를 발생시키게 되요.   
이를 해결하기 위해 checkout view에 이를 위한 작업을 해볼게요.   
  
일단 order 객체 딕셔너리에 'shipping':False를 써주세요. 

![](../../../../.gitbook/assets/image%20%28440%29.png)

## Step 3 \| Hide Shipping Form

'order' 객체에서 'shipping' 상태를 가져와서 만약 shipping == false일 경우 address field를 삭제하게 만들어야해요.

![](../../../../.gitbook/assets/image%20%28483%29.png)

## Step 4 \| Payment Option

위의 주문자 정보를 입력하고 request.POST를 하기전까지 Payment Option을 hide상태로 두도록 만들어 볼게요.

![](../../../../.gitbook/assets/image%20%28467%29.png)

### Hide button & open payment option on submit

checkout 페이지에 이벤트 핸들러를 만들고 hidden처리된 부분을 js로 처리하는 로직을 만들어 볼게요. 

![](../../../../.gitbook/assets/image%20%28526%29.png)

### Add demo Payment button

fake demo payment button을 만들어 볼게요 .  
추후 paypal에서 제공하는 API로 깔끔하게 만들거에ㅛ.

![](../../../../.gitbook/assets/image%20%28462%29.png)

![](../../../../.gitbook/assets/image%20%28469%29.png)



## Step 5 \| Trigger Payment Action

이벤트 핸들러를 만들어 볼게요. 계속 checkout.html 페이지 아래 script 태그 내에서 작업 하도록 할게요.

![](../../../../.gitbook/assets/image%20%28435%29.png)

