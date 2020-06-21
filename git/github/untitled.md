---
description: 원격 저장소 생성
---

# remote repository

### 이미 저장소가 생성된 경우 

github에서 막 원격 저장소를 생성한 경우 아래와 같은 소스 코드를 입력할 수 있어요. 

```text
$ git remote add origin https://github.com/osori-magu/gitfth.git
$ git remote -v 
```

git remote 깃의 원격 저장소를 의미하고요. add는 더한다는 의미에요.   
원격 저장소를 더할거다. 그런데 어떤 원격 저장소? origin이라는 master branch를 가진  원격 저장소를 더한다는 말이에요. 뒤에 주소는 해당 원격 저장소의 github website의 server를 가키게 되요. 



```text
$ git remote 
origin 
```

origin이라는 원격 저장소가 있네요. 

```text
$ git remote -v 
origin  https://github.com/osori-magu/gitfth.git (fetch)
origin  https://github.com/osori-magu/gitfth.git (push)
```

-v 옵션을 더하면 더 상세한 저장소의 서버 주소까지 알수 있어요.   
1\) 그런데 origin이라는 이름말고 다른 이름으로 애초에 만들수는 없을까요?  
혹은 2\) 추가로 다른 이름의 원격 저장소를 만들고 그리고 그 저장소의 서버는 위의 서버 주소와 동일하게 할 수 없을까요?   


가능해요. 아래를 보시조 . 

```text
$ git remote add friend https://github.com/osori-magu/gitfth.git

$ git remote -v
friend  https://github.com/osori-magu/gitfth.git (fetch)
friend  https://github.com/osori-magu/gitfth.git (push)
origin  https://github.com/osori-magu/gitfth.git (fetch)
origin  https://github.com/osori-magu/gitfth.git (push)

```

friend라는 이름의 원격 저장소를 가지고 있고 동일한 서버주소를 가지게 되었네요. 

#### 로컬에 등록된 원격 저장소 삭제 

```text
$ git remote remove friend # 로컬 등록된 원격 저장소 삭제 

```



###  git push 

```text
$ git push -u origin master # 처음 push할떄 쓰임 
$ git push                  $ 2번째 push할때는 git push만 사
```

항상 기준은 local 저장소 -&gt; remote\(원격\) 저장소로 push or pull하는 입장이에요.   
그래서 위 문장은 로컬\(master branch\)에서 origin\(원격저장소\)로 현재 파일과 폴더들을 밀어\(upload\)하겠다는 말이에요. 

> git push 할때 아이디, 비번 입력하라고 뜨는데 입력하면 되요.

2번째는 git push 명령어는 local과 remote 저장소를 이미 연결 시켰다면 두 단어만 적고 실행하면 간편하게 원격 저장소에 업로드 할 수 있어요. 



### git clone 

```text
 $ cd ..
 $ mkdir gitfth2 
 $ git clone https://github.com/osori-magu/gitfth.git
```

하나의 원격 저장소에 2개의 지역 저장소를 연결 할 수 있어요. 



















