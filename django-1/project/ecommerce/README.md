# Ecommerce

## 들어가기 앞서

### 개요

온라인 상거래 사이트를 간단히 만들어 볼게요. 

### 화면 둘러 보기 

#### 화면1

![](../../../.gitbook/assets/image%20%28388%29.png)

#### 화면2

![](../../../.gitbook/assets/image%20%28401%29.png)

#### 화면3 -1\(실제 해당 주소지로 배송되는 상품\)

![](../../../.gitbook/assets/image%20%28380%29.png)

#### 화면 3- 2\(배송이 필요 없는 상품\)

ex. Online paid contents

![](../../../.gitbook/assets/image%20%28385%29.png)



#### 화면4

![](../../../.gitbook/assets/image%20%28379%29.png)

#### 화면5

참고로 paypal business\(사업자용\), personal\(일반 구매자용\) 계정을 만들어야 가능합니다.

![](../../../.gitbook/assets/image%20%28397%29.png)

#### 화면6

![](../../../.gitbook/assets/image%20%28404%29.png)

#### 화면7 

![](../../../.gitbook/assets/image%20%28399%29.png)

#### 화면 8 

메인 화면으로 재접속하고 카트 수는 0으로 초기화됨.

![](../../../.gitbook/assets/image%20%28394%29.png)

## Model

![](../../../.gitbook/assets/image%20%28392%29.png)

This project will consist of 6 Models, so let's summarize each one:

1. **USER** 

* username
* first\_name
* last\_name
* email

2. **CUSTOMER** 

* user
* name
* email

3. **PRODUCT** -

* name
* price
* digital
* image

4. **ORDER** 

* product
* order
* quantity
* date\_added

5. **ORDERITEM** 

* product
* order
* quantity
* date\_added

#### 6. ShippingAddress

* customer
* order
* address
* city
* state
* zipcode
* date\_added



