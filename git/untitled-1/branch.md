# Branch 만들기



```text
git init
```

git init을 하게 되면 현재 디렉토리에 저장소가 만들어져요. 

```text
vim f1.txt
```

vim에디터로 a라는 글자를 입력할게요.  그리고 !wq!를 입력하고 저장하고 나올게요. 

```text
git add f1.txt
git commit -m '커밋 메시지 입력'
```

```text
vim f1.txt

<vim editor> 
b #입력후 저장 
```

```text
git commit -a -m '2' # -a 옵션은 git add f1.txt

# 위 1번 코드의 옵션을 축약하면 -am이라고 적용해도 되요. 
git commit -am '2' 
```

#### 참고

> -a를 하게 되면 commit 하기전 자동으로 add 명령을 실행하게 되요.   
> 그런데 아직 버전 관리를 하기 전인 파일\(즉, 한 번도 add를 하지 않은\)은 자동으로 add가 되지 않아요.

```text
$ git log
commit b5eac942f5e38bd0e5c1bb29dc103490eecabebd (HEAD -> master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:57:21 2020 +0900

    2

commit 66d89f8cf905fbb019285dfca59b44b573efd626
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:56:09 2020 +0900

    1

```

2개의 버전이 생성이 되었어요.  자~ 이렇게 소스코드와 버전이 만들어 지게 되조. 그럼 우리가 만든 소스코드는 그대로 두면서 고객사에게 주기위한 소스코드들을 특별히 커스터마이징하기 위할때 브렌치 기능이 필요해요.   
  
혹은 누군가가 코드 개발을 요청하였는데 불피요한 부분만 버리고 진행하면 된다고 느낄때. 이럴때 사용할 수 있어요.   
  
지금까지 작업했던것을 서버에 반영할때! 반영하기 위한 테스트를 확인하고 문제점을 점검하는 것이 필요해요. 메인이 되는 작업과 구분하기 위한 분기 작업이 필요할때 Branch가 필요해요.   
  
위 3가지 사유 이해했나요?



우리가 처음 git을 사용할때 알게 모르게 branch를 사용해요. 바로 master 브랜치를 이용하니깐요. 

```text
$ git branch
* master

```

branch의 이름을 정해 볼게요. exp, feature등으로 접두사를 정하면 좋아요.   
즉 master&lt;-&gt;exp 사이의 서로 상호 작용을 볼게요. 

```text
$ git branch exp

$ git branch
  exp
* master

```

git branch exp 명령어 입력으로 exp 브렌치가 생성된걸 확인 할 수 있어요.

```text
$ git checkout exp
Switched to branch 'exp'
```

checkout은 대부분의 버전관리 시스템에 있는 개념이에요.   
master에 checkout하고 exp브렌치에 들어간다고 봐도 될거에요. 

```text
$ git branch
* exp
  master
```

git branch를 해보면 exp가 되고요.

```text
$ ls -al
total 13
drwxr-xr-x 1 이혜성 197121 0  6월 19 13:56 ./
drwxr-xr-x 1 이혜성 197121 0  6월 19 13:34 ../
drwxr-xr-x 1 이혜성 197121 0  6월 19 14:23 .git/
-rw-r--r-- 1 이혜성 197121 4  6월 19 13:56 f1.txt

```

f1.txt.파일이 보이게 되요. 

```text
$ git log
commit b5eac942f5e38bd0e5c1bb29dc103490eecabebd (HEAD -> exp, master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:57:21 2020 +0900

    2

commit 66d89f8cf905fbb019285dfca59b44b573efd626
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:56:09 2020 +0900

    1

```

master branch == exp branch 의 상태가 일치한걸 파악 할수 있어요.   
  


```text
vim f1.txt

<vim editor mode>
a
b
c
```

f1.txt 파일에 c 문자를 입력하여 저장해주세요. 

```text
$ git add f1.txt
warning: LF will be replaced by CRLF in f1.txt.
The file will have its original line endings in your working directory

$ git commit -m '3'
[exp cb32bbc] 3
 1 file changed, 1 insertion(+)

$ git log
commit cb32bbc4095e7030f5eade782a4b8018e2f65af0 (HEAD -> exp)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 14:30:38 2020 +0900

    3
```

