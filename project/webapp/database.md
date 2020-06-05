# DataBase



## ERD  

![](../../.gitbook/assets/image%20%28224%29.png)



### 1. 테이블 정의 및 종류

####  들어가기전 

여기서 말하는 사이트는 웹 커뮤니티\(오유, 인벤, 디시, 일베, 여시, 판, 각종 국내 커뮤니티 사이트\) 지칭.

#### 1-1. 정의

* 각 사이트에 해당하는 데이터베이스는 필요 없다. 

  * 근거 : 해당 사이트의 인기 게시물 링크를 재구성하여 관리자 페이지를 띄우면 되기 때문.

* 게시물을 선택하여 올릴 경우에만 PostingTable에 데이터를 저장한 
* 게시물을 올릴 때, Posting의 타이틀 300개 정도를 올릴 게시물의 제목과 비교하며 중복 검사를 진행한 다. 

  * 이 부분의 해결 방법으로 일단 생각나는 것이 column생성시 Key제약조건중  UNIQUE값을 두면 해결 되지 않을까 ? 



 

\|무결성 제약 조건\|역할\|  
\|:---\|:---\|  
\|NOT NULL\|칼럼에 NULL 값을 포함하지 못하도록 지정한다.\|  


|  |  |
| :--- | :--- |
|  |  |



#### 1-2. 테이블 종류

* PostingTable
  * 취합된 게시물의 데이터를 저장할 테이블
* UserTable
  * 유저 정보 테이블
* CommentTable
  * 댓글을 관리하는 테이블

#### 3. PostingTable 컬럼 예제

* No Post의 인덱스로 사용될 컬럼. \(24450\) Q.혜성 :
* SiteName Post를 긁어온 사이트의 이름. \("오유" or "인벤" or "루리웹" or ...\)
* Link

    Post를 긁어온 링크. 

    \("[http://www.ppomppu.co.kr/zboard/view.php?id=humor&no=388656](http://www.ppomppu.co.kr/zboard/view.php?id=humor&no=388656)"\)

* Title

    해당 포스트의 타이틀.

    \("신입사원 대참사"\)

* Content
* UploadTime

#### 4. UserTable 컬럼 예제

* Index
* JoinDate
* ID
* PW

#### 4. CommentTable 컬럼 예제

* PostIndex
* UserIndex
* Contents
* Date

