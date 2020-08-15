# Part 9 \| Checkout.html

## 들어가기 앞서 

이번 checkout.html페이지를 아래와 같이 만들어 볼게요.

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/1+checkout.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/1+checkout.png)

## **Step 1 \| Layout**

**1개의 로우와 2개의 컬럼으로 만들도록 할게요.** 

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/2+checkout-layout.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/2+checkout-layout.png)

```text
///File: store/templates/store/checkout.html

<div class="row">
	<div class="col-lg-6">
		<div class="box-element" id="form-wrapper">

		</div>
		
	</div>

	<div class="col-lg-6">
		<div class="box-element">

		</div>
	</div>
</div>
```

## Step 2 \| Form

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/3+cart-form-empty.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/3+cart-form-empty.png)

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/4+form-full.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/4+form-full.png)

```text
<form id="form">
	<div id="user-info">
		<div class="form-field">
			<input required class="form-control" type="text" name="name" placeholder="Name..">
		</div>
		<div class="form-field">
			<input required class="form-control" type="email" name="email" placeholder="Email..">
		</div>
	</div>
	
	<div id="shipping-info">
		<hr>
		<p>Shipping Information:</p>
		<hr>
		<div class="form-field">
			<input class="form-control" type="text" name="address" placeholder="Address..">
		</div>
		<div class="form-field">
			<input class="form-control" type="text" name="city" placeholder="City..">
		</div>
		<div class="form-field">
			<input class="form-control" type="text" name="state" placeholder="State..">
		</div>
		<div class="form-field">
			<input class="form-control" type="text" name="zipcode" placeholder="Zip code..">
		</div>
	</div>
	<hr>
	<input id="form-button" class="btn btn-success btn-block" type="submit" value="Continue">
</form>
```

## Step 3 \| Payment Option

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/5+payment-options.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/5+payment-options.png)

```text
///File: store/templates/store/checkout.html

<br>
<div class="box-element hidden" id="payment-info">
	<small>Paypal Options</small>
</div>
```



## Step 4 \| Order Summary

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/6+link-back.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/6+link-back.png)

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/7+title.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/7+title.png)

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/8+cart-rows-checkout.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt9/8+cart-rows-checkout.png)

```text
<div class="box-element">
	<a  class="btn btn-outline-dark" href="{% url 'cart' %}">&#x2190; Back to Cart</a>
	<hr>
	<h3>Order Summary</h3>
	<hr>
	<div class="cart-row">
		<div style="flex:2"><img class="row-image" src="{% static 'images/placeholder.png' %}"></div>
		<div style="flex:2"><p>Product 1</p></div>
		<div style="flex:1"><p>$20.00</p></div>
		<div style="flex:1"><p>x2</p></div>
	</div>
	<h5>Items:   2</h5>
	<h5>Total:   $40</h5>
</div>
```

