# 기본

## Database\(DBMS\)

#### DDL\(Data Definition Language\) & DML\(Data Manipulation Language\)

#### Column & Row

#### Table, View, Trigger, Procedure

#### Database & Server & Daemon Process

#### Transaction, Lock, Index\(Primary, Foreign, Unique, Index\)

#### Object\(Account, Host\)

#### RDBMS, ORDBMS, NoSQL and in-memory DB

----

sqlite3가 대표적으로 관계형 DB RDBMS를 의미해요. 여기서 말하는 **관계형은** 

  
학생이라는 저장소와 클럽이라는 저장소 2개가 있으면   
동아리의 리더와 학생간에 관계를 말하는거에요. 

&lt;hr/&gt;  


## Sqlite 

* From August 2000\(current version 3.32.3\) 
* Fast & Embeded Relational Database
* File based Processing \( 1 Database == 1 File \) 
* Transaction with Backup File 
* Default Includes In Android, iOS, Mac, Python, etc. 
* Sqlite3\(2004\) \_ UTF-\*, UTF-16, Blob, 64-bit  

 데이터베이스 하나가 바로 파일이 되요.   
BLOB는 이미지, 동영상과 같은 대용량 파일까지 처리가 가능해요. 

  


![](../../../.gitbook/assets/image%20%28320%29.png)

sqlite-tools-win32-x86 압축 파일을 설치해주세요.   
1\) System32 폴더에 압축된 파일 3개를 풀어주세요. 그럼 sqlite3 명령어가 어느 디렉토리에서든지 실행할수 있어요.   
2\) 아니면 본인이 원하는 특정 working directory 구역에 폴더를 만들고 설치해주시고 해당 워킹 디렉토리를 전역변수로 설정해주시면 어디에서든 실행 가능한 상태가 되요.   






