# Branch Conflict

branch merge 시, git이 처리하는 작업이 무엇인지 파악하고 자동으로 병합하는 1차적인 방법이 안될 경우 2차적으로 접근하는 수동 방법이 무엇인지 파악해볼게요. 

```text
$ git branch exp 
fatal: A branch named 'exp' already exists. 
```

기존 동일명의 브렌치가 있다면 아래와 같이 삭제할게요. 

```text
$ git branch -d exp 
error: The branch 'exp' is not fully merged. 
if you are sure you want to delete it, run 'git branch -D exp'
```

오류가 발생했는데, 오류 지침에 확실히 지우는 방법을 알려주네요. 바로 기존 -d 옵션 대신 -D 옵션을 적용하는거에요.   


```text
$ git branch -D exp 
Deleted branch exp (was bd8999e). 
# 정상적으로 해당 브렌치가 완벽히 삭제 되었어요. 

```

```text
$ git branch exp # exp 브렌치 생성 
$ git checkout master
$ vim master.txt (안의 내용은 a 입력) 
$ git add master.txt 
$ git commit -m '6' 
$ git checkout exp
$ vim exp.txt(내용은 a 입력) 
$ git add exp.txt
$ git commit -m '7'
$ git checkout master 

```

```text
$ git log --branches --decorate --graph
```

위 명령어를 입력하면 아래와 같이 결과가 나오게 되요. 

![](../../.gitbook/assets/image%20%28267%29.png)

이 상태에서 git merge exp를 할 경우 커밋한 부분이 각자 단독적으로 있었기에 merge commit을 생성하게 되요. 

```text
Merge branch 'exp'
# Please enter a commit message to explain why this merge is necessary,
# especially if it merges an updated upstream into a topic branch.
#
# Lines starting with '#' will be ignored, and an empty message aborts
# the commit.
~
~

```

혹시 vim editorㅇ서 merge commit 메시지가 나타난다면 별것 없으니 :wq! 누르고 저장하며 나갈게요. 

![&#xB450;&#xAC1C;&#xC758; branch &#xBCD1;&#xD568;&#xB41C; &#xBAA8;&#xC2B5; ](../../.gitbook/assets/image%20%28289%29.png)

![ls -al &#xBA85;&#xB839;&#xC5B4; ](../../.gitbook/assets/image%20%28282%29.png)

원래 exp 브렌치에 있던 exp.txt파일이 master 브렌치에 옮겨간 모습 잘 보이조? 즉, 파일이 다르면 무조건 자동으로 병합 되요.  하지만 파일이 같으면 문제가 발생해요. 

이제 master 브렌치와 exp 브렌치의 같은 파일 이름을 병합해 볼게요.   
exp 브렌치로 checkout하고 common.txt파일을 생성한 다음 commit하고 master 브렌치로 돌아와서 exp의 내용을 merge시켜서 양쪽다 똑같은 파일을 갖게 해볼게요. 

```text
$ git checkout exp  
$ vim common.txt( function a() {} 입력 )
$ git add common.txt
$ git commit -m "8"
$ git checkout master 
$ git merge exp 
```

```text
$ ls -al
total 17
drwxr-xr-x 1 이혜성 197121  0  6월 20 16:45 ./
drwxr-xr-x 1 이혜성 197121  0  6월 20 00:45 ../
drwxr-xr-x 1 이혜성 197121  0  6월 20 16:45 .git/
-rw-r--r-- 1 이혜성 197121 17  6월 20 16:45 common.txt
-rw-r--r-- 1 이혜성 197121  3  6월 20 05:00 exp.txt
-rw-r--r-- 1 이혜성 197121  9  6월 19 19:32 f1.txt
-rw-r--r-- 1 이혜성 197121  0  6월 19 19:32 f2.txt
-rw-r--r-- 1 이혜성 197121  3  6월 19 22:46 f3.txt
-rw-r--r-- 1 이혜성 197121  3  6월 20 16:45 master.txt
```

exp branch에서 생성한 common.txt 파일이 master 브렌치에서도 동일하게 생성되었네요. 

```text
$ vim common.txt(function b(){} 내용을 기존 내용 앞에 붙임)
$ git commit -am "9" 
$ git checkout exp 
$ vim common.txt( function c(){} 내용을 붙임 ) 
$ git commit -am "10"
$ git checkout master 
```

이 상태는 common.txt 파일을 브렌치마다 다른 부분을 수정했어요.   
이 상태에서 

```text
$ git merge exp 
$ vim common.txt 
```

```text
# master branch, common.txt 

function b() {}
function a() {}
function c() {}
```

### 같은 파일 다른 부분 수정시 

같은 파일이라도 수정한 위치가 다르면 자동으로 합쳐지게 되요. 

### 같은 파일 동일 부분 수정시 

현재 master 브렌치의 common.txt 내용을 보면 

```text
$ cat common.txt 
function b() {} 
function a() {} 
function c() {} 
$ git checkout exp 

```

```text
cat common.txt 
function a() {}
function c() {}
```

```text
$ git merge master

$ cat common.txt
function b() {}
function a() {} 
function c() {} 


```

```text
$ git checkout master 
$ vim common.txt
function b() {}
function a(master) {} 
function c() {} 

$ git commit -am '11'
$ git checkout exp 
$ vim common.txt
function b() {}
function a(exp) {} 
function c() {} 
```

동일 파일의 같은 부을 수정하면 어떻게 될지 알아보는거에요. 

```text
$ git commit -am '12' 
$ git checkout master 
$ git merge exp 
Auto-merging common.txt
CONFLICT (content): Merge conflict in common.txt
Automatic merge failed; fix conflicts and then commit the result.

$ git status 
On branch master
You have unmerged paths. 
 (fix conflicts and run "git commit")
 
 Unmerged paths: 
   ( use 'git add <file>...' to mark resolution)
   
        both modified: common.txt 
 
 no changes added to commit (used "git add" and /or "git commit -a ")
 
```

```text
vim common.txt

function b() {}
<<<<<<<<< HEAD
function a(master) {}
=========
function a(exp) {}
>>>>>>>>> exp
function c() {}


```

바로 위 소스코드 6번째줄의 ========== 구분자를 중심으로 위쪽의 &lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD부분이 현재 우리가 checkout한 브레친의 부분을 나타내고요.   
&gt;&gt;&gt;&gt;&gt; exp 부분이 exp 브렌치 common.txt에서 작업한 내역을 나타내요.   
결국 이게 말하는 바는 깃이 자동으로 병합하는 것이 실패했기 때문에 merge를 시도한 우리가 이를 해결하라는 신호를 준거에요.   
  
이 신호를 바탕으로 병합 문제를 해결해야 해요.   
우리는 이를 원하는 방향으로 수정해 볼게요. 

```text
# master branch/vim common.txt

function b() {}
function a(master, exp) {}
function c() {}
```

```text
$ git add common.txt 
$ git status 
On branch master 
All conflicts fixed but you are still merging. 
(use 'git commit' to conclude merge) 
changes to be committed: 
        modified: common.txt

```

```text
$ git commit 
```

commit 내역들에 상세 내역을 볼수 있는 vim 에디터 모드로 전환되고. 다시 저장하고 나와주세요. 

```text
$ git log 
$ vim common.txt 
function b() {}
function a(master,exp) {}
function c() {}
```

정상적으로 잘 반영된 모습들을 확인 할 수 있어요. 



































## 오류 유도 

#### master & exp 브렌치에 같은 파일 생성하기 

## 

## 

## 

## 요약 

**충돌이 일어났을 때** 

충돌이 생기면 아래와 같은 메시지가 뜹니다. 

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5123.png)

git status를 하면 충돌이 일어난 파일을 찾을 수 있습니다. 

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5125.png)

 충돌이 발생한 파일을 수정합니다. 아래와 같습니다. 

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5126.png)

'&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD' 부터 '=======' 사이의 구간이 현재 체크 아웃된 파일의 내용이고 '=======' 부터 '&gt;&gt;&gt;&gt;&gt;&gt;&gt; exp' 사시의 구간이 병합하려는 대상인 exp 브랜치의 코드 내용입니다.  이 정보를 참고로해서 두개의 코드를 병합한 후에 특수기호들을 제거해주시면 됩니다. 작업이 끝나면 파일을 저장.

충돌 작업을 끝냈다는 것을 깃에게 알려줍니다. 

| 1 | `git add` `'conflicted file name'` |
| :--- | :--- |


