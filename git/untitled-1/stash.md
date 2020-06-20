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

![](../../.gitbook/assets/image%20%28272%29.png)

exp에서 수정했던 내용이 master까지 영향을 주게 되요.   
다시 git checkout exp로 돌아갈게요.  여전한 모습을 status 명령어를 통해 확인 해 볼 수 있어요. 

![](../../.gitbook/assets/image%20%28280%29.png)

그럼 f1.txt를 어떻게 해야 할까요? git stash --help 명령어로 사용법을 알아볼게요. 

```text
$ git stash --help 
```

![&#xBA54;&#xB274;&#xC5BC; &#xC6F9; &#xD398;&#xC774;&#xC9C0; &#xD31D;&#xC5C5; ](../../.gitbook/assets/image%20%28277%29.png)

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

맨 마지막 9번째줄을 보게 되면 nothing to commit 이라는 문구가 보여요 이말은 commit할 것들이 없다는 말이에요. 



















