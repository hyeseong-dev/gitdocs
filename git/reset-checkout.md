# reset, checkout명령어

Git에서는 과거로 돌아가는 reset, revert, checkout 명령어가 있어요.   
  
실습을 위해서 새로운 디렉토리를 만들고 git init 명령어를 실행한후 여러 텍스트파일을 만들고 add, commit 명령어를 우선적으로 해볼게요.   


### 준비 

```text
$ git init
$ vim f1.txt(a 입력) 
$ git add f1.txt
$ git commit -m 1 

$ vim f1.txt(b 다음줄 입력) 
$ git add f1.txt
$ git commit -m 2 

$ vim f1.txt(c 다음줄 입력) 
$ git add f1.txt
$ git commit -m 3

$ vim f1.txt(d 다음줄 입력) 
$ git add f1.txt
$ git commit -m 4
```

이제 git log 명령어로 commit 내역을 볼게요. 

```text
$ git log 
commit 0e5abd8b73920a485f443cfeaaea9651bfa68107 (HEAD -> master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:41:33 2020 +0900

    4

commit fc987de11044869766f7a7bd2ccdf1dad204da3b
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:40:38 2020 +0900

    3

commit 95c8fd7df2bc2a333592cb5d96824274ad822a17
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:40:10 2020 +0900

    2

commit 6715a500a4faa868c8553cbbd1372fa9016e0de9
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:39:44 2020 +0900

    1

```

### 최근 커밋 지우기\(reset --hard 해당 커밋 아이디\)

```text
$ git reset --hard fc98 # 커밋아이디4개만 입력해도 되요.

$ git log
commit fc987de11044869766f7a7bd2ccdf1dad204da3b (HEAD -> master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:40:38 2020 +0900

    3

commit 95c8fd7df2bc2a333592cb5d96824274ad822a17
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:40:10 2020 +0900

    2

commit 6715a500a4faa868c8553cbbd1372fa9016e0de9
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21   
```

위에서 커밋 기록이 3번이 head로 잡혀있는걸 볼 수 있어요.   
만약 실수로 4번을 날려먹은거라면 다시 또?! 돌아가야 겠조?   


## 실수로 reset ?! 돌아가자 ORIG\_HEAD

가장 최근 reset한 내역을 취소한다고 보면 되요. 

```text
$ git reset --hard orig_head $ orig_head 소문자 가능
HEAD is now at 0e5abd8 4

$ git log
commit 0e5abd8b73920a485f443cfeaaea9651bfa68107 (HEAD -> master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:41:33 2020 +0900

    4

commit fc987de11044869766f7a7bd2ccdf1dad204da3b
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:40:38 2020 +0900

    3

commit 95c8fd7df2bc2a333592cb5d96824274ad822a17
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:40:10 2020 +0900

    2

commit 6715a500a4faa868c8553cbbd1372fa9016e0de9
Author: hyeseong <hyeseong@gmail.com>
Date:   Sun Jun 21 00:39:44 2020 +0900

    1

```

### 명령어 log기록 보기 reflog

```text
$ git reflog
0e5abd8 (HEAD -> master) HEAD@{0}: reset: moving to orig_head
fc987de HEAD@{1}: reset: moving to fc98
0e5abd8 (HEAD -> master) HEAD@{2}: commit: 4
fc987de HEAD@{3}: commit: 3
95c8fd7 HEAD@{4}: commit: 2
6715a50 HEAD@{5}: commit (initial): 1

```

