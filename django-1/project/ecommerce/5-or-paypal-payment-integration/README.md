# 5 \| PayPal Payment Integration

## 들어가기 앞서

기존 결제 버튼을 아래와 같이 깔끔하게 PayPal에서 제공하는 버튼들로 꾸며볼게요.

![](../../../../.gitbook/assets/image%20%28574%29.png)



## 

아래 웹사이트에서 해당 template을 가져오면되요.

![](../../../../.gitbook/assets/image%20%28554%29.png)

### Client Side integration Vs Server side integration

파이썬과 papal API를 사용하는 Server side 방식과 client side방식! 이 2가지가 있어요. 

여기서는 front end 처리 방식을 사용하는 client side를 사용 하도록 해볼게요. 결제가 되면 확인 과정을 backend로 전달되고 order status도 변하게 되요.  


### Paypay 작동 순서 

1. 웹페이지에 PayPal Smart Payment Buttons 을 추가
2. 구매자가 버튼 클릭
3. 버튼에서 결제를 위해 PayPal Orders API를 호출
4. 버튼에서 PayPal Checkout experience를 실행
5. 구매자는 결제 승인
6. 버튼에서 결제를 마무리하기 위해 PayPal Orders API를 호출
7. 바이어는 결제가 된것을 확인 하게됨.  

![](../../../../.gitbook/assets/image%20%28556%29.png)

### Sandbox Account

우선 sandbox 계정을 통해서 모든 과정을 진행할게요. 그리고 나서 최종적인 작업이 되면 실제 paypal account의 clinet id를 통해서 결제 처리가 이행 될 수 있도록 할 수 있어요.

![](../../../../.gitbook/assets/image%20%28549%29.png)

