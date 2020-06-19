# Branch 정보확인

## Branch 정보 확인

```text
git branch # 현재 등록된 branch 목록 확인 
```

```text
git log #해당 브렌치의 기록 확인 

$ git log
commit 8b8db28b31818c9469109b80d9db9a7f72edd07c (HEAD -> exp)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 15:13:07 2020 +0900

    4

commit cb32bbc4095e7030f5eade782a4b8018e2f65af0
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 14:30:38 2020 +0900

    3

commit b5eac942f5e38bd0e5c1bb29dc103490eecabebd (master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:57:21 2020 +0900

    2

commit 66d89f8cf905fbb019285dfca59b44b573efd626
:...skipping...
commit 8b8db28b31818c9469109b80d9db9a7f72edd07c (HEAD -> exp)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 15:13:07 2020 +0900

    4

commit cb32bbc4095e7030f5eade782a4b8018e2f65af0
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 14:30:38 2020 +0900

    3

commit b5eac942f5e38bd0e5c1bb29dc103490eecabebd (master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:57:21 2020 +0900

    2

commit 66d89f8cf905fbb019285dfca59b44b573efd626
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:56:09 2020 +0900

    1

```

## 

하지만 위 방법만으로는 master와 다른 branch log 내역을 구분하기 힘들어요.  이런 어려운 상황의 경우 아래와 같이 하면 되요. 

```text
$ git log --branches --decorate

commit 8b8db28b31818c9469109b80d9db9a7f72edd07c (HEAD -> exp) # exp 브랜치의 최근 commit 한 부분 + 그리고 현재 checkout된 브랜치를 나타내기도해요.
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 15:13:07 2020 +0900

    4

commit cb32bbc4095e7030f5eade782a4b8018e2f65af0
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 14:30:38 2020 +0900

    3

commit b5eac942f5e38bd0e5c1bb29dc103490eecabebd (master) # 이 부분까지가 master 브랜치 commit한 최근부분
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:57:21 2020 +0900

    2

commit 66d89f8cf905fbb019285dfca59b44b573efd626
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 13:56:09 2020 +0900

    1

```



위 명령어로는 브랜치간 구분이 그래도 어렵기 때문에 더 시각화 한다면. 

```text
$ git log --branches --decorate --graph 
```

![git log --branches --decorate --graph](../../.gitbook/assets/image%20%28275%29.png)

--graph 옵션을 추가하면 빨간줄이 있는  모습이 보여요.   
즉, branch가 흘러간 모습을 보여주는거에요.   
지금은 master branch == exp branch가 동일한 상태라서 구분되지 않아 그 시각적 차이가 구분되지 않아요.   
  
구분 시켜 보도록 할게요. 이제 master branch에 새로운 commit을 만들어 볼게요. 

```text
$ git checkout master
$ vim f3.txt 
a

$ git add f3.txt 
$ git commit -m 5
$ git log 
```

![1, 2, 5  &#xB0B4;&#xC5ED;&#xB9CC; &#xB098;&#xD0C0;&#xB0A8; ](../../.gitbook/assets/image%20%28271%29.png)

1, 2, 5 만 나오게 됩니다. 왜? 일까요?   
git log는 현재 brach의 commit된 내역들만 보여주게 되요. 

#### 자 그럼 모든 branches의 log 내역을 보고자 한다면? 아래처럼하세요.

```text
git log --branches 
```

![git log --branches ](../../.gitbook/assets/image%20%28269%29.png)

이 방법의 한계는 여전히 브랜치 구분이 쉽지 않아요. 

```text
git log --branches --decorate --graph
```

![git log --branches --decorate](../../.gitbook/assets/image%20%28267%29.png)

git log --branches V.S git log --branches --decorate   
뒤에 --decorate 있나 없나 차이가 없네요. 동영상에는 있다 했는데....  


#### git log --branches --decorate --graph 

![git log --branches --decorate --graph ](../../.gitbook/assets/image%20%28276%29.png)

--graph 옵션을 붙이니 분기된 branch 모습들이 명확히 보이네요. 

#### exp 브렌치의 경우 : 

최신 commit이   
4번 - 8b8db28b31818c9469109b80d9db9a7f72edd07c \(exp\) 에요.   
그 이전에는 3번 - cb32bbc4095e7030f5eade782a4b8018e2f65af0  
그리고 2번에서 비롯되었다고 나오는거조.   
  
또한 5번 master branch의 경우 5 이전의 별표인 2에 해당되요.   
  
즉, master와 exp의 공통의 조상은 2번 commit에서 분기된거에요. 



```text
git log --branches --decorate --graph --oneline
```

![--oneline &#xC635;&#xC158;](../../.gitbook/assets/image%20%28254%29.png)

git log --branches --decorate --graph --oneline 명령어를 통해서 **더 짧고 간결하게 표현된 branch들간의 commit 구조를 확인** 할 수 있어요.   
1\) commit 날짜와 작성자\(생략\)  
2\) 선도 단색으로 통일   
3\) commit id7자로 줄어



### CLI VS GUI 

![](../../.gitbook/assets/image%20%28262%29.png)

sourcetree 명령어는 GUI 프로그램\(별도 설치 필요\)으로 본인의 OS에 맞게 설치해주어야해요.   
또한 전역변수 설정도 해줘야하는거 잊지마세요.\(installer가 아닌경우\)   


![window, sourcetree ](../../.gitbook/assets/image%20%28280%29.png)

CLI환경보다 더 직관적이며 마우스 클릭만으로 해결 가능하니 선택보다 필수에 가깝지 않을까? 생각해봐요.   
물론 CLI 환경이 필요하거나 익숙한 경우도 있겠지요?!   
CLI 와 GUI 둘중 하나만 고집하지 말고 유연성있게 상황에 맞추어 사용가능한 사람이 오히려 더 버전관리를 효율적으로 한다는점 명심하세요.   


### branch간 차이점

```text
$ git log master..exp
commit 8b8db28b31818c9469109b80d9db9a7f72edd07c (exp)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 15:13:07 2020 +0900

    4

commit cb32bbc4095e7030f5eade782a4b8018e2f65af0
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 14:30:38 2020 +0900

    3

```

즉, master에는 없고 exp에는 있는 것들만 보여줘요. 

```text
$ git log exp..master
commit 13014a559db79ab957ac57204d143c676587a1a9 (HEAD -> master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 17:50:28 2020 +0900

    5


```

위의 경우는 log 브렌치에는 없고 master 브렌치에만 있는 5번 commit만 보여주게 되네요.   


### 코드까지 확인 git log -p

#### git log -p branch1..branch2

branch1에는 없고 branch2에 있는  소스코드까지 보고 싶은 경우 위 명령어를 사용하게되요. 

```text
$ git log -p exp..master
commit 13014a559db79ab957ac57204d143c676587a1a9 (HEAD -> master)
Author: hyeseong <hyeseong@gmail.com>
Date:   Fri Jun 19 17:50:28 2020 +0900

    5

diff --git a/f3.txt b/f3.txt
new file mode 100644
index 0000000..7898192
--- /dev/null
+++ b/f3.txt
@@ -0,0 +1 @@
+a
```

exp 브렌치에는 없고 오직 master 브렌치에만 있는 커밋이 5라는것과 그리고 exp에는 파일이 없는데\(--- /dev/null \) master에 있는 파일\(+++ b/f3.txt\) 을 명시한거에요.  그리고 \(+a\)라는 표시를 통해서 a 소스코드가 추가 된걸 파악 할 수 있어요. 

### git diff 

각각으 branch에 현재 상태들을 비교 할 수 있어요. 

> git diff master..exp

```text
$ git diff master..exp
diff --git a/f1.txt b/f1.txt
index 422c2b7..de98044 100644
--- a/f1.txt
+++ b/f1.txt
@@ -1,2 +1,3 @@
 a
 b
+c
diff --git a/f2.txt b/f2.txt
new file mode 100644
index 0000000..7898192
--- /dev/null
+++ /b/f2.txt
@@ -0,0 +1 @@
+a
diff --git a/f3.txt b/f3.txt
deleted file mode 10644
index 7898192..0000000
--- a/f3.txt
+++ /dev/null
@@ -1 +0,0 @@
-a

```

4번째줄이 master 5번째 줄이 exp 브렌치에요.   
7~8번째 줄을 보면 master 브렌치의 f1.txt파일은 a,b만 있는데 9번쨰 줄 exp브렌치는 c까지도 포함하여 가지고 있다는 의미에요.

16번쨰줄 +a 만 적힌 부분은 f2.txt파일에있고 exp브렌치에는 있는데 master에는 없다는걸 말해요. 

 23번째줄은 master에는 있는 20번쨰줄의 master에는 있, f3.txt가 21번째줄에서 exp브렌치에는 없다는걸 말해요\(+++ /dev/null\)

## 요약 정리 

### 수업에서 사용한 명령어

**브랜치 간에 비교할 때**

git log "비교할 브랜치 명 1".."비교할 브랜치 명 2"

**브랜치 간의 코드를 비교 할 때** 

git diff "비교할 브랜치 명 1".."비교할 브랜치 명 2"

**로그에 모든 브랜치를 표시하고, 그래프로 표현하고, 브랜치 명을 표시하고, 한줄로 표시할 때** 



출처 : [https://opentutorials.org/course/2708/15261](https://opentutorials.org/course/2708/15261)

