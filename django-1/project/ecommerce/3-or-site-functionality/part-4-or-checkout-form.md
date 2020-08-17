# Part 4 \| Checkout Form

## Step 1 \| Hide Form or Fields

![](../../../../.gitbook/assets/image%20%28456%29.png)

### Page Logic 

1. 로그인 유저                                                         --&gt; Hide Name and Email Fields
2. 로그인 유저 & 배송이 불필요한 Item\(digital\) --&gt; Hide form & Open Payment option

로그인 유저의 경우 이름과 이메일 작성이 불필요합니다. 이미 DB에 저장 되어 있기 때문이조. 



## Step 2 \| Form Data

### what data are we sending:

payment button이 눌러질 경우 3가지가 backend 작업으로 전달 되게 되요. 

1. Cart Total
2. User Information\(If user is NOT logged in\)
3. Shipping Address\(If item in order needs shipping\)

### Cart total

![](../../../../.gitbook/assets/image%20%28535%29.png)

### User & Shipping Data

"user"와 "shipping"을 2 개의 개별 자바 스크립트 객체\(userFormData, shippingInfo\)로 보내서 백엔드에서 별도로 액세스 할 수 있도록 할게요.   
일단 우리가 만든 전역변수 total을 userFormData 객 내부 'total'의 값으로 설정할게요.

![](../../../../.gitbook/assets/image%20%28437%29.png)

shipping != False가 결국 True가 된다는 건 address, city,state, zipcode를 입력해야하는 경우를 말해요. 

user == 'AnonymousUser'가 True인 경우는 name과 email을 작성해야하는 경우인 비 로그인 유저를 말하는거고요.

![](../../../../.gitbook/assets/image%20%28423%29.png)





