# Form?

폼은 알게 모르게 웹에서 많이 사용합니다. 사용자 의견이나 정보를 알기 위해 입력할 큰 틀을 만드는 데 사용되기 때문입니다. 폼은 입력된 데이터를 한 번에 서버로 전송합니다. 전송한 데이터는 웹 서버가 처리하고, 결과에 따른 또 다른 웹 페이지를 보여줍니다. 이번 글에서 우리가 잘 모르는 폼의 내부적인 동작과정부터 폼의 큰 틀을 구성하는 엘리먼트에 대해 알아보겠습니다.

### 1. 폼 태그 동작방법 <a id="1"></a>

1. 폼이 있는 웹 페이지를 방문합니다.
2. 폼 내용을 입력합니다.
3. 폼 안에 있는 모든 데이터를 웹 서버로 보냅니다.
4. 웹 서버는 받은 폼 데이터를 처리하기 위해 웹 프로그램으로 넘깁니다.
5. 웹 프로그램은 폼 데이터를 처리합니다.
6. 처리결과에 따른 새로운 html 페이지를 웹 서버에 보냅니다.
7. 웹 서버는 받은 html 페이지를 브라우저에 보냅니다.
8. 브라우저는 받은 html 페이지를 보여줍니다.

위 설명을 그림 1과 같이 표현할 수 있습니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-01.png)\[그림 1\]

### 2. 폼 태그 속성 <a id="2"></a>

폼 태그 속성에는 name, action, method, target 등이 있습니다. 폼 속성을 이용하여 전송할 때 어디로 보내야 하는지 그리고 어떤 방법으로 보낼지 정합니다. 폼 태그 속성은 다음과 같습니다.

* action : 폼을 전송할 서버 쪽 스크립트 파일을 지정합니다.
* name : 폼을 식별하기 위한 이름을 지정합니다.
* accept-charset : 폼 전송에 사용할 문자 인코딩을 지정합니다.
* target : action에서 지정한 스크립트 파일을 현재 창이 아닌 다른 위치에 열도록 지정합니다.
* method : 폼을 서버에 전송할 http 메소드를 정합니다. \(GET 또는 POST\)

아래 소스와 같이 폼 태그 속성을 지정할 수 있습니다.

```text
<html>  
    <head>
    </head>

    <body>
        <form action = "http://localhost:8080/form.jsp" accept-charset="utf-8" 
              name = "person_info" method = "get"> 

        </form>
    </body>
<html>  
```

전송할 http 메소드 종류인 GET과 POST는 브라우저에서 폼 데이터를 가져와 서버로 보내는 똑같은 기능을 수행하지만, 방식은 다릅니다. GET은 폼 데이터를 URL 끝에 붙여서 눈에 보이게 보내지만 POST 방식은 내부적으로 보이지 않게 보냅니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-03-1.png)\[그림 2\]

위 그림 2 위쪽은 GET 방식이고 아래쪽은 POST 방식입니다.

URL 끝에 데이터를 붙여 보내는 GET 방식은 데이터가 외부에 노출되어 보안에 취약합니다. 그래서 보내려는 데이터가 개인정보나 보안을 해야 하는 경우는 POST 방식을 사용해야 합니다. 또한, HTTP 메소드 정의에서 GET 방식은 지정된 리소스에서 데이터를 요청하는 경우인 읽을 때 사용하는 메소드입니다. 반면 POST 방식은 지정된 리소스에서 데이터를 처리할 경우인 쓰고, 수정, 삭제할 때 사용합니다.

보안이 필요하지 않으면서 지정된 리소스에서 자원을 읽을 경우에는 GET 방식을 사용하고, 그렇지 않다면 POST 방식을 사용하면 됩니다.

GET 방식과 POST 방식 대한 정보

[http://www.w3schools.com/tags/ref\_httpmethods.asp](http://www.w3schools.com/tags/ref_httpmethods.asp)

### 3. 폼을 구성하는 다양한 엘리먼트 <a id="3"></a>

#### \(1\) 폼 엘리먼트 그룹 &lt;field&gt;, &lt;legend&gt; 태그 <a id="1ltfieldgtltlegendgt"></a>

`<fieldset>` 태그는 폼 태그 안에 관련 있는 폼 엘리먼트들을 그룹화할 때 사용합니다. 그리고 `<fieldset>` 태그 하위에 `<legend>` 태그를 사용하여 그룹화한 폼 엘리먼트들을 목적에 맞게 이름을 지정합니다. 아래 그림 3과 같이 만들 수 있습니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-04.png)\[그림 3\]

```text
<html>  
    <head>
    </head>

    <body>
        <form action = "#" accept-charset="utf-8" name = "person_info" method = "get">
            <fieldset style = "width:150">
                <legend>개인 정보 입력</legend>
                    이름 : <input type = "text" name = "name"/><br><br>
                    나이 : <input type = "text" name = "age"/><br><br>
            </fieldset>
            <br>
            <fieldset style = "width:180; height:180">
                <legend>여가 활동</legend>
                    취미 : <input type = "text" name = "hobby"/><br><br>
                    특기 : <input type = "text" name = "specialty"/><br><br>
            </fieldset> 
        </form>
    </body>
<html>  
```

#### \(2\) 다양한 모양을 가진 &lt;input&gt; 태그 <a id="2ltinputgt"></a>

`<input>` 태그는 사용자가 다양하게 폼 태그에 입력할 수 있는 공간을 만들어 줍니다. 속성에는 type, readonly, maxlength 등이 있습니다. 자주 사용 되거나 알아두면 좋은 속성은 다음과 같습니다.

* type : 태그 모양을 다양하게 변경할 수 있습니다. type에는 text, radio, checkbox, password, button, hidden, fileupload, submit, reset 등을 지정할 수 있습니다.
* name : 태그 이름을 지정합니다.
* readonly : 태그를 읽기전용으로 합니다.
* maxlength : 해당 태그 최대 글자 수를 지정합니다.
* required : 해당 태그가 필수태그로 지정됩니다. 필수 태그를 입력하지 않고, submit 버튼을 누르면 에러메시지가 웹 브라우저에 출력됩니다. \(HTML5 추가사항\)
* autofocus : 웹 페이지가 로딩되자마자 이 속성을 지정한 태그로 포커스가 이동됩니다. \(HTML5 추가사항\)
* placeholder : 태그에 입력할 값에 대한 힌트를 줍니다. \(HTML5 추가사항\)
* pattern : 정규표현식을 사용하여 특정범위 내의 유효한 값을 입력받을 때 사용합니다. \(HTML5 추가사항\)

![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-05.png)\[그림 4\]

```text
<html>  
    <head>
    </head>

    <body>
        <form action = "#" accept-charset="utf-8" name = "person_info" method = "get">
            <fieldset style = "width:150">
                <legend>개인 정보 입력</legend>
                   이름 : <input type = "text" name = "name" required/><br><br>
                   주민번호 : <input type = "text" name = "security_number" 
                              pattern = "\d{6}\-\d{7}" 
                              title = "123456-1234567 형식으로 입력해주세요"/><br><br>

                   아이디 : <input type = "text" name = "id"/><br><br>
                   패스워드 : <input type = "password" name = "password"/><br><br>

                   성별 : 남<input type = "radio" name = "gender" />
                          여<input type = "radio" name = "gender" /><br><br>

                   관심사 : 연예<input type = "checkbox" name = "checkbox1" />
                            스포츠<input type = "checkbox" name = "checkbox2" />
                            IT<input type = "checkbox" name = "checkbox3" /><br><br>

                   <input type = "submit" value = "submit"/>
                   <input type = "reset" value = "reset"/><br><br>
            </fieldset> 
        </form>
    </body>
<html>  
```

위 그림 4는 `<input>` 태그 type 속성을 다양하게 지정하여 출력한 화면입니다. 주민번호 입력 칸은 HTML5에서 추가된 pattern 속성을 사용하여 정규표현식에 맞는 정확한 값을 입력해야 합니다. 정규표현식을 지키지 않고 submit 버튼을 누르면 정확한 입력방법 설명이 나타납니다. 체크박스는 여러 개를 선택할 수 있지만, 라디오는 그룹 목록 중 하나만 선택합니다. `<input>` 태그는 위 예제 말고도 다양하게 type속성을 지정할 수 있습니다. 책이나 인터넷 자료를 참고하여 상황에 맞게 지정하면 됩니다.

#### \(3\) 목록태그 &lt;select&gt;, &lt;optgroup&gt;, &lt;option&gt; <a id="3ltselectgtltoptgroupgtltoptiongt"></a>

`<select>`는 항목을 선택할 수 있는 태그입니다. 속성 중에 size와 multiple 속성이 있습니다. size는 한 번에 표시할 항목 수를 의미하고, multiple는 다중선택을 허용할 것인지를 지정하는 속성입니다. `<select>` 태그 하위에 `<optgroup>` 태그와 `<option>` 태그가 있습니다. `<optgroup>` 태그 는 `<select>` 태그 안에서 목록들을 그룹화할 경우 사용됩니다. label 속성을 사용하여 그룹 이름을 지정합니다. `<optgroup>` 태그 하위에 `<option>` 태그를 포함합니다. `<option>` 태그는 목록을 나타내는 태그입니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-06.png)\[그림 5\]

```text
<html>  
    <head></head>

    <body >
        <form action = "#" accept-charset="utf-8" name = "person_info" method = "get"> 
            <fieldset style = "width:250">
                <legend>개인 정보 입력</legend>
                    지역선택 (size, multiple속성 추가)<br>
                    <select name = "city2" size = "5" multiple>
                            <option value = "seongnam-si">성남시</option>
                            <option value = "suwon-si">수원시</option>
                            <option value = "yongin-si">용인시</option>
                            <option value = "anyang-si">안양시</option>
                            <option value = "gwacheon-si">과천시</option>
                            <option value = "hanam-si">과천시</option>  
                    </select>
                    <br><br>
                    지역선택 (optgroup 태그 포함)<br>
                    <select name = "city1">
                        <optgroup label = "서울">
                            <option value = "songpa-gu">송파구</option>
                            <option value = "gangnam-gu">강남구</option>
                            <option value = "seocho-gu">서초구</option>
                            <option value = "junggu-gu">중구</option>
                        </optgroup>

                         <optgroup label = "경기도">
                            <option value = "seongnam-si">성남시</option>
                            <option value = "suwon-si">수원시</option>
                            <option value = "yongin-si">용인시</option>
                            <option value = "anyang-si">안양시</option>
                        </optgroup>         
                    </select>
                    <br><br>
                    <input type = "submit" value = "submit"/>
                    <input type = "reset" value = "reset"/><br><br>
            </fieldset> 
        </form>
    </body>
</html>  
```

위 그림 5 위쪽 select 박스는 size 속성을 사용하여 한 번에 볼 수 있는 크기를 5개 목록으로 지정했습니다. size 속성 기본값은 4입니다. 그리고 multi ple 속성을 지정하여 한번에 여러 개를 선택합니다. 아래 select 박스는

#### \(4\) 여러 줄 글상자 &lt;textarea&gt; <a id="4lttextareagt"></a>

여러 줄을 입력받는 태그입니다. 속성 중에 rows와 cols가 있습니다. rows는 줄을, cols는 한 줄에 입력될 크기를 지정합니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-07.png)\[그림 6\]

```text
<html>  
    <head></head>

    <body >
        <form action = "#" accept-charset="utf-8" name = "person_info" method = "get"> 
            <fieldset style = "width:250">
                <legend>개인 정보 입력</legend>
                    가입 인사 <br>
                    <textarea name = "comment" cols = "50" rows = "5"  
                              placeholder="가입인사를 남겨주세요."></textarea>
                    <br><br>
                    <input type = "submit" value = "submit"/>
                    <input type = "reset" value = "reset"/><br><br>
            </fieldset> 
        </form>
    </body>
</html>  
```

위 그림 6은 `<textarea>` 태그를 사용하여 여러 줄을 입력받습니다. rows와 cols 속성에 각각 5와 50을 지정했습니다. placeholder 속성을 지정하여 텍스트 공간에 어떤 내용을 입력하면 되는지 힌트를 줬습니다. 이 외에도 다양한 속성이 있으며 상황에 맞게 적용하면 됩니다.

### 4. HTML5 에서 추가된 엘리먼트 <a id="4html5"></a>

HTML5에서 새롭게 추가된 엘리먼트들이 있습니다. 그 중에서 유용한 엘리먼트를 소개 하겠습니다.

#### \(1\) 입력 값 후보 &lt;datalist&gt; <a id="1ltdatalistgt"></a>

텍스트 상자에 입력 값 후보 목록을 지정할 경우 사용합니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-08.png)\[그림 7\]

```text
<html>  
    <head></head>

    <body >
        <form action = "#" accept-charset="utf-8" name = "datalist" method = "get"> 
            <fieldset style = "width:350">
                <legend>HTML5 < 입력 값 후보 ></legend>
                    <br>
                    자주 사용하는 웹 브라우저를 입력해주세요.<br>
                    <input type = "text" name = "browser" list = "browser">
                    <datalist id = "browser">
                        <option value = "크롬">Google</option>
                        <option value = "파이어폭스">Mozilla</option>
                        <option value = "사라피">Apple</option>
                        <option value = "익스플로러">MicroSoft</option>
                    </datalist>
                    <br><br>
                    <input type = "submit" value = "submit"/>
                    <input type = "reset" value = "reset"/><br><br>
            </fieldset> 
        </form>
    </body>
</html>  
```

위 소스 부분에서 `<datalist>` 태그 id 값을 `<input>` 태그 list 속성값으로 지정하여 텍스트 박스 아래 그룹리스트로 출력되는 것을 볼 수 있습니다.

#### \(2\) &lt;input&gt; 태그의 date <a id="2ltinputgtdate"></a>

날짜를 입력받기 위한 속성값입니다. 날짜 선택을 위한 달력도 함께 표시됩니다. 이 값이 서버 프로그램에 전달되면 자바 date 객체에 바로 데이터가 전달됩니다. 그래서 쉽게 date 데이터를 서버 프로그램에서 받을 수 있는 장점이 있습니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-10.png)\[그림 8\]

```text
<html>  
    <head></head>

    <body >
        <form action = "#" accept-charset="utf-8" name = "datalist" method = "get"> 
            <fieldset style = "width:350">
                <legend>HTML5 < date ></legend>
                    <br>
                    날짜 입력<br>
                    <input type = "date" min = "1987-07-01" max = "2014-03-01" name = "date" step = "7">
                    <br><br>
                    <input type = "submit" value = "submit"/>
                    <input type = "reset" value = "reset"/><br><br>
            </fieldset>
        </form>
    </body>
</html>  
```

날짜와 관련된 것에는 date 말고 month, week, time, datatime, datetime-local이 추가되었습니다. date 속성과 비슷하게 지정하면 사용자가 원하는 결과를 볼 수 있습니다.

#### \(3\) &lt;input&gt; 태그의 number와 range <a id="3ltinputgtnumberrange"></a>

number와 range는 둘 다 숫자를 입력할 때 사용합니다. 차이점으로 range 태그는 슬라이더 형태의 UI로 렌더링 된다는 점입니다. min, max 속성을 사용하여 최소 최댓값을 지정합니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-11.png)\[그림 9\]

```text
<html>  
    <head></head>

    <body >
        <form action = "#" accept-charset="utf-8" name = "datalist" method = "get"> 
            <fieldset style = "width:350">
                <legend>HTML5 < number ></legend>
                   number : <input type = "number" min = "0" max = "100" step = "10" name = "number">       
            </fieldset>
            <br><br><br>
            <fieldset style = "width:350">
                <legend>HTML5 < range ></legend>
                   range : <input type = "range" min = "0" max = "100" step = "10" name = "range">    
            </fieldset>
            <br><br>
            <input type = "submit" value = "submit"/>
            <input type = "reset" value = "reset"/><br><br>
        </form>
    </body>
</html>  
```

위 그림 9와 같이 숫자만 입력받을 수 있습니다. 숫자가 아닌 값을 입력하고 submit 버튼을 누르면 에러메시지가 나타납니다. range는 슬라이더 모습으로 숫자를 지정하는 것을 확인할 수 있습니다.

#### \(4\) &lt;input&gt; 태그의 color <a id="4ltinputgtcolor"></a>

색상을 입력받을 때 사용합니다. color 타입은 아직 모든 웹 브라우저에서 지원하지 않지만, 일부 웹 브라우저에서 Color Picker 형태의 UI로 렌더링 됩니다.![](http://www.nextree.co.kr/content/images/2016/09/hjkwon-140328-form_-12.png)\[그림 10\]

```text
<html>  
    <head></head>

    <body>
        <form action = "#" accept-charset="utf-8" name = "datalist" method = "get"> 
            <fieldset style = "width:350">
                <legend>HTML5 < color ></legend>
                   color : <input type = "color" color = "color">    
            </fieldset>
            <br><br>
            <input type = "submit" value = "submit"/>
            <input type = "reset" value = "reset"/><br><br>
        </form>
    </body>
</html>  
```

위 그림 10과 같이 색상을 선택할 수 있는 창이 나타나는 걸 확인할 수 있습니다.

이 밖의 기능 말고도 다른 기능도 많이 있으며 상황에 맞게 책이나 인터넷을 통해 쉽게 사용할 수 있습니다.

### 5. 마치며 <a id="5"></a>

폼은 웹 페이지 안에 또 다른 페이지이며 사용자와 대화를 할 수 있게 해줍니다. 폼을 구성하는 큰 틀은 HTML 문법에 맞게 작성하면 누구든지 쉽게 만들 수 있습니다. 폼을 구성하는 정보는 많이 있으며, 상황에 맞게 지정하면 큰 어려움 없이 만들 수 있습니다. 지금까지 폼의 내부 동작 과정부터 폼을 구성하는 엘리먼트에 대해 알아보았습니다. HTML을 처음 접하거나 폼을 처음 만드는 분에게 많은 도움이 되었으면 하는 바람입니다.

### 참조 도서 및 사이트

* 김데레사 저, 웹 표준 핵심가이드북2 HTML5+CSS3
* 엘리자베스 프리먼, 에릭 프리먼 저, Head First HTML With CSS & XHTML
* 웹 문서 - [http://www.w3schools.com/](http://www.w3schools.com/)

####  해당글 출처 

[http://www.nextree.co.kr/p8428/](http://www.nextree.co.kr/p8428/)

