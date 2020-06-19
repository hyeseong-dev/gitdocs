# Branch 정보확인

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

commit 8b8db28b31818c9469109b80d9db9a7f72edd07c (HEAD -> exp) # exp 브랜치의 최근 commit 한 부분 + 현재 checkout된 브랜치를 나타내기도해요.
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

아

## 

## 요약 정리 

### 수업에서 사용한 명령어

**브랜치 간에 비교할 때**

git log "비교할 브랜치 명 1".."비교할 브랜치 명 2"

**브랜치 간의 코드를 비교 할 때** 

git diff "비교할 브랜치 명 1".."비교할 브랜치 명 2"

**로그에 모든 브랜치를 표시하고, 그래프로 표현하고, 브랜치 명을 표시하고, 한줄로 표시할 때** 



출처 : [https://opentutorials.org/course/2708/15261](https://opentutorials.org/course/2708/15261)

