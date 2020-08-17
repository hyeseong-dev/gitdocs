# Part 4 \| User Cart

## 들어가기 앞서 

이번 페이지는 cart.html과 checkout.html페이지를 아래와 같이 각각 구현해 보도록 할게요.

![](../../../../.gitbook/assets/image%20%28477%29.png)

## Step 1 \| Add data \(Admin Panel\)

### 1. 로그인 유저 등록

유저 등록을 하도록 할게요. 

![](../../../../.gitbook/assets/image%20%28495%29.png)

### 2. Order 등록

![](https://gblobscdn.gitbook.com/assets%2F-M7Y0ZqsG2k35xf7O6P2%2F-MElRJIXg6zfBKh5ZRbp%2F-MElSGB-903jEpExBPeg%2Fimage.png?alt=media&token=12129c74-e1d0-4ce4-b51a-524f15bb80ad)

### 3. OrderItem 등

![](../../../../.gitbook/assets/image%20%28497%29.png)



## Step 2 \| Query Data\(Cart\)

뷰에서 우리는 2가지 다른 시나리오를 만들어 둬야 해요. 

#### 하 - 로그인 유저

#### 둘 - 비로그인 유

### Query User Cart

유저 account, order and cart items들이 로그인 된걸로 찾는걸 확인해볼게요. 

get\_or\_create\(\)메서드를 통해서 이를 잘 구현해 볼수 있어요. 

![](../../../../.gitbook/assets/image%20%28540%29.png)

### Create Guest Cart

비로그인 유저의 경우, 빈 리스트 변수 값을 만들어 context변수에 집어 넣어 주세요..   


![](../../../../.gitbook/assets/image%20%28489%29.png)

## Step 3 \| Render data \(cart.html\)

cart items에 대한 쿼리를 마쳤으므로 이제 rendering해보도록 할게요.  
ImageURL, Name, Price, Quantity를 for문을 돌려서 진행하게되요.  


![](../../../../.gitbook/assets/image%20%28532%29.png)

## Step 4 \| Calculating Totals

화살표 부분에 대한 데이터 처리가 여전히 부족한데요. 해볼게요. 

![](../../../../.gitbook/assets/image%20%28514%29.png)



## Step 5 \| Query Totals

property 데코레이터와 get\_total 메서드를 통해서 해당 제품 total price를 구할 수 있어요.

![](../../../../.gitbook/assets/image%20%28445%29.png)

 그리고 get\_cart\_total과 get\_cart\_items를 작성하여 cart내 제품의 총 수량과 그 금액을 구할 수 있어요.

![](../../../../.gitbook/assets/image%20%28524%29.png)

## Step 6 \| Render Totals

![](../../../../.gitbook/assets/image%20%28539%29.png)

![](../../../../.gitbook/assets/image%20%28434%29.png)

하지만 관리자 페이지에서 로그아웃하고 다시 cart로 가보면 오류가 발생하네요. 

![](../../../../.gitbook/assets/image%20%28512%29.png)

![](../../../../.gitbook/assets/image%20%28446%29.png)

## Step 7 Checkout Page Data

이제 cart.html페이지에서 랜더링 한걸 똑같이 checkout.html에도 동일하게 적용 시켜 볼게요.

**1 - cart view 로직을 복사해서 동일하게 checkout view 로직에 붙여넣어주세요.**

\*\*\*\*

![](../../../../.gitbook/assets/image%20%28487%29.png)

2 - checkout.html 템플릿에 랜더링하기   


![](../../../../.gitbook/assets/image%20%28503%29.png)























