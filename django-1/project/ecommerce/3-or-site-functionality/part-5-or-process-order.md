# Part 5 \| Process Order

## Step 1 \| Process Order View/url

view와 url을 만들어 볼게요.

### Create View

![](../../../../.gitbook/assets/image%20%28485%29.png)

### URL Path

![](../../../../.gitbook/assets/image%20%28413%29.png)

## Step 2 \| Send POST Data

이전 작업에서 url과 fetch\(\) API작업했던것과 비슷한 방식으로 코딩 작업이 이루어 질거에요. 

![](../../../../.gitbook/assets/image%20%28501%29.png)

이렇게 작성하고 결제 진행까지 마무리 하면 최종적으로 다시 화면이 homepage로 넘어가게 되요.

## Step 3 \| Transacion ID

### Import Date Time\(views.py\)

datetime 임포트할게요.

![](../../../../.gitbook/assets/image%20%28473%29.png)

### Set Transaction ID variable

![](../../../../.gitbook/assets/image%20%28511%29.png)

윗 코드를 일단 작성했다면 아래와 같이 추가 작성을 해주세요.  
if, else 조건문으로 로그인 유저와 비로그인 유저를 구분하여 로직을 구성했어요.



## Step 4 \| Set Data

post request를 통해서 data parsing을 할데요. 만약 로그인 유저의 경우 데이터를 query/create 하도록 할게요\(비로그인 유저는 다음에 다루도록 할게요.\)

```text
def processOrder(request):
    transaction_id = datetime.now().timestamp()
    data = json.loads(request.body)
    
    if request.user.is_authenticated:
        customer = request.user.customer
        order, created = Order.objects.get_or_create(customer=customer, complete=False)
        total = float(data['form']['total'])
        order.transaction_id = transaction_id
    else:
        print('User is not logged in..')
    return JsonResponse('Payment complete!, safe=False)
    
```

## Step 5 \| Confirm Total

![](../../../../.gitbook/assets/image%20%28466%29.png)

cart\_total과 total이 맞는지 안맞는지 비교하기 위해 if문을 사용하고 만약 맞다면 주문을 db에 저장하게 되요.

## Step 6 \| Shipping Logic

아래 처럼 코드를 작성했다면 이제 로그인 유저가 결제하는 로직 처리는 거진 다 끝났어요.

![](../../../../.gitbook/assets/image%20%28416%29.png)





