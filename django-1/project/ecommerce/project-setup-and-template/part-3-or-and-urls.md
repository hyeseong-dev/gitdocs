# Part 3 \| 뷰&URLs

## 들어가기 앞서

이제 앞서 만든 template을 랜더링하기 위해 views와 url paths를 작성해보도록 할게요.

## **Step 1 \| Create Views**

**3개의 뷰를 만들거에요. store, cart, checkout**

각 뷰의 내부에는 빈 딕셔너리 context 변수를 만들게요.

![](../../../../.gitbook/assets/image%20%28381%29.png)

## **Step 2 \| URLs**

**store 앱 안에 urls.py파일을 생성해주세요.** 

urlpatterns 리스트안에 빈문자열, cart, checkout을 각 만들어 줄게요.  
이후 아래 사진처럼 2번째, 3번째 인자값을 넣어주세요.

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt3/2+urls.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt3/2+urls.png)

## **Step 3 \| Base URLs Configuration**

**step2에서 만든 urls을 root디렉토리\(ecommerce 폴더안\)의 urls.py 파일을 작성해줘야해요.** 

**핵심은 include매소드를 통해서 store.urls까지 연결시켜주는거에요.**

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt3/3+urls-root.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt3/3+urls-root.png)



###  실행 

```text
python mange.py runserver
```

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt3/4+testurls.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt3/4+testurls.png)

