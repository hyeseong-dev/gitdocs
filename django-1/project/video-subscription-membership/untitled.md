# 프로젝트 개요

프로젝트를 진행하기 앞서서 무엇을 그리고 어떤 기능들이 있을지 알아 보겠습니다. 

## 들어가기

### homepage

첫 메인 화면 페이지에는 각 과정별 리스트들이 세로로 나열됩니다. 

![](../../../.gitbook/assets/image%20%28395%29.png)

 만약 Django 101 링크를 클릭하면 아래와 같이 더 세분화된 내용들이 다시 열거되요.   


![](../../../.gitbook/assets/image%20%28394%29.png)

 그리고 이 Django 101 과정은 Free course이기 때문에 클릭하면 바로 접근하고 영상 시청이 가능하게 만들어져 있어요.

![](../../../.gitbook/assets/image%20%28378%29.png)

현재 본인 계정의 Membsership 상태를 알아 보고 싶다면 Profile 페이지로 가서 확인할 수 있어요. 

![](../../../.gitbook/assets/image%20%28405%29.png)

만약 다른 유료 컨텐츠를 보고자 한다면 아래와 같이 Upgrade membership을 진행해야 합니다. 

![](../../../.gitbook/assets/image%20%28401%29.png)

Chek out memberships 버튼을 누르면 아래 화면으로 이동하게 됩니다.

![](../../../.gitbook/assets/image%20%28392%29.png)

만약 Enterprise와 Professional를 선택하면 아래 화면으로 이동하게 됩니다. 

![](../../../.gitbook/assets/image%20%28404%29.png)

![](../../../.gitbook/assets/image%20%28382%29.png)

그리고 Stripe\(Paypal 같은 서비스\)를 통해 만들어진 form을 이용해서 카드 정보를 입력하고 결제 할수 있어요. 

성공적으로 결제가 이루어지면 이전 화면에서 notification이 나타나서 membership 등록 성공 여부를 알려줘요. 

![](../../../.gitbook/assets/image%20%28383%29.png)



#### admin

관리자 화면에서는 이전 등록된 부분을 User memberships에서 확인 할 수 있어요.

![](../../../.gitbook/assets/image%20%28381%29.png)

그럼 admin 계정이 등록된 걸 확인 할 수 있습니다.   
무엇보다 membersip에 해당하는 계정이기  


![](../../../.gitbook/assets/image%20%28389%29.png)

해당 계정의 membership 상태도 확인 할 수 있어요.

![](../../../.gitbook/assets/image%20%28388%29.png)

실제 stripe 서비스를 통해 수익 창출이 가능하다는걸 다른 JustDjango 채널의 영상을 통해서 확인도 할 수 있었어요. 

![](../../../.gitbook/assets/image%20%28407%29.png)

## 결론 

유료 영상 웹앱 컨텐츠를 django 웹 프레임 워크를 통해 구축!

