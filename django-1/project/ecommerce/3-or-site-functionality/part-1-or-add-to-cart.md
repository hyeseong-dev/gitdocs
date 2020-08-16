# Part 1 \| Add to Cart

## 들어가기 앞서 

유저 기능중 하나인 add to cart기능과 update cart 그리고 checkout 기능을 구현해볼게요. 

비로그인 유저의 위 3가지 기능은 다음 번에 다루도록 할게요.   


### Javascript 

frontend기능을 다루고 이 정보를 backend로 보내기 위해서 javascript를 사용할게요. 

## Step  1 \| cart.js

hompage에서 cart 기능은 기본적으로 상품을 더하거나 뺄수 있게되요. 상품을 더하면 숫자가 늘어나고 빼게되면 숫자가 줄어들면서 말이조.

그래서 파일 하나를 생성해서 main template에 연결하고 이를 모든 페이지에서 사용가능하도록 코딩해볼게요. 

### js 폴더 + 파일

js폴더와 파일을 아래와 같이 만들어 주세요.  


![](../../../../.gitbook/assets/image%20%28416%29.png)

### Add JS script link to template

main.html안의 가장 아래 Bootstrap link를 걸어뒀던 곳에 아래 그림과 같이 script tag를 걸어둬서 연동 할 수 있도록 할게요. 

![](../../../../.gitbook/assets/image%20%28458%29.png)

### Confirm Link Connection

 제대로 연결 되었는지 확인하기 위해서 우선 cart.js 파일 안에 console.log\('Hello world!'\)를 입력하고 저장해주세요.   
그리고 서버를 돌린다 크롬 개발자 도구를 열어서 아래 그림과 같이 모든 페이지가 동일하게 hello world가 나타나는지 확인해주세요.

![](../../../../.gitbook/assets/image%20%28426%29.png)

## Step 2 \| Add Event Handlers

![](../../../../.gitbook/assets/image%20%28457%29.png)

store.html페이지에 Add to Cart 버튼에 event handler를 더해 볼게요. 

### Add Class to Buttons

"Add to Cart"가 있는 button태그의 class의 마지막에 update-cart를 추가해 줄게요.   


![](../../../../.gitbook/assets/image%20%28435%29.png)

### Product ID & Action

![](../../../../.gitbook/assets/image%20%28418%29.png)

### Add Event

cart.js 파일을 아래오 같이 작성해주세요.

![](../../../../.gitbook/assets/image%20%28434%29.png)

## Step 3 \| Use Type Logic

기본적으로 로그인 유저와 비로그인 유저에 대한 logic을 만들건데요.  
일단 로그인 유저에 대한 로직을 만들거에요. 

### Set/Query user \(main.html\)

먼저 쿼리를 통해서 로그인 상태를 확인 할거에요.  main.html header tag내에서 script tag를 이용해 "request.user"를  통해서 변수 user값을 만들건데요. 만약 로그인 되어 있지 않다면 "AnonymousUser"가 value값이 될거에요.

![](../../../../.gitbook/assets/image%20%28465%29.png)

### Check user status on click \(cart.js\)

cart.js 안에 if 조건문을 만들어 볼게요 그리고 유저의 로그 상태 유무에 따라 다른 두 가지 statements 역시 설정하도록 할게요.

![](../../../../.gitbook/assets/image%20%28433%29.png)

## Step 4 \| UpdateItem View

로그인 유저가 "add to cart"버튼을 클릭했을때 이 정보를 view로 전달해 볼게요.

"add" or "remove"예 따라서 로직을 만들어 볼게요. 

### Create View

먼저 views.py파일 안에 로직을 만들어 볼게요. 그리고 return은 JsonResopnse로 돌려주도록 할게요. 

![](../../../../.gitbook/assets/image%20%28444%29.png)

### URL path

urls.py 파일 안에 path를 만들고 view연결을 해보도록 할게요.

![](../../../../.gitbook/assets/image%20%28446%29.png)

## Step 5 \| updateUserOrder\(\)

이제 'add"버튼을 누르면 로그인, 비로그인 유저를 구분하는 이벤트 핸들러가 있고 그리고 로그인 유저라면 해당 정보를 데이터 전송을 위한 views.url도 있어요. 

그리고 만 로그인 유저가 함수를 만들게 되면 POST 요청 함수를 가져서 view로 처리 하도록 해볼게요. 

조건문 else updateUserOrder\(\)함수를 작성해주세요.  
그리고 그 아래에 updateUserOrder\(\)함수를 정의하도록 할게요.

![](../../../../.gitbook/assets/image%20%28460%29.png)

### Send POST request to View

정의된 함수 내부를 보면 url 변수와 fetch api가 보이는데요. 이 fetch api는 requst POST 역할을 하게되요. 즉 backend로 data를 보내는 중요한 역할을 갖고 있어요.

![](../../../../.gitbook/assets/image%20%28430%29.png)

이 data를 보내기 전에 csrftoken을 먼저 처리해주어야해요. 그렇지 않으면 이렇게 아래 오류코드가 나타나요.

![](../../../../.gitbook/assets/image%20%28437%29.png)

## Step 6 \| CSRF Token

기본적으로 {% csrf\_token %} 형태로 csrf token을 통상적으로 사용했는데요. 현재 우리는 자바스크립트를 사용하기에 통상적 방법으로는 안되요.   


하지만 장고 공식문서에서 아래와 같이 통상적 방법 이외로 csrf token을 만들수 있게 했어요.

### Create Token

아래 코드를 main.html파일의 script 태그의 user 변 코드에 아래 붙여 넣도록 할게요.

![](../../../../.gitbook/assets/image%20%28447%29.png)



### Send Token with POST request

이제 "csrftoken" 변수를 만들었어요 이를 fetch\(\) call 함수 안에 집어 넣을게요.

그리고 cart에 바로 즉각적인 변화가 나타날 거에요.   
post data를 보낼때 cart 이미지 숫자가 변화되는게 정상적으로 나타나야해요.

![](../../../../.gitbook/assets/image%20%28448%29.png)

## Step 7 \| UpdateItem view logic

data를 view에 보내게 될때 fetch call에 있는 productid와 action을 처리하도록 할게요. 

json을 import해주세요.   
아래 json정보를 불러온 다음 data 변수에 담아 python dictionary로 해당 data값에 접근하도록 할게요. 그리고 이상 유무 확인을 위해 print로 productId와 action 변수를 출력 하도록 할게요.

![](../../../../.gitbook/assets/image%20%28454%29.png)

![](../../../../.gitbook/assets/image%20%28424%29.png)

### Create OR Update Order & OrderItem

requst.user.customer를 통해서 customer 변수에 담고 productId를 인자로 받아서 product 쿼리를 하고 get\_or\_create메서드를 이용해서 complete가 False인 경우 해당 제품이 db에 없다는 의미하는 만큼 order변수를 성하게 되요.   
이후 orderItem, created 변수를 만들기 위해서 또 get\_or\_create\(\)함수를 사용하는데 이때 실제적인 로직이 마무리 되게 되요. 

![](../../../../.gitbook/assets/image%20%28449%29.png)

### Action Logic

마지막으로 order에서 item을 제거하는 로직을 몇가지 더해볼게요.

필수적으로 action에 근거하여 quantity update가 필수적인데요 만약 수량이 0아래로 떨어질경우 operitem을 cart에서 제거해야해요. 

![](../../../../.gitbook/assets/image%20%28461%29.png)

## Step 8 \| Cart Total

더하거나 뺄때 카트 icon에 cart total을 더해보도록 할게요. 

![](../../../../.gitbook/assets/image%20%28443%29.png)

### User data in store view

store view에 if 조건문을 더해서 쿼리 작업을 해보도록 할게요. 

![](../../../../.gitbook/assets/image%20%28456%29.png)

///file: main.html 

{{cartItems}}을 넣어주세요.

![](../../../../.gitbook/assets/image%20%28413%29.png)

이제 정상적으로 홈페이지로 가보면 cart 아이콘에 carttotal이 정상적으로 수량 표기가 나타날거에요.

### cart view 작성

![](../../../../.gitbook/assets/image%20%28468%29.png)

### checkout view 작성

![](../../../../.gitbook/assets/image%20%28428%29.png)

