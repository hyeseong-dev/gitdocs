# git add, commit, push 취소

### .gitignore을 설정하지 않고 github remote에 push한 경우



### Goal <a id="goal"></a>

> * github에 잘못 올라간 파일을 삭제할 수 있다.
> * .gitignore을 설정하지 않고 github remote에 push한 경우, 잘못 올라간 파일을 삭제할 수 있다.



**들어가기 전**

예를 들어, IntelliJ IDE를 사용할 때 .out 폴더를 .gitignore에 넣지 않고 원격 저장소에 push했다고 가정하자. \(_IntelliJ의 .out 폴더:_ 빌드/컴파일 시 .class 파일이 포함된 프로젝트의 출력이 포함되는 위치\)  


### git add 취소하기\(파일 상태를 Unstage로 변경하기\) <a id="git-add-&#xCDE8;&#xC18C;&#xD558;&#xAE30;&#xD30C;&#xC77C;-&#xC0C1;&#xD0DC;&#xB97C;-unstage&#xB85C;-&#xBCC0;&#xACBD;&#xD558;&#xAE30;"></a>

* 아래와 같이 실수로 git add \* 명령을 사용하여 모든 파일을 Staging Area에 넣은 경우,
* Staging Area\(git add 명령 수행한 후의 상태\)에 넣은 파일을 빼고 싶을 때가 있다.
* ```text
  // 모든 파일이 Staged 상태로 바뀐다.
  $ git add *
  // 파일들의 상태를 확인한다.
  $ git status
  On branch master
  Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    renamed:    README.md -> README
    modified:   CONTRIBUTING.md
  ```

이때, git reset HEAD \[file\] 명령어를 통해 git add를 취소할 수 있다.

* 뒤에 파일명이 없으면 add한 파일 전체를 취소한다.
* CONTRIBUTING.md 파일을 Unstaged 상태로 변경해보자.
* ```text
  // CONTRIBUTING.md 파일을 Unstage로 변경한다.
  $ git reset HEAD CONTRIBUTING.md
  Unstaged changes after reset:
  M	CONTRIBUTING.md
  ```
* ```text
  // 파일들의 상태를 확인한다.
  $ git status
  On branch master
  Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
    renamed:    README.md -> README
  Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   CONTRIBUTING.md
  ```

### git commit 취소하기 <a id="git-commit-&#xCDE8;&#xC18C;&#xD558;&#xAE30;"></a>

#### commit 취소하기 <a id="commit-&#xCDE8;&#xC18C;&#xD558;&#xAE30;"></a>

* 완료한 commit을 취소해야 할 때가 있다.
  1. 너무 일찍 commit한 경우
  2. 어떤 파일을 빼먹고 commit한 경우 이때, git reset HEAD^ 명령어를 통해 git commit을 취소할 수 있다.

     ```text
     // commit 목록 확인
     $ git log
     ```

     ```text
     // [방법 1] commit을 취소하고 해당 파일들은 staged 상태로 워킹 디렉터리에 보존
     $ git reset --soft HEAD^
     // [방법 2] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에 보존
     $ git reset --mixed HEAD^ // 기본 옵션
     $ git reset HEAD^ // 위와 동일
     $ git reset HEAD~2 // 마지막 2개의 commit을 취소
     // [방법 3] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에서 삭제
     $ git reset --hard HEAD^
     ```

#### commit message 변경하기 <a id="commit-message-&#xBCC0;&#xACBD;&#xD558;&#xAE30;"></a>

* commit message를 잘못 적은 경우, git commit –amend 명령어를 통해 git commit message를 변경할 수 있다.

  ```text
  $ git commit --amend
  ```

**TIP git reset 명령은 아래의 옵션과 관련해서 주의하여 사용해야 한다.**

* reset 옵션
  * **–soft** : index 보존\(add한 상태, staged 상태\), 워킹 디렉터리의 파일 보존. 즉 모두 보존.
  * **–mixed** : index 취소\(add하기 전 상태, unstaged 상태\), 워킹 디렉터리의 파일 보존 **\(기본 옵션\)**
  * **–hard** : index 취소\(add하기 전 상태, unstaged 상태\), 워킹 디렉터리의 파일 삭제. 즉 모두 취소.

**TIP 만약 워킹 디렉터리를 원격 저장소의 마지막 commit 상태로 되돌리고 싶으면, 아래의 명령어를 사용한다.**

* 단, 이 명령을 사용하면 원격 저장소에 있는 마지막 commit 이후의 워킹 디렉터리와 add했던 파일들이 모두 사라지므로 주의해야 한다.

  ```text
  // 워킹 디렉터리를 원격 저장소의 마지막 commit 상태로 되돌린다.
  $ git reset --hard HEAD
  ```

### git push 취소하기 <a id="git-push-&#xCDE8;&#xC18C;&#xD558;&#xAE30;"></a>

* 이 명령을 사용하면 자신의 local의 내용을 remote에 강제로 덮어쓰기를 하는 것이기 때문에 주의해야 한다.
  * 되돌아간 commit 이후의 모든 commit 정보가 사라지기 때문에 주의해야 한다.
  * 특히, 협업 프로젝트에서는 동기화 문제가 발생할 수 있으므로 팀원과 상의 후 진행하는 것이 좋다.

1. 워킹 디렉터리에서 commit 되돌린다.
   * 가장 최근의 commit을 취소하고 워킹 디렉터리를 되돌린다.
   * ```text
     // 가장 최근의 commit을 취소 (기본 옵션: --mixed)
     $ git reset HEAD^
     ```
   * 원하는 시점으로 워킹 디렉터리를 되돌린다.
   * ```text
     // Reflog(브랜치와 HEAD가 지난 몇 달 동안에 가리켰었던 커밋) 목록 확인
     $ git reflog 또는 $ git log -g
     // 원하는 시점으로 워킹 디렉터리를 되돌린다.
     $ git reset HEAD@{number} 또는 $ git reset [commit id]
     ```
2. 되돌려진 상태에서 다시 commit을 한다.

   ```text
   $ git commit -m "Write commit messages"
   ```

3. 원격 저장소에 강제로 push 한다.

   ```text
   $ git push origin [branch name] -f
   또는
   $ git push origin +[branch name]
   ```

   ```text
   // Ex) master branch를 원격 저장소(origin)에 강제로 push
   $ git push origin +master
   ```

**TIP 경고를 무시하고 강제로 push 하기**

* \[방법 1\] -f 옵션
  * –force 옵션과 동일하다.
* \[방법 2\] +\[branch name\]
  * 해당 branch를 강제로 push한다.

### untracked 파일 삭제하기 <a id="untracked-&#xD30C;&#xC77C;-&#xC0AD;&#xC81C;&#xD558;&#xAE30;"></a>

git clean 명령은 추적 중이지 않은 파일만 지우는 게 기본 동작이다. 즉, .gitignore 에 명시하여 무시되는 파일은 지우지 않는다.

```text
$ git clean -f // 디렉터리를 제외한 파일들만 삭제
$ git clean -f -d // 디렉터리까지 삭제
$ git clean -f -d -x // 무시된 파일까지 삭제
```

**TIP option**

* -d 옵션
  * 디렉터리까지 지우는 것
* -x 옵션
  * 무시된 파일\(.DS\_Store나 .gitignore에 등록한 확장자 파일들\)까지 모두 지우는 것
  * Ex\) .o 파일 같은 빌드 파일까지도 지울 수 있다.
* -n 옵션
  * 가상으로 실행해보고 어떤 파일들이 지워질지 알려주는 것
  * ![](https://gmlwjd9405.github.io/images/git-add-cancel/n-option.png)

## 관련된 Post <a id="&#xAD00;&#xB828;&#xB41C;-post"></a>

* .gitignore을 설정하지 않고 github remote에 push한 경우, [Github에 잘못 올라간 파일 삭제하기](https://gmlwjd9405.github.io/2018/05/17/git-delete-incorrect-files.html)를 참고하시기 바랍니다.

