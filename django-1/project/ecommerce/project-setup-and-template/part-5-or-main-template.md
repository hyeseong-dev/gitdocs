# Part 5 \| Main Template

## **Step 1 \| Add HTML Boilerplate to main.html**

**표준 html 형식의 뼈대를 만들어 주세요.** 

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/2+blank-html.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/2+blank-html.png)

## **Step 2 \| Adding Viewport & Static**

**&lt;!DOCTYPE html&gt; 바로 아래에 load static를 작성하세요 그럼 image와 styling이 가능해요.   
그리고 &lt;head&gt; &lt;/head&gt;태그 내부에 viewport meta tag와 stylesheet을 작성해서 css가 가능하도록 작성할게요.**

\*\*\*\*

![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/3+template-1.png)

## **Step 3 \| Adding Bootstrap**

Bootstrap을 기본으로 메인 레이아웃으로 깔고 이용 할게요. 

{% embed url="https://getbootstrap.com/" %}



![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/4+nootstrap-links.png)

```text
///File: store/templates/store/main.html

<!DOCTYPE html>
{% load static %}
<html>
<head>
	<title>Ecom</title>

	<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1" />

	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">

	<link rel="stylesheet" type="text/css" href="{% static 'css/main.css' %}">

</head>
<body>


	<script src="https://code.jquery.com/jquery-3.4.1.slim.min.js" integrity="sha384-J6qa4849blE2+poT4WnyKhv5vZF5SrPo0iEjwBvKU7imGFAV0wwj1yYfoRSJoZ+n" crossorigin="anonymous"></script>

	<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>

	<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js" integrity="sha384-wfSDF2E50Y2D1uUdj0O3uMBJnjuUD4Ih7YwaYd1iqfktj0Uod8GCExl3Og8ifwB6" crossorigin="anonymous"></script>
</body>
</html>
```

## **Step 4 \| Container/Navbar Placeholder**

**navigation bar를 넣기 전에 placeholer를 모든 페이지에 상속하기 위해서 main.html페이지에 넣어주도록 할게요.  
&lt;body&gt;태그안에 div 태그를 만들고 class는 container'로 만들도록 할게요.** 

이후 div태그 안에 blcok태그를 만들게요. 

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/5+main-block-tag.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/5+main-block-tag.png)

## **Step 5 \| Inheritin**

**main.html를 갖고 store.html과 cart.html, checkout.html를 모두 상속 되도록 해볼건데요.** 

**아래처럼 코드를 작성해주세요.**

![](../../../../.gitbook/assets/image%20%28406%29.png)

![](../../../../.gitbook/assets/image%20%28398%29.png)

## 코드 실행

 [![](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/9+template-demo.png)](https://stepswithcode.s3-us-west-2.amazonaws.com/m1-prt5/9+template-demo.png)

