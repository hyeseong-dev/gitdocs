# Part \| 5 cartData\(\)

## 들어가기 앞서 

### Movig all cart logic utils.py

여전히 반복되는 코드들이 있어 효율성이 상대적으로 떨어지게 되네요. 

메서드 하나를 만들어서 이렇게 반복적인 코드를 대체하도록 해볼건데요.   
  
이전의 cookieCart\(\)와 동일한 역할처럼 이번에는 cartData\(\)를 만들어서 비슷한 패턴으로 작성해보도록 할게요.

![](../../../../.gitbook/assets/image%20%28460%29.png)

## Step 1 \| Create Function

### Create function

cartData\(\)를 만들어 볼게요. utils.py파일에 만들어 주세요.

![](../../../../.gitbook/assets/image%20%28538%29.png)

### Import into views.py

cookie cart처럼 이번에도 views.py 파일에 cartData를 import할게요. 

```text
from .utils import cookieCart, cartData
```



## Step 2 \| Move view logic

View에 있는 로직을 utils.py에 붙여넣어주세요.

### **Copy**

![](../../../../.gitbook/assets/image%20%28518%29.png)



**Paste**

![](../../../../.gitbook/assets/image%20%28494%29.png)

## Step 3 \| User cartData\(\) in views



![](../../../../.gitbook/assets/image%20%28470%29.png)



![](../../../../.gitbook/assets/image%20%28537%29.png)



![](../../../../.gitbook/assets/image%20%28415%29.png)

