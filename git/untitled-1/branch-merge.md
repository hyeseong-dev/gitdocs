# Branch merge

앞선 노트에서 branch를 말들었습니다. 이제는 병합\(합치기\)하는 방법을 알아볼게요.   


```text
$ git log --branches --graph --decorate --oneline

```

![](../../.gitbook/assets/image%20%28258%29.png)

브랜치들 상태를 확인할 수 있어요.   
위의 스샷을 요약하면 exp,master 브렌치에서 1,2commit은 공통이고   
exp브렌치는 3,4 버전으로 분기 된걸 볼 수 있어요.   
master브렌치는 버전5로 나오게 되었네요.   
  
그럼 이제 5와 4를 병합해볼게요.   
좀더 구체적으로  **b774b3e\(exp\)4==&gt;7081152\(master\)5** 이렇게 가는거에요. exp 브렌치내용을 가져다가 master에 쏟아 붇는다고 보면 되요.   
그래서 master branch commit 5에 exp 브렌치 3과 4의 내용을 갖게 만들어 준다는 의미에요.   


우선 exp --&gt; master로 merge하기 위해선 master로 checkout한 다음 master에서 merge 명령어를 입력하고 실행하게 되요. 

```text
$ git checkout master 
$ git merge exp  
```

![git merge exp ](../../.gitbook/assets/image%20%28261%29.png)

vim 에디터가 열리고 노락색 글자로 Merge branch 'exp'라는 문장이 보이네요. 다음 :wq! 키를 누르고 저장하고 나와주세요.   


```text
git log --branches --graph --decorate --online
```

![](../../.gitbook/assets/image%20%28282%29.png)

현재 master는 11467cd 커밋으로 checkout되었네요. 그리고 자동으로 작성된 commit message인 "Merge branch 'exp' " 가 보이네요.   
그리고 이 11467cd 커밋은 2개의 부모 커밋을 가져요.   
첫 번째! 원래 master 브랜가 가지고 있었던 13014a5에요. 자세히 보면 빨간줄 따라서 \*표가 이어진게 보이조?   
두 번쨰! 3번\(cb32bbc\)과 4번\(8b8db28\)을 조상과 부모로 가지게 되요.

```text
$ ls -al
total 14
drwxr-xr-x 1 이혜성 197121 0  6월 19 19:32 ./
drwxr-xr-x 1 이혜성 197121 0  6월 19 18:19 ../
drwxr-xr-x 1 이혜성 197121 0  6월 19 19:34 .git/
-rw-r--r-- 1 이혜성 197121 9  6월 19 19:32 f1.txt
-rw-r--r-- 1 이혜성 197121 0  6월 19 19:32 f2.txt
-rw-r--r-- 1 이혜성 197121 2  6월 19 17:50 f3.txt

```

f1, f2, f3 텍스트를 모두 갖게 되요. 

하지만 exp 브렌치는 3~4번은 갖고 있지만 5번은 갖고  있지 못해요.   
 그럼 exp가 master가 작업했던 5번을 가질수 있도록 해볼게요. 

```text
$ git checkout exp
$ git merge master 
$ git log --branches --graph --decorate --oneline
```

![](../../.gitbook/assets/image%20%28263%29.png)

log 기록을 통해서 exp, master브랜치가 똑같은 커밋 기록을 가지고 있는걸 확인 할 수 있어요.   
구체적으로 본다면 11467cd 커밋이 3~5번 커밋을 공통의 부모로 가지게 되었어요.   
  
그럼 더이상 exp는 사실상 필요 없게 되었어요. 

```text
$ git checkout master 
$ git branch -d exp # exp 브렌치 삭제 
$ git log --branches --graph --decorate --oneline
```

![](../../.gitbook/assets/image%20%28281%29.png)

\(head -&gt; master\) 이 부분이 master branch만 남은게 보이고 다른 곳 어디에도 exp라는 글자가 보이지 않네요. 삭제된걸 파악 할 수 있어요.   
이렇게 해서 병합\(merge\)이 무엇인지 살펴 봤어요. 

