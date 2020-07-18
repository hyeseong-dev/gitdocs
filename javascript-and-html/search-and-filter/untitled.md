# Search/Filter

자바스크립트를 이용하여 프론트엔드의 search기능을 구현해보도록 할게요.  
  
아래 소스 html source code를 베이스로 해서 작성해보도록 할게요.

## 시작 전 소스코드 

{% file src="../../.gitbook/assets/sorttable.html" %}

{% tabs %}
{% tab title="sorttable.html" %}
```text
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

<style>
    th{ 
        cursor: pointer;
        color:#fff;
            }
</style>

<div class="row">
  <div class="col">
    <div class="card card-body">

      <input id="search-input" class="form-control" type="text">
    </div>
  </div>
</div>

<table class="table table-striped">
    <tr  class="bg-info">
        <th  class="bg-info" data-colname="name" data-order="desc">Name &#9650</th>
        <th  data-colname="age" data-order="desc">Age &#9650</th>
        <th  data-colname="birthdate" data-order="desc">Birthday &#9650</th>
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

    table.innerHTML = ''
    
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
{% endtab %}
{% endtabs %}

일단 현재 나온 화면은 아래와 같아요.   
검색창이 테이블 위에 보이네요.  


![](../../.gitbook/assets/image%20%28353%29.png)

### 

### Keyup Event 등록

소스코드 등록 위치는 아래와 같아요 그리고 

![](../../.gitbook/assets/image%20%28350%29.png)

아래와 같이 search-input id에 keyup이벤트를 등록했어요. 

![](../../.gitbook/assets/image%20%28355%29.png)

크롬 개발자도구의 console창을 띄워놓고 검색창에 타이핑을 하는순간 값들이 즉각적으로  console에 출력되는걸 확인 할 수 있어요. **event handler**가 잘 작동되는게 확인되는 부분이군요.

![](../../.gitbook/assets/image%20%28344%29.png)

### 

### 

### searchTable 메소드 

아래 searchTable에 대소문자 구분을 없애도록 할게요. 

![](../../.gitbook/assets/image%20%28357%29.png)

![](../../.gitbook/assets/image%20%28352%29.png)

![](../../.gitbook/assets/image%20%28346%29.png)

위의 빨간 부분이 소문자 구분 없이 바로 즉각적으로 테이블 내의 이름을 매칭시켜서 찾아주게되요.

![](../../.gitbook/assets/image%20%28356%29.png)

