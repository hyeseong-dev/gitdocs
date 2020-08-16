# Part 2 \| Render Products

## Step 1 \| Query Products

views.py 파일을 작성하도록 할게요.   
그리고 Query를 이용해서 products 변수를 만들도록 할게요.   
context 딕셔너리안에 products 변수와 그에 대응하는 문자열을 꼭 넣어주세요.

![](../../../../.gitbook/assets/image%20%28415%29.png)

## Step 2 \| Render Products

1.template rendering작업을 하기 앞서 &lt;div class="col-lg-4"&gt;&lt;/div&gt;가 3개 있을 거에요.   
1개만 제외하고 모두 지워주세요.



2.for문을 이용해서 제품을 template에 출력하도록 할게요. 

{% for product in products % } 이건 div column 바로 위에 작성할게요. 그리고 

{% endfor %}는 div column태그 바로 아래에 작성하도록 할게요.   
둘다 row 태그 안에 작성되요. 

![](../../../../.gitbook/assets/image%20%28464%29.png)

3. 제품의 이름 가격에 {{product.name}}, {{product.price\|floatformat:2}}d을 작성할게요. 

![](../../../../.gitbook/assets/image%20%28451%29.png)







