# stash

 stash의 어원적 정의는 '감추다, 숨겨두다'라는 의미가 있어요. 

#### branch에서 작업중인데 다른 브렌치로 checkout 해서 다른 일을 하는 경우가 발생할때, 아직 작업중이던 내용을 commit하기도 애매하고 commit하지 않으면 checkout할 수 없수없어요. 

그런 경우 stash를 이용하면 작업한 내용을 숨겨 둘수 있어요.   
head의 version으로 이동해서 현재 branch의 상태를 깔금하게 만들고 다른 branch로 checkout할 수 있어요.    
  
**단,**   
이 stash기능은 branch기능을 활발하게 사용하지 않는다면 사실은 배우지 않아도 되는 기능이에요. 그냥 알고 있다가 추후 필요할때 사용하면 좋을듯해요.\(머리속에 인지정도만\) 

```text
$ git init 
$ f1.txt ( a 입력 ) 
$ git add f1.txt 
$ git commit -m 1  
```

```text
$ git checkout -b exp # exp 브렌치를 생성하고 체크아웃까지 동시에
$ vim f1.txt
a
b

```

아직 작업이 끝나지 않았는데 checkout을 하면 어떤 문제가 생길까요?   


```text
$ git checkout master 

```

![](../../.gitbook/assets/image%20%28273%29.png)

exp에서 수정했던 내용이 master까지 영향을 주게 되요.   
다시 git checkout exp로 돌아갈게요.  여전한 모습을 status 명령어를 통해 확인 해 볼 수 있어요. 

![](../../.gitbook/assets/image%20%28281%29.png)

그럼 f1.txt를 어떻게 해야 할까요? git stash --help 명령어로 사용법을 알아볼게요. 

```text
$ git stash --help 
```

![&#xBA54;&#xB274;&#xC5BC; &#xC6F9; &#xD398;&#xC774;&#xC9C0; &#xD31D;&#xC5C5; ](../../.gitbook/assets/image%20%28278%29.png)

```text
$ git stash 
warning: LF will be replaced by CRLF in f1.txt.
The file will have its original line endings in your working directory
Saved working directory and index state WIP on exp: 2441228 1

```

4번째 줄을 보면 working directory와 WIP\(working in process\)인 exp 브렌치 인덱스가 저장 되었다는 문구를 볼 수 있어요.   
즉, 우리의 워킹디렉토리와 작업중인 변경사항들이 저장 되었다는 말이에요. 

```text
$ git status 
On branch exp
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        common.txt
        exp.txt
        master.txt

nothing added to commit but untracked files present (use "git add" to track)
```

맨 마지막 9번째줄을 보게 되면 nothing to commit 이라는 문구가 보여요 이말은 commit할 것들이 없다는 말이에요.  그럼 이 상태에서   
git checkout master 명령어를 사용하면 

```text
$ git checkout master
```

master branch에서 작업을 마음 편하게 할 수  있게 되는 거에요. 이후 다시 git checkout exp로 돌아온 다음 master로 checkout 하기 이전 작업 내역들을 다시 불러서 할 수 있어요. 

```text
$ git stash apply
```

![](../../.gitbook/assets/image%20%28253%29.png)

그럼 아래 modified: f1.txt 라는 문구가 보일거에요. stash로 감춰줬던 사항들이 다시 적용되서 살아난거에요. 

```text
$ git stash list
stash@{0}: WIP on exp: 2441228 1
```

```text
$ git reset --hard HEAD 
# 가장 최신 커밋 상태로 만드는건데, 다 지우는거에요. 
nothing added to commit but untracked files present (use "git add" to track)
```

```text
$ git stash list
stash@{0}: WIP on exp: 2441228 1

# 여전히 stash 이력이 남아  있어요. 

$ git stash apply 
On branch exp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   f1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        common.txt
        exp.txt
        master.txt

no changes added to commit (use "git add" and/or "git commit -a")

```



```text
$ git reset --hard 
HEAD is now at 2441228 1

$ git stash apply
On branch exp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   f1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        common.txt
        exp.txt
        master.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

특히 git stash를 명시적으로 삭제하지 않는 이상 항상 살아 있어요. 

```text
$ git stash list 
stash@{0}: WIP on exp: 2441228 1
```

그리고 현재 수정된 내역을 다시 reset 해볼게요. 

```text
$ git reset --hard
HEAD is now at 2441228 1
$ vim f2.txt(a 입력) 
$ git add f2.txt
$ git stash 
Saved working directory and index state WIP on exp: 2441228 1

$ git status 
On branch exp
nothing to commit, working tree clean

$ git stash list
stash@{0}: WIP on exp: 2441228 1
stash@{1}: WIP on exp: 2441228 1

```

13번째 줄의 git stash의 내역은 5번째줄에 처리한 git stash를 가리키게 되요.  그렇다면 14번째 줄은 그 이전에 stash한 내역을 말하겠조?  
그래서 만약 git stash apply 명령어를 그냥 적용하면 git stash list의 0번째를 적용시켜요.   
  
그럼 만약 stash list의 내역을 0번째부터 순차적으로 적용하고자 한다면 어떻게 해야할까요? 아래와 같이 해볼게요. 

```text
$ git stash apply # 가장 최근(0번째) stash 리스트 내역 적용! 
$ git stash drop  # 가장 최근(0번째) 리스트 삭제 
Dropped refs/stash@{0} (b0de4a37c4cb3e9f2b105f4cd4c0b4394d15a

$ git stash apply; git stash drop; # 2개의 명령 수행 
```

5번째 줄  적용과 삭제를 한번에 하게 되요.   
위 방식은 그래도 뭔가 여러번 반복하는 작업이 있네요. 한번에 해결하는 방법을 알아볼게요. 우선 status 명령어로 상태부터 확인해 볼게요. 

```text
$ git status
On branch exp
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   f2.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   f1.txt

```

깔끔하게 지울게요. 

```text
$ git reset --hard
HEAD is now at 2441228 1

$ git status
On branch exp
nothing to commit, working tree clean

$ vim f1.txt( b추가 입력 ) 
$ git add f1.txt 
$ git stash 
Saved working directory and index state WIP on exp: 2441228 1

$ git status 
On branch exp
nothing to commit, working tree clean

```

10번째 stash 명령어로 감춰지고 11번째 줄의 status 명령어로 상태가 어떤지 바로 확인 가능해요.   
이상태에서 아래 명령어를 실행해 볼게요. 

```text
$ git stash pop # == git stash apply; git stash drop;동일
```



#### 단 stash 기능은 최소한 버전관리를 하는 파일들만 이 기능을 사용할 수 있어요. 

아래를 살펴 볼게요.

```text
$ git reset --hard 
HEAD is now at 2441228 1

$ vim f1.txt(a입력, 이미 있다면 b입력후 저장) 
$ vim f2.txt(a 입력) 

$ git status
On branch exp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   f1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        f2.txt

no changes added to commit (use "git add" and/or "git commit -a")

```

12번째 줄에서 modified: f1.txt라는거 보이조?   
tracked되고 있다는 말이에요. 추적되고 있는 파일이에요.   
  
하지만 14번째 줄에서 Untracked files: ~~~~~f2.txt 가 보이조?  
즉 추적되고 있지 않은 파일이에요.   
  
자! 이상태로 git stash를 하게될 경우. 

```text
$ git stash 
$ git status 
On branch exp
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        f2.txt

nothing added to commit but untracked files present (use "git add" to track)
```

f2.txt는 추적되고 있지 않기 때문에 stash 기능을 적용 받을 수 없어요.   
그래서 최소한 버전관리를 받고 있는 파일에서만 stash를 한다는것도 기억해 두어야 할 사항이에요. 











