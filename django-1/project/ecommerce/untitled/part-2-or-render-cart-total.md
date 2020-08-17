# Part 2 \| Render cart Total

## 들어가기 앞서 

앞서 만든 쿠키를 front에 뿌려줄건데요. 

### Turn this

![](../../../../.gitbook/assets/image%20%28471%29.png)

### Into This

![](../../../../.gitbook/assets/image%20%28452%29.png)

## Step 1 \| Query Cart in views.py

현재까지 쿠키를 만든 작업은 프런트에서 머물러 있습니다. 백엔드\(view\)로 넘겨주기 위한 작업이 필요해요.   
  
즉 get\_cart\_total, get\_cart\_items와 연결이 필요해요.

![](../../../../.gitbook/assets/image%20%28468%29.png)

### Get Cookies in view

requst.COOKIE\['cart'\] 와 json.loads\(\)로 data parse를 할게요.   
  
view.py 에서 else 조건 다음 'cart'변수를 만들게요. 

그 이후 cart 페이지를 열어서 확인해보면 성공적으로 프린트된게 프롬프트 창\(bash\)에 찍히게 될거에요.

![](../../../../.gitbook/assets/image%20%28519%29.png)

### Cart does not exist error

그런데 만약 처음 웹사이트를 방문한 경우 오류가 발생하게 될거에요. 혹은 쿠키가 삭제된 경우도 동일한 오류가 발생하는데요. 이를 해결하도록 해볼 게요.

try except 구문으로 마지막 except 안의 cart에 빈 딕셔너리 값을 주면되요.

![](../../../../.gitbook/assets/image%20%28438%29.png)



## Step 2 \| Build Cart Total

"cart object"를 가지고 있는데요. 비로그인 유저의 cart에서 총 수량을 파악하고 이를  update하기 위해서 order objects 'get\_cart\_items'속성에 대한 작업을 해볼게요. 

이를 위해 for문을 사용하도록 할게요.

![](../../../../.gitbook/assets/image%20%28453%29.png)

![](../../../../.gitbook/assets/image%20%28542%29.png)

![](../../../../.gitbook/assets/image%20%28482%29.png)

그럼 위의 item 변수가 갖는 실제 값을 조금더 구체적으로 대입해보면 아래와 같아요. 

![](../../../../.gitbook/assets/image%20%28502%29.png)



