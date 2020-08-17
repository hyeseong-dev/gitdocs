# Part 3 \| Build Order

## Step 1 \| Order Totals

이전 cart내에 있는 모든 품목의 수, total item 로직을 작성했다면 이번에는 값을 파악해야겠조?\(get\_cart\_total\)

### Query Product

유의 해야 할 것이 for문 cart의 i는 product id를 의미해요. 

![](../../../../.gitbook/assets/image%20%28422%29.png)

### Get and set totals

total value에 대한 setting을 했다면 이제는 product price \* quantity를 적용해서 값만 구하면 되요.   
total\(+=\) to order\['get\_cart\_total'\]



## Step 2 \| Items Queryset

![](../../../../.gitbook/assets/image%20%28493%29.png)



![](../../../../.gitbook/assets/image%20%28527%29.png)

![](../../../../.gitbook/assets/image%20%28433%29.png)

## Step 3 \| Shipping Information

현재 동일한 data가 상당히 많은 페이지에 걸쳐서 동일하게 있는데요. 몇가지 소스 코드를 수정해볼게요.   
우선 digital 제품 유무에 따른 소스 코드 작업이에요. 

![](../../../../.gitbook/assets/image%20%28414%29.png)

## Step 4 \| Product Does Not Exist

잠재적인 오류 문제가 하나 있는데요. 만약 관리자가 임의의 product를 생성했고 유저가 그 product를 카트에 추가했는데 관리자가 다시 그 product  제거했다고 해볼게요. 그럴경우 잘못된 id로 query하게 될거에요.   
그럼 당근 오류 발생할거고요.   
  
그래서 try except구문으로 오류 발생을 방지하도록 할게요.

![](../../../../.gitbook/assets/image%20%28418%29.png)

