# Part 1 \| Add Buttons

## Step 1 \| Add Buttons



![](../../../../.gitbook/assets/image%20%28572%29.png)

### Paypal Buttons

아래 웹 사이트에서 코드를 가져오도록 할게요. 

{% embed url="https://developer.paypal.com/demo/checkout" %}

### Paypal button container

기존 결제 버튼을 comment하거나 삭제해주세요. \(이벤트 핸들러 역시 동일하게 처리해주세요.\)  
그리고 empty paypal-button-container로 div 태그를 만들도록 할게요.

![](../../../../.gitbook/assets/image%20%28547%29.png)

### Script tag

![](../../../../.gitbook/assets/image%20%28563%29.png)

그리고 아래 script tag를 작성할게요.\(위치 잘 파악하세요.\)

![](../../../../.gitbook/assets/image%20%28560%29.png)

### Add JS code

아까 만든 script tag 한줄 바로 아래에 위치해주세요.  
마지막 render쪽에 매개변수 값 보이나요?   
결제 버튼의 id 값과 동일하조? 

![](../../../../.gitbook/assets/image%20%28564%29.png)

## Step 2 \| Style Buttons

버튼 스타일링을 해볼게요.

### 'style' objects

paypa.buttons 메서드 안에다가 style속성으로 딕셔너리를 둘게요.

![](../../../../.gitbook/assets/image%20%28567%29.png)

아래 웹사이트에서 버튼을 사용자가 원하는 색상과 모양으로 customizing 할 수 있어요.

![](../../../../.gitbook/assets/image%20%28545%29.png)

우선 style의 속성의 color와 shape의 값을 각각 'blue', 'rect'로 설정해주세요

![](../../../../.gitbook/assets/image%20%28551%29.png)

그럼 색상과 모양이 파란색에 사각형 테두리로 바뀌게 될 거에요.

![](../../../../.gitbook/assets/image%20%28557%29.png)

## Step 3 \| Hide Buttons

이번 step은 옵션이에요. 버튼이 기본적으로 숨김 상태로 있다가 필요한 순간 나타나는거조. 

### Disable Credit card option

현재 버튼이 3개인데요. 그중 PayPal Credit 버튼을 없애보도록 할게요. 

![](../../../../.gitbook/assets/image%20%28562%29.png)

![](../../../../.gitbook/assets/image%20%28565%29.png)

