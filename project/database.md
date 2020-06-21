# DataBase



1. 챗봇 :

   카카오랑 연동 , 크롤링 필요함 \(내용 잘몰라서 검색 해보겠음\)

   2.네이버 카페 툴

   네이버 카페등 특정사이트 에서 자신이 가입한 내용들중에서 특정 정보들 필터링

   3.기자 성향 분석

   뉴스를 보고 기자 이름을 가져와서 그 기자가 쓴글을 긁어온뒤 성향파악\(직접 or AI\)

   4.법원 경매 

   법원경매 사이트들을 취합해서 쉽게 검색 해줄수있는 플랫폼 구축

   5.작은 커뮤니티 게시판 

   고급유머 라는 어플처럼 개발자가 시간 맞춰서 올리는 커뮤티니 구축

## ERD  

![](../.gitbook/assets/image%20%28224%29.png)



### 

## \[ DB \]

* 하기 내용 작성자 - 정 : 권종범, 부: 이혜성

### 1. 테이블 정의 및 종류

#### 1-1. 정의

* 각 사이트에 해당하는 데이터베이스는 필요 없다. 해당 사이트의 인기 게시물 링크를 재구성하여 관리자 페이지를 띄우면 되기 때문.
* 게시물을 선택하여 올릴 경우에만 PostingTable에 데이터를 저장한다.
* 게시물을 올릴 때, Posting의 타이틀 300개 정도를 올릴 게시물의 제목과 비교하며 중복 검사를 진행한다.

#### 1-2. 테이블 종류

* PostingTable
  * 취합된 게시물의 데이터를 저장할 테이블
* UserTable
  * 유저 정보 테이블
* CommentTable
  * 댓글을 관리하는 테이블

#### 3. PostingTable 컬럼 예제

* No Post의 인덱스로 사용될 컬럼. \(24450\)

  혜성 : 데이터 타입- INTEGER / 키제약\(Key Constraints\) Not Null, Primary Key, Auto Increment, UNIQUE 키들을 각각 설정 송쌤 : OK

* SiteName Post를 긁어온 사이트의 이름. \("오유" or "인벤" or "루리웹" or ...\)

  혜성 : 데이터 타입- TEXT / 키 제약- NN제약 조건만 설정 송쌤 : OK

* Link Post를 긁어온 링크. \("[http://www.ppomppu.co.kr/zboard/view.php?id=humor&no=388656](http://www.ppomppu.co.kr/zboard/view.php?id=humor&no=388656)"\)

  혜성 : 데이터 타입- TEXT?, 다른걸로 할지 보류중 / 키 제약- 기존\(NN, U\) 송쌤 : OK

* Title 해당 포스트의 타이틀. \("신입사원 대참사"\)

  혜성 : 데이터 타입- TEXT / 키 제약- 기존\(NN\) 송쌤 : OK

* Content 게시물 내용
  * \(예제 생략\)

혜성 : 데이터 타입- 확인 필요? / 키 제약- 기존\(NN\) 송쌤 : 1\)이미지를 따로 저당 해도 OK, 2\)크롤링으로도 처음 생각했던 방식으로 충분히\(많은 시간과 노력없이\) 가능함.\(데이터 타입 - TEXT\)

* UploadTime

    \(0000-00-00 00:00:00\)

혜성 : 데이터 타입- 기존\(Integear\) -&gt;변경\(TEXT\) / 키 제약- 기존\(NN\) TEXT로 데이터 잡으면 조회시 소요시간이 길어진다고함. 송쌤 : 1. TEXT타입으로 충분히 가능함.\(하드웨워가 괜찮기 때문에 속도저하를 느끼는 사용자 불편함이 대형 포탈이 아닌이상 소규모 웹사이트라면 현재 문제없음\)

1. MM second방식

   \(20200606131313 방식은 비표준. 본인이 정한 개발 방식임. \)

   그래서 MMseoncd방식으로 0년0월0일0시0분0초~2020년06년06월6일 06시06분06초까지 second단위로 표현하게됨. 

   이 방식은 backend쪽에서 관련 라이브러리와 함수를 통해서 설정해야하는 표준적 방식을 사용해야함.

#### 4. UserTable 컬럼 예제

* ID 인덱스로 사용될 유저 아이디 \(...\)

  혜성 : 데이터 타입- TEXT / 키제약\(Key Constraints\) Not Null, Primary Key, Auto Increment, UNIQUE 키들을 각각 설정 송쌤 : OK

* PW 유저 패스워드 \(...\) 혜성 : 데이터 타입- TEXT / 키 제약- NN제약 조건만 설정 송쌤 : OK
* JoinDate 회원가입날짜 \(0000-00-00 00:00:00\)

  혜성 : 데이터 타입- PostingTable의 UploadTime과 동일 / 키 제약- PostingTable의 UploadTime과 동일 송쌤 : 상기 UploadDate 컬럼 내용과 동일

#### 4. CommentTable 컬럼 예제

* PostIndex PostingTable의 Index\(No\)

  혜성 : 데이터 타입- INTEAGER / 키 제약- NN, FK

* UserIndex UserTable의 Index

  혜성 : 데이터 타입- INTEAGER, UserTable의 ID컬럼을 기준 / 키 제약- NN, FK\(Foreign Key\)

* Contents 댓글 내용 \("뷰우우우우릐뿔..."\)

혜성 : 데이터 타입- TEXT / 키 제약 - NN 송쌤 :

텍스트로 댓글 기능을 먼저 완성한 후 DB, Front, Backend에서 댓글 이미지 삽입을 추가 구현 할 수 있음. 1. 텍스트 기능 1순위 2. 1순위가 완성된 후 2순위로 이미지 기능 + 텍스트

* Date 날짜 \(0000-00-00 00:00:00\)

  혜성 : 데이터 타입- TEXT / 키 제약 - NN,

  송쌤 : 상기 uploaddate와 joindate 컬럼 방식과 동일함

