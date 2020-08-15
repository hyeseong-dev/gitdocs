# Part 6 \| Navbar

**Step 1 \| Bootstrap Navbar**

**bootstrap웹사이트에서** 

{% embed url="https://getbootstrap.com" %}

아래 navbar에 해당하는 코드를 가져와주세요.\(그냥 제가 붙여넣은거 따라서 pate하면되요.\)

```text
///Bootstrap Navbar code

<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="#">Home <span class="sr-only">(current)</span></a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Link</a>
      </li>
      <li class="nav-item dropdown">
        <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
          Dropdown
        </a>
        <div class="dropdown-menu" aria-labelledby="navbarDropdown">
          <a class="dropdown-item" href="#">Action</a>
          <a class="dropdown-item" href="#">Another action</a>
          <div class="dropdown-divider"></div>
          <a class="dropdown-item" href="#">Something else here</a>
        </div>
      </li>
      <li class="nav-item">
        <a class="nav-link disabled" href="#">Disabled</a>
      </li>
    </ul>
    <form class="form-inline my-2 my-lg-0">
      <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">Search</button>
    </form>
  </div>
</nav>
```

![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/2+bootstrap+copy.png)

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/4+navbar.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/4+navbar.png)

**참고로 2줄 아니에요.\(16번째줄 ~ 50번째줄\)** 

## **Step 2 \| Dark Theme**

**만약 navbar 색깔을 검은색으로 바꾸고 싶으면 After형식대로 작성해주세요.** 

**bg-light -&gt; bg-dar**

Before:

```text
<nav class="navbar navbar-expand-lg navbar-light bg-light">
```

After:

```text
<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
```

![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/5+navbar-in-template.png)

## **Step 3 \| Customize Navbar**

bootstrap에서 가져온 코드를 그대로 사용하지 않고 약간의 수정\(삭제, 추가\)이 필요해요.  
일단 nav 태그에 해당하는 부분을 update했는데요.   
아래 코드를 가져가 주세요.

```text
///File: store/templates/store/main.html

<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <a class="navbar-brand" href="{% url 'store' %}">Ecom</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>

  <div class="collapse navbar-collapse" id="navbarSupportedContent">
    <ul class="navbar-nav mr-auto">
      <li class="nav-item active">
        <a class="nav-link" href="{% url 'store' %}">Store <span class="sr-only">(current)</span></a>
      </li>
 
    </ul>
    <div class="form-inline my-2 my-lg-0">
     	<a href="#"class="btn btn-warning">Login</a>
     	
     	<a href="{% url 'cart' %}">
    		<img  id="cart-icon" src="{% static 'images/cart.png' %}">
    	</a>
    	<p id="cart-total">0</p>

    </div>
  </div>
</nav>
```

## **Step 4 \| Custom CSS**

**아마 위의 코드를 적용해도 글자 크기 이미지 크기 배치등이 헝클어져 있을거에요.   
깔끔하게 모양을 다듬기 위해서 main.css파일을 아래 코드로 복붙해주세요.**

**그럼 아래 이미지가 적용될거에요.**

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/6+updated-template.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/6+updated-template.png)

```text
///File: static/css/main.css

body{
	background-color: hsl(0, 0%, 98%);
}

h1,h2,h3,h4,h5,h6{
	color:hsl(0, 0%, 30%);
}

.box-element{
	box-shadow:hsl(0, 0%, 80%) 0 0 16px;
	background-color: #fff;
	border-radius: 4px;
	padding: 10px;
}

.thumbnail{
	width: 100%;
	height: 200px;
	-webkit-box-shadow: -1px -3px 5px -2px rgba(214,214,214,1);
    -moz-box-shadow: -1px -3px 5px -2px rgba(214,214,214,1);
    box-shadow: -1px -3px 5px -2px rgba(214,214,214,1);
}

.product{
	border-radius: 0 0 4px 4px;
}

.bg-dark{
	background-color: #4f868c!important;
}

#cart-icon{
	width:25px;
	display: inline-block;
	margin-left: 15px;
}

#cart-total{
	display: block;
	text-align: center;
	color:#fff;
	background-color: red;
	width: 20px;
	height: 25px;
	border-radius: 50%;
	font-size: 14px;
}

.col-lg-4, .col-lg-6, .col-lg-8, .col-lg-12{
	margin-top: 10px;
}

.btn{
	border-radius: 0;
}

.row-image{
	width: 100px;
}

.form-field{
	width:250px;
	display: inline-block;
	padding: 5px;
}

.cart-row{
	display: flex;
    align-items: flex-stretch;
    padding-bottom: 10px;
    margin-bottom: 10px;
    border-bottom: 1px solid #ececec;

}

.quantity{
	display: inline-block;
	font-weight: 700;
	padding-right:10px;
	

}

.chg-quantity{
	width: 12px;
	cursor: pointer;
	display: block;
	margin-top: 5px;
	transition:.1s;
}

.chg-quantity:hover{
	opacity: .6;
}


.hidden{
	display: none!important;
}
```



## 다른 템플릿

앞으로 남은 template의 모습인데요. 추후에 아래 이미지대로 만들어 보도록 할게요. 그 이후 database setup도 해보도록 할게요.

**store.html**

[![store.html](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/7+store.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/7+store.png)

**cart.html**

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/8+cart.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/8+cart.png)

**checkout.html**

[![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/9+checkout.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt6/9+checkout.png)

