---
description: JSON Array to HTML Table with Javascript
---

# Table Creation

## 들어가기 앞

실습할 파일은 아래 파일을 다운 받아 진행할게요.

{% file src="../.gitbook/assets/jsontable.html" %}

자바스크랩트의 객체배열에 대해 배워볼게요.  


언제 사용할떄 좋나요?  
**1. API를 호출하거나   
2. 직접 만든 REST API를 DB로 부터 호출하여 사용할때**

### **뭐 만들건지?**

**첫째, 우선 아래와 같은 표를 만들거에요.**

![](../.gitbook/assets/image%20%28346%29.png)

둘째,  sorting 기능을 구현해 볼게요.\(name, age, birthday\)

![](../.gitbook/assets/image%20%28348%29.png)

셋째, 검색 기능을 구현해 볼게요. 

![](../.gitbook/assets/image%20%28343%29.png)

넷째, API를 만들어서 URL을 랜더링해서 HTML테이블로 나타나도록 할게요.



### 뼈대 

테이블의 컬럼 3개와 약간의 스타일링을 아래와 같이 할거에요. 

![](../.gitbook/assets/image%20%28353%29.png)

가장 첫번째 줄은 jquery리 cdn을 박아 넣을게요.   
그리고 아래에 Bootstrap을 붙여 넣을게요.

![](../.gitbook/assets/image%20%28354%29.png)

그리고 소스코드가 계속 이어져서 아래 스크린샷의 1번은 css를 이용한거에요.   
2번째는 html table태그를 이용해서 th태그의 이름을 딱 정해뒀어요.   
테이블이 파랗게 나타난 이유는 &lt;tr class="bg-info"&gt; 이 소스코드를 지정해줘서 그래요.  
  
3번째는 array of object 객체 배열이 나오게되요. 

![](../.gitbook/assets/image%20%28345%29.png)

이제 본격적으로 함수를 만들어 볼건데요. 3번 바로 아래에 작성하면 되요.   
3번째 줄에 테이블 쿼리문을 작성해볼게요. 

그 아래에 for문을 작성해서 테이블 row를 하나씩 생성하게되요.  
6번째 줄에 row 변수를 생성하고 backtick\(홑&쌍따옴표 역할을 하지만 줄 바꿈을해도 영향이 없음\)을 만들어주세요.

&lt;tr&gt;태그로 감싸주고 안에 &lt;td&gt;를 작성하고 그리고 그 안의 내용은 $기호와 curly bracket으로 작성해주세요.  
그리고 매개변수로 받은 data가 0번부터 해서 순차적으로 key값이 정의된 대로 출력되게 되요.   
  
11번째의 table변수의 innerHTML 형식으로 말이조.

```text

	function buildTable(data){
		var table = document.getElementById('myTable')

		for (var i = 0; i < data.length; i++){
			var row = `<tr>
							<td>${data[i].name}</td>
							<td>${data[i].age}</td>
							<td>${data[i].birthdate}</td>
					  </tr>`
			table.innerHTML += row


		}
	}

</script>
```

위의 정의된 소스코드들이 호출되어야겠조? 

우리가 정의한 javascript 소스코드 위에 호출해주면 딱!되요.

```text
	buildTable(myArray)
	
	function buildTable(data){
		var table = document.getElementById('myTable')

		for (var i = 0; i < data.length; i++){
			var row = `<tr>
							<td>${data[i].name}</td>
							<td>${data[i].age}</td>
							<td>${data[i].birthdate}</td>
					  </tr>`
			table.innerHTML += row


		}
	}

</script>
```

