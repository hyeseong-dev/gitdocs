# Part 3 \| Making Payments

## Step 1 \| Test Payments

personal 계정에 접속하고 그다음 checkout page의 Paypal checkout button을 눌러서 결제를 하고 이후 sandbox.paypal.com에서 확인 할수 있어요 

![](../../../../.gitbook/assets/image%20%28546%29.png)

## Step 2 \| Setting Price

현재는 $0.01만 결제되는데요. 

### Move 'total'

쿼리문을 작성해서 total 변수를 정의하도록 할게

![](../../../../.gitbook/assets/image%20%28575%29.png)

기존 0.01있던 부분을 저렇게 대채해서 작성하도록 할게요. 

![](../../../../.gitbook/assets/image%20%28571%29.png)

## Step 3 \| Process Order

아래 빨간 부분 alert\(\)메소드를 삭제해주세요.

![](../../../../.gitbook/assets/image%20%28548%29.png)

그리고 submitForData\(\)함수를 아래에 작성해주세요.

Trigger Paypal Checkout --&gt; User Makes Payment --&gt; On Payment success "submitFormdata\(\)"

![](../../../../.gitbook/assets/image%20%28553%29.png)

## Step 4 \| Live Client ID



