# API call/Adding the JSON response

## 들어가기 앞서 

이전 시간 Table Creation을 했어요. 이번에는 Ajax를 이용해서 API endpoint 요청을 만들거고  
요청 받은 data를 바탕으로 테이블에 출력 하도록 할게요.   
  
API call과 JSON 응답을 html table에 적용시켜보도록 할게요

## 현재까지 소스코드 

```text
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

<style>
    th{ 
        color:#fff;
            }
</style>


<table class="table table-striped">
    <tr  class="bg-info">
        <th>Name</th>
        <th>Age</th>
        <th>Birthday</th>
    </tr>

    <tbody id="myTable">
        
    </tbody>
</table>

<script>
	var myArray = [
	    {'name':'Michael', 'age':'30', 'birthdate':'11/10/1989'},
	    {'name':'Mila', 'age':'32', 'birthdate':'10/1/1989'},
	    {'name':'Paul', 'age':'29', 'birthdate':'10/14/1990'},
	    {'name':'Dennis', 'age':'25', 'birthdate':'11/29/1993'},
	    {'name':'Tim', 'age':'27', 'birthdate':'3/12/1991'},
	    {'name':'Erik', 'age':'24', 'birthdate':'10/31/1995'},
	]
	
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



## jQuery 

첫 째줄에 jQuery 소스 코드를 붙여넣었는데요. 이제 jquery method를 사용해 볼게요. 

13번째부터 19번째에 소스코드를 작성할게요.

```text
<script>
	var myArray = [
	    {'name':'Michael', 'age':'30', 'birthdate':'11/10/1989'},
	    {'name':'Mila', 'age':'32', 'birthdate':'10/1/1989'},
	    {'name':'Paul', 'age':'29', 'birthdate':'10/14/1990'},
	    {'name':'Dennis', 'age':'25', 'birthdate':'11/29/1993'},
	    {'name':'Tim', 'age':'27', 'birthdate':'3/12/1991'},
	    {'name':'Erik', 'age':'24', 'birthdate':'10/31/1995'},
	]
	
	buildTable(myArray)

	$.ajax({
		method:'GET',
		url:'https://regres.in/api/users',
		success:function(response){
			console.log(response)
		}
	})


	function buildTable(data){
```

사전에 만들었던 myArray의 내용들을 다 지우고 빈 값으로 둘게요.   
그럼 실제 내용물이 들어있는 response를 받아서 myArray에 넣겠조?

```text
<script>
	var myArray = []
	
	buildTable(myArray)

	$.ajax({
		method:'GET',
		url:'https://regres.in/api/users',
		success:function(response){
			myArray = response
			console.log(response)
		}
	})


	function buildTable(data){
```

![](../../.gitbook/assets/image%20%28361%29.png)

분명 우리는 빈 array로 줬는데 값이 들어있는 모습이네요. 다시 수정해 볼게요.



![](../../.gitbook/assets/image%20%28348%29.png)

response뒷부분에 .data를 입력했어요.   


![](../../.gitbook/assets/image%20%28363%29.png)

안의 데이터 내용을 보니 테이블 구조를 조금 바꿔 줄게요. 

![](../../.gitbook/assets/image%20%28360%29.png)

이번엔 ajax메소드 안에서 buildTable 함수를 호출하도록 할텐데요.   
  
그리고 기존에 작성된 값들 3개 몽땅 바꾸도록 할게요. 

![](../../.gitbook/assets/image%20%28366%29.png)

그리고 기존 호출되었던 buildTable함수를 호출했던 소스코드를 삭제할게요.

![](../../.gitbook/assets/image%20%28354%29.png)



그리고 나서 확인해보니 아래와 같이 잘 출력된 걸 확인 할 수 있어요. 

![](../../.gitbook/assets/image%20%28362%29.png)

```text
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>

<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

<style>
    th{ 
        color:#fff;
            }
</style>


<table class="table table-striped">
    <tr  class="bg-info">
        <th>Name</th>
        <th>Age</th>
        <th>Birthday</th>
    </tr>

    <tbody id="myTable">
        
    </tbody>
</table>

<script>
	var myArray = []
	
	$.ajax({
		method:'GET',
		url:'https://reqres.in/api/users',
		success:function(response){
			myArray = response.data
			buildTable(myArray)
			console.log(response)
		}
	})


	function buildTable(data){
		var table = document.getElementById('myTable')

		for (var i = 0; i < data.length; i++){
			var row = `<tr>
							<td>${data[i].first_name}</td>
							<td>${data[i].last_name}</td>
							<td>${data[i].email}</td>
					  </tr>`
			table.innerHTML += row


		}
	}

</script>
```





