# Create & Connect

## DB 생성과 생성한 DB에 연경 하기 

## 실습 

### 1. 접속하자마자 DB생성

```text
PS C:\Workspace\db_practice> sqlite3 userinfo.sqlite3
SQLite version 3.32.1 2020-05-25 16:19:56
Enter ".help" for usage hints.
```

userinfo.sqlite3 데이터베이스가 존재하지 않으면 새로운 데이터베이스 userinfo.sqlite3가 생성되고 생성된 데이터베이스에 바로 연결  


### 2. 테이블 생성 후 DB 접속 종

```text
sqlite> create table customer (id, name);
sqlite> .exit
```

### 3. 기존 테이블 확인 

```text
PS C:\Workspace\db_practice> sqlite3 .\userinfo.sqlite3
SQLite version 3.32.1 2020-05-25 16:19:56
Enter ".help" for usage hints.
sqlite> .tables
customer
```

