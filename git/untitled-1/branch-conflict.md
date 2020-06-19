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
$ git log --branches --decorates --graph
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

merge commit 메시지는 별것 없으니 !wq 누르고 저장하며 나갈게요. 

![&#xB450;&#xAC1C;&#xC758; branch &#xBCD1;&#xD568;&#xB41C; &#xBAA8;&#xC2B5; ](../../.gitbook/assets/image%20%28286%29.png)

![ls -al &#xBA85;&#xB839;&#xC5B4; ](../../.gitbook/assets/image%20%28279%29.png)

원래 exp 브렌치에 있던 exp.txt파일이 master 브렌치에 옮겨간 모습 잘 보이조?

## 

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


