# Part 4 \| cookieCart\(\) Function

## 들어가기 앞서 

 현재 만든 브라우저 cart cookie를 통해서 cart items\(OrderItems\)를 갖고 cart\(Order\)를 만들었는데요. 현재 약 30줄 가량 되는 코드량이에요. 문제는 여러 view에서 동일하게 적용되니 중복되는 코드가 발생하게 되요.   


### Let's make our code reusable

D.R.Y.\(Don't Repeat Yourself\)에 따라서 별도의 파일에 한개의 메소드를 만들어 호출만 하면 자동으로 실행되도록 깔끔하게 작성해볼게요.

아래 도식도를 참고해주세요.

![](../../../../.gitbook/assets/image%20%28428%29.png)

## Step 1 \| utils.py

### Create new file \| utils.py

store앱  안에 utils.py파일을 생성해주세요.   
그리고 json과 우리가 만든 model을 import 해주세요.

```text
File:// store/utils.py

import json
from .models import * 
```

### Create Function \| cookieCart\(\)

cookieCart 메서드를 만들도록 할게요.

```text
File:// store/utils.py

import json
from .models import * 

def cookieCart(request):
return {}
```

### Import cookieCart\(\) into vies.py

views파일에 위에서 만든 cookieCart\(\)를 import해주세요.

![](../../../../.gitbook/assets/image%20%28447%29.png)

## Step 2 \| Copy Cart Logic

view의 cart 메소드에 있는 로직\(else 뒷부분 부터 pass까지\)을 잘라서 utils.py의 cookieCart메서드에 붙여 넣을게요.

![](../../../../.gitbook/assets/image%20%28432%29.png)

![](../../../../.gitbook/assets/image%20%28465%29.png)

![](../../../../.gitbook/assets/image%20%28499%29.png)

## Step 3 \| User cookieCart in views

 이전에 잘라냈던 else 뒷부분에 아래와 같이 소스코드를 작성해주세요.그리고 딕셔너리 cookieData변수를 받아서 필요한 속성들을 불러와서 변수에 담아 랜더링해주면되요.

동일한 4줄의 코드를 store, cart, checkout메서드에 적용해주면 되요.

![](../../../../.gitbook/assets/image%20%28480%29.png)

![](../../../../.gitbook/assets/image%20%28451%29.png)

![](../../../../.gitbook/assets/image%20%28486%29.png)

