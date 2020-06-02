# Appendix

안드로이드 운영체계는 "SQLite" 데이터베이스를 기본으로 지원합니다.

SQLite의 사전적 의미는

"SQLite는 MyAQL이나 PostgreSQL과 같은 데이터베이스 관리 시스템이지만,   


서버가 아니라 응응프로그램에 넣어 사용하는 비교적 가벼운 데이터베이스이다.

일반적인 RDBMS에 비해 대규모 작업에는 적합하지 않지만, 중소 규모라면 속도에 손색이 없다.   


또 API는 단순히 라이브러리를 호출하는 것만 있으며, 데이터를 저장하는 데 하나의 파일만을 사용하는 것이 특징이다." - Wikipedia  


자세한 내용은 SQL 문법 참고 사이트를 방문해 보시기 바랍니다..

**데이터베이스의 간단한 구성 : 테이블, 레코드, 필드**  
  
데이터베이스를 구성하는 요소는 참으로 다양하지만, 자주 쓰이는 것들은 기본적인 것들 몇 가지들입니다.   
  
**1. 테이블**  
  
![](https://t1.daumcdn.net/cfile/tistory/13052A214A453C8656)

  
  테이블은 데이터들이 저장되어 있는 공간입니다. 테이블은 특정 주제에 관련된 데이터들을 담고 있으므로, 하나의 데이터베이스 내에는 여러 개의 테이블이 존재할 수 있습니다.   
  
**2. 필드**  
  
![](https://t1.daumcdn.net/cfile/tistory/1852A8144A4E6F7920)

![](https://t1.daumcdn.net/cfile/tistory/16289C124A4E7E6B26)

  
필드는 각 항목의 "분류" 정도로 보면 되겠습니다. 전화번호부의 이름, 전화번호, 이메일주소 등이 필드에 해당됩니다.  
  
**3. 레코드**  
  
![](https://t1.daumcdn.net/cfile/tistory/1752A8144A4E6F7A21)

  
  
레코드는 하나의 항목과 관련된 필드의 값의 집합입니다. 예를 들면 위의 그림에서는 \_id가 2, name은 google, phone은 12345 인 데이터의 집합이 하나의 레코드입니다. 이것 뿐 아니라 나머지 하이라이트된 4개 항목도 모두 레코드이지요. 전화번호부를 예로 들자면, 한 사람이 가지고 있는 데이터들\(이름, 전화번호, 이메일주소\)을 레코드라 할 수 있습니다.  
  
  
**안드로이드에서 데이터베이스 다루기 : 데이터베이스 어댑터**  
  
  데이터베이스를 생성하고, 열고, 데이터베이스에 데이터를 넣고, 쿼리를 통해서 데이터베이스에서 정보를 받아오는 작업은 SQLiteDatabase\([android.database.sqlite.SQLiteDatabase](http://developer.android.com/reference/android/database/sqlite/SQLiteDatabase.html)\) 와 SQLiteOpenHelper\([android.database.sqlite.SQLiteOpenHelper](http://developer.android.com/reference/android/database/sqlite/SQLiteOpenHelper.html)\) 내의 메소드를 통해 처리됩니다.   
  
  **SQLiteDatabase** 클래스에서는 데이터베이스를 다루는 작업\(추가, 삭제, 수정, 쿼리\)를 담당하고, **SQLiteOpenHelper** 클래스에스는 데이터베이스의 생성, 열기, 업그레이드를 담당합니다. 이러한 클래스 내의 메소드를 통해 직접 데이터베이스를 생성하고, 수정하고, 쿼리를 수행할 수도 있지만 이렇게 할 경우 코드상에 데이터베이스 구조들도 다 드러나게 되고, 실제로 코드를 볼 때에도 이 코드가 무엇을 하는 코드인지 바로 보기 불편합니다. 그래서, 일반적으로는 내가 사용할 데이터베이스에 맞게끔 데이터베이스 어댑터를 만들고 어댑터를 통해 데이터베이스를 관리합니다.  
  
  
**데이터베이스에서 원하는 자료를 받아오기 : 쿼리\(query; 질의\)**  
  
  데이터베이스를 생성하고 자료를 추가하는 것 못지않게 중요한 것이 바로 자신이 원하는 데이터베이스를 가져오는 것입니다. 이는 쿼리\(Query; 질의\)를 통해 이루어집니다. 질의 결과는 Cursor객체 형태로 반환됩니다.  
  
**public Cursor query \(String table, String\[\] columns, String selection, String\[\] selectionArgs,   
String groupBy, String having, String orderBy, String limit\)**   
  


* table  질의를 수행할 테이블 이름입니다.
* columns  자료를 받아올 필드들입니다. null을 입력하면 모든 필드를 반환합니다.
* selection  SQL의 "where" 구문에 해당되는 조건을 입력합니다. 조건이 많을 경우, ?로 대체합니다.
* selectionArgs  selection을 ?로 지정하였을 경우, 그 조건들을 입력합니다.
* groupBy  SQL의 "group by"구문에 해당합니다.
* having  groupBy를 지정했을 경우, 그 조건을 넣어줍니다.
* orderBy  결과값 정렬 방식을 지정합니다. null을 입력하면 기본 정렬을 수행합니다.
* limit  결과값의 개수를 제한합니다.

  
\(API : [android.database.sqlite.SQLiteDatabase](http://developer.android.com/reference/android/database/sqlite/SQLiteDatabase.html#query%28java.lang.String,%20java.lang.String[],%20java.lang.String,%20java.lang.String[],%20java.lang.String,%20java.lang.String,%20java.lang.String,%20java.lang.String%29)\)  
위에서 소개된 형태 외에도 다른 형태로 2가지 메소드가 있으니 참조하시면 됩니다.  
  
예제\)  
[?](http://androidhuman.com/210#)

| 1234 |             `// 모든 레코드를 반환하는 쿼리를 실행합니다.Cursor all = myDB.query("data",` `null,` `null,` `null,` `null,` `null,` `null,` `null);            // 이름이 google인 레코드를 반환하는 쿼리를 실행합니다.Cursor sel = myDB.query("data",` `"name = google",` `null,` `null,` `null,` `null,` `null,` `null);` |
| :--- | :--- |


  
  
**데이터베이스 값을 가지는 객체, Cursors와 ContentValues**  
  
  데이터베이스 내에서 값을 추가하고, 삭제하고, 수정하는 작업돠는 별도로, 데이터베이스에 저장된 값을 코드 내로 가져와야 하거나, 코드 내에서 받은 값들을 데이터베이스에 추가시키는 과정이 있습니다. 우선, 데이터베이스의 데이터를 코드 내로 가져오는 것부터 보도록 하겠습니다.  
  
**데이터베이스 -&gt; 코드 데이터 가져오기 : Cursor**  
  
  데이터베이스에서 자료를 가져올 때는 그 자료가 특정한 값 하나 \(예:이름\)이 될 수도 있고, 레코드가 될 수도 있고, 혹은 전체 데이터가 될 수도 있습니다. 이런 자료들을 받아오기 위해서 [Cursor](http://developer.android.com/reference/android/database/Cursor.html) 인터페이스를 사용합니다.   
  커서는 쿼리\(질의\) 결과로 나온 레코드들을 가리키는, 말 그대로 마우스 "커서" 처럼 특정 레코드를 가리키는 역할을 합니다. 결과 레코드가 여러 개일 경우, 커서를 이리저리 움직이면서 여러 레코드들의 데이터들을 받아올 수 있습니다.  
  
  
![](https://t1.daumcdn.net/cfile/tistory/1765281F4A4EF51E0C)

데이터베이스에서 커서는 특정 레코드를 가리키는 역할을 합니다.

  
  
Cursor 인터페이스의 주요 메소드는 다음과 같습니다.  
  


* moveToFirst  커서가 쿼리\(질의\) 결과 레코드들 중에서 가장 처음에 위치한 레코드를 가리키도록 합니다.
* moveToNext  다음 레코드로 커서를 이동합니다.
* moveToPrevious  이전 레코드로 커서를 이동합니다.
* getCount  질의 결과값\(레코드\)의 갯수를 반환합니다.
* getColumnIndexOrThrow  특정 필드의 인덱스값을 반환하며, 필드가 존재하지 않을경우 예외를 발생시킵니다.
* getColumnName  특정 인덱스값에 해당하는 필드 이름을 반환합니다.
* getColumnNames  필드 이름들을 String 배열 형태로 반환합니다.
* moveToPosition  커서를 특정 레코드로 이동시킵니다.
* getPosition  커서가 현재 가리키고 있는 위치를 반환합니다.

  
커서에서 데이터를 받아올 때에는,  **get&lt;데이터타입&gt;\(필드 인덱스\)** 메소드를 사용합니다.  
위의 그림과 같은 질의 결과에서 이름을 받아오고 싶다면, 우선 이름 필드\(name\)의 인덱스를 알야아 합니다. 필드 인덱스는 일반적인 인덱스들과 마찬가지로 0부터 시작하므로 \_id의 필드 인덱스는 0, name은 1, phone은 2가 되겠습니다. 참고로, 위 데이터베이스의 각 필드별 데이터 타입은 \_id는 long, name은 String, phone은 long입니다.  
  
필드 인덱스는 알았고, 받아올 데이터 타입이 String이므로 현재 레코드에서 이름을 받아오기 위해서는 getString\(int ColumnIndex\)메소드를 사용하면 됩니다. 즉, getString\(1\)이 되겠죠. 만약, 이름이 아니라 전화번호를 받아오고 싶다면 getLong\(2\)을 사용하면 되겠죠?  
  
[?](http://androidhuman.com/210#)

| 1234 | `// 레코드로부터 이름을 받아옵니다.String name = result.getString(1);// 레코드로부터 전화번호를 받아옵니다.long` `phone = result.getLong(2);` |
| :--- | :--- |


  
  
다른 데이터타입을 불러오는 메소드는 [여기](http://developer.android.com/reference/android/database/Cursor.html)를 참조하세요.  
  
  
**코드 -&gt; 데이터베이스에 자료 입력하기 : ContentValues**  
  
\([android.content.ContentValues](http://developer.android.com/reference/android/content/ContentValues.html)\)  
위의 Cursor와는 반대로, 자료를 데이터베이스에 입력하기 위해서 ContentValues 객체를 데이터베이스의 레코드와 동일하게 사용합니다. ContentValues 객체에 데이터베이스 테이블에 맞게 자료를 입력한 후, SQLiteDatabase 클래스의 insert\(\)메소드를 사용하여 데이터베이스에 새로운 레코드를 추가합니다.  
  
Cursor 형태로 된 쿼리 결과에서 데이터를 가져오는 것과 비슷하게, put\(\_필드 이름\_, \_입력할 값\_\)을 이용합니다.  
  
[?](http://androidhuman.com/210#)

| 123456 | `// 필요한 데이터를 입력합니다.ContentValues newValues =` `new` `ContentValues();newValues.put("name",` `"구글");newValues.put("phone",` `"1234567");// 레코드를 추가합니다.myDB.insert("data",` `null, newValues);` |
| :--- | :--- |


  
데이터베이스에 레코드를 추가하는 메소드인 insert\(\)메소드에 대해 자세한 정보는 [여기](http://developer.android.com/reference/android/database/sqlite/SQLiteDatabase.html#insert%28java.lang.String,%20java.lang.String,%20android.content.ContentValues%29)를 참고하세요. 

출저 : http://androidhuman.com/210  


