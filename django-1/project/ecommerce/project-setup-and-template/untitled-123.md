# Part 8 \| cart.html

##  들어가기 앞서 

이번 cart.html페이지는 아래와 같이 최종적으로 나오게 될거에요.

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/1+cart.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/1+cart.png)

download below images

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/2+arrow-down.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/2+arrow-down.png) [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/3+arrow-up.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/3+arrow-up.png)

## **Step 1 \| Layout**

아래 코드는 row 하나에 12개의 column을 통으로 다 쓸거고 box는 2개 만든다는 말이에요.

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/4+cart-layout.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/4+cart-layout.png)

```text
///File: store/templates/store/cart.html

<div class="row">
	<div class="col-lg-12">
		<div class="box-element">

		</div>

		<br>
		<div class="box-element">

		</div>
	</div>
</div>
```

## **Step 2 \| Cart Headers**

**안에 class 속성과 href속성 값을 작성해주세요. 그리고 Continue Shopping 글 바로 앞에 특수문자와 숫자 2190이있는데 고건 &lt;- 화살표를 나타내주게 되요.** 

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/5+back-btn.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/5+back-btn.png)

 아래는 br태그와 table 태그를 잘 버무려서 Items, Total, Checkout 버튼을 각각 구현했는건데요. th태그중 Checkout부분만 신경써서 작성해주세요.

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/6+header.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/6+header.png)

```text
///File: store/templates/store/cart.html

<div class="box-element">
	<a  class="btn btn-outline-dark" href="{% url 'store' %}">&#x2190; Continue Shopping</a>
	<br>
	<br>
	<table class="table">
		<tr>
			<th><h5>Items: <strong>3</strong></h5></th>
			<th><h5>Total:<strong> $42</strong></h5></th>
			<th>
				<a  style="float:right; margin:5px;" class="btn btn-success" href="{% url 'checkout' %}">Checkout</a>
			</th>
		</tr>
	</table>
</div>
```

## **Step 3 \| Cart Rows**

여기서 눈여겨 볼 점은 이전에 다운받았던 placeholder.png ,arrow-up.png, arrow-down.png파일을 static변수와 연결시켜 출력해줘야해요. 

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/7+row-cart.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/7+row-cart.png)

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/8+row-items.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt8/8+row-items.png)

```text
///File: store/templates/store/cart.html

<div class="box-element">
	<div class="cart-row">
		<div style="flex:2"></div>
		<div style="flex:2"><strong>Item</strong></div>
		<div style="flex:1"><strong>Price</strong></div>
		<div style="flex:1"><strong>Quantity</strong></div>
		<div style="flex:1"><strong>Total</strong></div>
	</div>
	
	<div class="cart-row">
		<div style="flex:2"><img class="row-image" src="{% static 'images/placeholder.png' %}"></div>
		<div style="flex:2"><p>Product 1</p></div>
		<div style="flex:1"><p>$20</p></div>
		<div style="flex:1">
			<p class="quantity">2</p>
			<div class="quantity">
				<img class="chg-quantity" src="{% static  'images/arrow-up.png' %}">
		
				<img class="chg-quantity" src="{% static  'images/arrow-down.png' %}">
			</div>
		</div>
		<div style="flex:1"><p>$32</p></div>
	</div>
```

