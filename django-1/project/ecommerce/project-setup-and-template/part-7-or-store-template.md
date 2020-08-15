# Part 7 \| Store.html

## 살펴보기 

store.html을 아래와 같이 만들텐데요. 기본적으로 여러 행과 3개의 열로 구성되게되요. 

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/1+store.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/1+store.png)

#### download below image

아래 이미지를 다운받아 static/images폴더에 저장해 주세요.

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/2+placeholder.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/2+placeholder.png)

## **Step 1 \| Layout**

**1개의 컬럼은 4/12, 4/12, 4/12로 총 12등분을 기준으로 bootstrap은 row를 구성하게 되요.**

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/3+row.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/3+row.png)

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/4+box.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/4+box.png)

그리고 1개 컬럼 안에 box-element product 클래스 값을 만들어 div태그를 구성시켜 3개 column모두 동일하게 적용하면 아래 이미지 처럼 나타나게 되요.

![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/5+empty.png)

## **Step 2 \| Placeholder Content**

col-lg-4 class안에 img, div 태그를 만들어 줄게요.   
특히 img 태그의 src 속성값을 jinja문법을 이용해서 static 변수로 연결하여 placeholder.png 출력 하도록 할게요.[  
![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/6+placeholder+img.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/6+placeholder+img.png)

h6태그\(제품 이름이 출력됨\)와 hr 태그를 작성할게요.

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/7+title.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/7+title.png)

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/8+buttons.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt7/8+buttons.png)

```text
///File: store/templates/store/store.html

<div class="col-lg-4">
	<img class="thumbnail" src="{% static 'images/placeholder.png' %}">
	<div class="box-element product">
		<h6><strong>Product</strong></h6>
		<hr>

		<button  class="btn btn-outline-secondary add-btn">Add to Cart</button>
		<a class="btn btn-outline-success" href="#">View</a>
		<h4 style="display: inline-block; float: right"><strong>$20</strong></h4>

	</div>
</div>
```

## 확인하기 

![](../../../../.gitbook/assets/image%20%28396%29.png)

