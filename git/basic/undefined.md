# 저장소 생성

### Git 저장소 만들기 <a id="_getting_a_repo"></a>

주로 다음 주 가지 중 한 가지 방법으로 Git 저장소를 쓰기 시작한다.

1. 아직 버전관리를 하지 않는 로컬 디렉토리 하나를 선택해서 Git 저장소를 적용하는 방법
2. 다른 어딘가에서 Git 저장소를 _Clone_ 하는 방법

어떤 방법을 사용하든 로컬 디렉토리에 Git 저장소가 준비되면 이제 뭔가 해볼 수 있다.

#### 기존 디렉토리를 Git 저장소로 만들기 <a id="_&#xAE30;&#xC874;_&#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xB97C;_git_&#xC800;&#xC7A5;&#xC18C;&#xB85C;_&#xB9CC;&#xB4E4;&#xAE30;"></a>

버전관리를 하지 아니하는 기존 프로젝트를 Git으로 관리하고 싶은 경우 우선 프로젝트의 디렉토리로 이동한다. 이러한 과정을 처음 해보는 것이라면 시스템마다 조금 다른 점을 주의하자.

Linux:

```text
$ cd /home/user/my_project
```

Mac:

```text
$ cd /Users/user/my_project
```

Windows:

```text
$ cd /c/user/my_project
```

그리고 아래와 같은 명령을 실행한다:

```text
$ git init
```

이 명령은 `.git` 이라는 하위 디렉토리를 만든다. `.git` 디렉토리에는 저장소에 필요한 뼈대 파일\(Skeleton\)이 들어 있다. 이 명령만으로는 아직 프로젝트의 어떤 파일도 관리하지 않는다. \(`.git` 디렉토리가 막 만들어진 직후에 정확히 어떤 파일이 있는지에 대한 내용은 [Git의 내부](https://git-scm.com/book/ko/v2/ch00/ch10-git-internals)에서 다룬다\)

Git이 파일을 관리하게 하려면 저장소에 파일을 추가하고 커밋해야 한다. `git add` 명령으로 파일을 추가하고 `git commit` 명령으로 커밋한다:

```text
$ git add *.c
$ git add LICENSE
$ git commit -m 'initial project version'
```

명령어 몇 개로 순식간에 Git 저장소를 만들고 파일 버전 관리를 시작했다.

#### 기존 저장소를 Clone 하기 <a id="_git_cloning"></a>

다른 프로젝트에 참여하려거나\(Contribute\) Git 저장소를 복사하고 싶을 때 `git clone` 명령을 사용한다. 이미 Subversion 같은 VCS에 익숙한 사용자에게는 "checkout" 이 아니라 "clone" 이라는 점이 도드라져 보일 것이다. Git이 Subversion과 다른 가장 큰 차이점은 서버에 있는 거의 모든 데이터를 복사한다는 것이다. `git clone` 을 실행하면 프로젝트 히스토리를 전부 받아온다. 실제로 서버의 디스크가 망가져도 클라이언트 저장소 중에서 아무거나 하나 가져다가 복구하면 된다\(서버에만 적용했던 설정은 복구하지 못하지만 모든 데이터는 복구된다 - [서버에 Git 설치하기](https://git-scm.com/book/ko/v2/ch00/_getting_git_on_a_server)에서 좀 더 자세히 다룬다\).

`git clone <url>` 명령으로 저장소를 Clone 한다. `libgit2` 라이브러리 소스코드를 Clone 하려면 아래과 같이 실행한다.

```text
$ git clone https://github.com/libgit2/libgit2
```

이 명령은 “libgit2” 라는 디렉토리를 만들고 그 안에 `.git` 디렉토리를 만든다. 그리고 저장소의 데이터를 모두 가져와서 자동으로 가장 최신 버전을 Checkout 해 놓는다. `libgit2` 디렉토리로 이동하면 Checkout으로 생성한 파일을 볼 수 있고 당장 하고자 하는 일을 시작할 수 있다.

아래과 같은 명령을 사용하여 저장소를 Clone 하면 \`libgit2\`이 아니라 다른 디렉토리 이름으로 Clone 할 수 있다.

```text
$ git clone https://github.com/libgit2/libgit2 mylibgit
```

디렉토리 이름이 `mylibgit` 이라는 것만 빼면 이 명령의 결과와 앞선 명령의 결과는 같다.

Git은 다양한 프로토콜을 지원한다. 이제까지는 `https://` 프로토콜을 사용했지만 `git://` 를 사용할 수도 있고 `user@server:path/to/repo.git` 처럼 SSH 프로토콜을 사용할 수도 있다. 자세한 내용은 [서버에 Git 설치하기](https://git-scm.com/book/ko/v2/ch00/_getting_git_on_a_server)에서 다루며 각 프로토콜의 장단점과 Git 저장소에 접근하는 방법을 설명한다.  
  
출처 : [https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-Git-%EC%A0%80%EC%9E%A5%EC%86%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0](https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-Git-%EC%A0%80%EC%9E%A5%EC%86%8C-%EB%A7%8C%EB%93%A4%EA%B8%B0)

