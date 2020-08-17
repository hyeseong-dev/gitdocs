# Part 1 \| Set Cookie's

## 들어가기 앞

쿠키를 이용해서 웹사이트를 나가고 다시 접속하더라고 카트안의 아이템들이 다시 동일하게 되도록 설정해볼게요

### Using Cookies

비로그인 유저 브라우저를 사용해서 쿠키를 만들어 볼게요.   
이후 쿠키를 만들게 되면 아래와 같이 확인 가능하게되요.  
브라우저 console 창을 열고, 그 다음 application 탭을 누른 후 Storage-&gt;Cookies에서 cart라고 적힌 쿠키를 만들게 될거에요.

![](../../../../.gitbook/assets/image%20%28530%29.png)

## Step 1 \| Create Cart

우리가 만들 웹페이지에 로그인을 했든 안했든 쿠키를 생성해보도할게요.   


main.html 파일 안에 함수를 정의하여 특정한 쿠키를 브라우저에 저장할 수 있도록 할게요.   


### Get Cookie

getCookie\(\)라는 함수를 script tag안에 만들게요. 위치는 csrf token 변를를 정의한 곳 바로 아래에 하면 되요.

![](../../../../.gitbook/assets/image%20%28459%29.png)

### Create Cookie

![](../../../../.gitbook/assets/image%20%28515%29.png)

## Step 2 \| Adding/Removing Items

post request와 items를 db에 저장 하기위한 cart.js 파일에 대해 잠깐 짚고 넘어 갈게요.   
"click"할때 if 조건문이 발동했조? 근데 로그인 유저만 처리하게 하고 비로그인 유저는 그냥 무시하도록 로직을 짜뒀어요.  

![](../../../../.gitbook/assets/image%20%28420%29.png)

### Add to cookie item function

cart.js 파일에 있는 updateUserOrder 함수 바로 아래에 addCookieItem함수를 만들도록 할게요.

![](../../../../.gitbook/assets/image%20%28513%29.png)

addCookieItem 함수는 바로 위에 있 updateUserOrder\(\) 함수의 productId, action 매개변수를 받아서 실행하게 되는데 이때 if 문안에서 처리되게 되요.

![](../../../../.gitbook/assets/image%20%28429%29.png)

### updateCookie

### Add or Increate item Quantity

action == 'add'와 동일하면 해당 아이템이 없다면 해당 item 1개를 등록하고 만약 있다면 수량을 1개 증가시키게되요.

![](../../../../.gitbook/assets/image%20%28449%29.png)

### Remove or Decrease item Quantity

이번에는 action == 'remove'에 해당 된다면 기존에 제품이 있다면 수량을 1개 줄이고 만약 0아래로 떨어지게 되면 cart에서 제품을 지워버리게 로직을 구성하게되요. 

![](../../../../.gitbook/assets/image%20%28421%29.png)

### Change cookie value in browser

main.html에서 처리했던 document.cookie = 'cart=' + JSON.stringfy\(cart\)+";domain=;path=/"

이 부분을 복사해서 if문 바로 아래에 작성할게요.

![](../../../../.gitbook/assets/image%20%28490%29.png)

