# git 사용법\(SourceTree\)

Git을 이용하려면 두가지 방법이 있다.

* **SourceTree**라는 Git GUI 툴을 이용한 Git
* **Git Bash**를 이용한 Git

SourceTree를 이용하면 GUI 툴이기에 접근하기에는 편하지만, 리눅스는 지원이 안되고 좀 더 디테일한 명령어를 다룰 수 없다. 따라서 보기엔 불편하지만 Git Bash를 이용하는 것이 낫다고 생각한다. \(그리고 얘가 좀 더 간지난다\)

지금부터 첫번째 방법에 대해서 알아보자.

### 1. Git & SourceTree 설치

* Git 설치 : [https://git-scm.com/](https://git-scm.com/)
* SourceTree 설치 : [https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/)

### 2. 테스트할 저장공간 만들기

Git과 SourceTree를 연동하여 소스를 관리하려면, 테스트할 저장공간이 필요하다. 내 경우는 C:\gbsb\project1 폴더에 index.html이라는 파일을 만들었다. 

\[index.html\]

| &lt;html&gt;    &lt;head&gt;        &lt;title&gt;Git&lt;/title&gt;    &lt;/head&gt;     &lt;body&gt;        &lt;ul&gt;            &lt;li&gt;Hello Git!&lt;/li&gt;        &lt;/ul&gt;    &lt;/body&gt;&lt;/html&gt; |  |
| :--- | :--- |


### 3. 새 저장소 만들기\(init 명령어\)

이제 SourceTree을 열어보자. 지금부터 SourceTree에서 Git에게 추적당할 로컬 저장소를 만들 것이다.

![](https://t1.daumcdn.net/cfile/tistory/26254244596FC1BD23)

아래는 저장소가 만들어진 모습이다.

![](https://t1.daumcdn.net/cfile/tistory/212DFF46597022DD10)

노란색으로 표시한 부분은 Git과 이것저것 연동하는 부분이고, 빨간색으로 표시한 부분은 C:\gbsb\project1 저장소의 안에 있는 파일들을 보여준다.

Staging Area는 Git에게 추적되는 공간이고, Working Directory는 Git에게 추적되지 않는 공간이다. 현재 워킹 디렉토리에는 아직 추적되지 않은 index.html 이 보인다.

![](https://t1.daumcdn.net/cfile/tistory/2724A033596FC62816)

이 아이콘은 새로운 파일이 등록되었을 경우다. \(아직 Git이 추적하기 전\)

![](https://t1.daumcdn.net/cfile/tistory/22306F33596FC62916)

이 아이콘은 새로운 파일은 최초로 커밋하면 Git이 추적을 시작한다. \(즉 저장소에 저장된다\)

> **아직까지 Git은 이 디렉토리 안의 파일의 내용이 변경되었는지 추적하지 않는다.**

### 4. 버전 만들기\(commit 명령어\)

처음으로 커밋을 시도한다면, 계정을 입력하라는 알림이 뜰 것이다. \[Tools\] &gt; \[Options\] &gt; Dafault user infomation에서 계정을 추가한 뒤, 아래의 단계를 실행하여 커밋해보자.

![](https://t1.daumcdn.net/cfile/tistory/2313D14C596FC9B61F)

이제 커밋이 완료되었다. 왼쪽엔 master브랜치가 생성되었고, 오른쪽엔 커밋할 때 작성한 이력, 날짜 등이 보여진다.

![](https://t1.daumcdn.net/cfile/tistory/2215E847596FCA952A)

이번에는 소스파일을 변경한 후 커밋해보자. 나는 index.html 파일에 한 줄을 추가하고 저장하였다.

\[index.html\]

| &lt;html&gt;    &lt;head&gt;        &lt;title&gt;Git&lt;/title&gt;    &lt;/head&gt;     &lt;body&gt;        &lt;ul&gt;            &lt;li&gt;Hello Git!&lt;/li&gt;            **&lt;li&gt;Add Source~~&lt;/li&gt;**        &lt;/ul&gt;    &lt;/body&gt;&lt;/html&gt; |  |
| :--- | :--- |


그 다음에 소스트리 목록을 보면 'Uncommitted changes', 즉 커밋되지 않은 변화가 추가되었다. \(안보일 경우 F5 새로고침\) 이번에도 아까와 같은 방식으로 커밋을 하면 된다.![](https://t1.daumcdn.net/cfile/tistory/210FB142596FCC4F2F)

> **커밋을 하니, 저장소로 등록한 C:\gbsb\project1 내의 파일들이 Git에게 추적되어 보여지고 있다.**

### 5. 되돌리기\(discard, reset, revert 명령어\)

작성한 파일을 다시 되돌릴 수 있는 3개의 방법이 있다. \(파일을 되돌려보기 위해 index.html 파일에 이것저것 내용을 변경하려고 한다.\)

#### 1\) **Discard** \(커밋하기 전, 되돌리기\)

Staging Area 목록에서 되돌릴 파일을 선택한 뒤 \[Discard\] 버튼을 클릭하면 창이 뜬다. \[Discard Changes\] 버튼을 클릭하면 최종 커밋된 버전으로 돌아간다.

#### 2\) **Reset** \(커밋해버린 후, 버전을 제거하고 되돌리기\)

목록에서 되돌아가고 싶은 버전을 선택하고 마우스 우클릭한 뒤, 'Reset current branch to this commit'을 선택하면 아래의 창이 뜬다.![](https://t1.daumcdn.net/cfile/tistory/233088425970226C15)

* Soft 모드
* Mixed 모드 : 선택한 버전 이후의 모든 버전이 사라지지만 Working Directory에 남겨진다. 또한 작업중이던 Working Directory의 상태는 유지된다. \(소스에 중요한 정보가 들어가 있을 때 사용\)
* Hard 모드 : 선택한 버전 이후의 모든 버전이 삭제된다. Working Directory와 Staging Area 공간에 있는 파일도 모두 삭제된다.

#### 3\) **Revert** \(커밋해버린 후, 버전을 제거하지 않고 되돌리기\)

버전을 제거하지 않고, 새로운 커밋을 생성하여 이전 상태로 되돌린다. 목록에서 되돌아가고 싶은 버전을 선택하고 마우스 우클릭한 뒤 'Reverse Commit'을 선택한다. 주의할 점은 위에서부터 아래로, 즉 역순으로 차례대로 하나씩 Reverse Commit 해야 충돌이 발생하지 않는다.

### 6. 브랜치\(branch 명령어\)

브랜치는 보통 원본과 실험용 프로젝트를 분리해서 만들고자 할 때 사용한다. \(예를 들어, 신규기능이나 불확실한 코드를 실험용에서 개발하고자 할 때\)

#### 1\) 브랜치 만들기

소스트리에서 \[Branch\] 버튼을 클릭한 뒤 아래의 단계를 실행한다.

![](https://t1.daumcdn.net/cfile/tistory/246E0143597034961A)

이제 브랜치는 총 2개가 존재하게 된다. \(master 브랜치, 실험용 브랜치\) 지금부터 브랜치 별로 따로 코드를 짜는 것이 가능하다.

#### 2\) 브랜치 합치기\(merge 명령어\)

신규기능 테스트가 끝났다고 가정했을 때, 실험용 브랜치를 master 브랜치로 합쳐보자. 실험용 브랜치를 우클릭한 뒤 'Merge 실험용 into current branch'를 클릭한다. 이를 'master브랜치로 체크아웃 했다'고 말할 수 있다. 브랜치가 잘 합쳐졌는지 확인해보고 싶다면, master브랜치의 소스에 실험용에서 만든 코드가 보이는지 찾아보면 된다.

![](https://t1.daumcdn.net/cfile/tistory/2545C93C5970E07307)

#### 3\) 브랜치간 충돌 해결하기

두개의 브랜치에서 서로 같은 위치의 코드를 변경하고 커밋했을 때 충돌이 발생한다. 아래가 충돌이 난 예시이다. master 브랜치 내의 파일의 3번째 줄을 커밋하고, 실험용 브랜치 내의 파일의 3번째 줄을 커밋한 뒤 master 브랜치로 병합\(merge\)하자 충돌이 발생한 모습이다.

![](https://t1.daumcdn.net/cfile/tistory/217EE33A5970E5E709)

해결방법은 일단 충돌이 난 부분을 지운뒤, 해당 파일을 우클릭한 뒤 'Resolve Conflicts' &gt; 'Mark Resolved'를 선택한다.  
충돌이 해결되었으면 다시 커밋을 하면 된다.

> 충돌을 줄이기 위해서는, 브랜치를 주기적으로 master의 내용과 동기화하자.

### 7. GitHub 원격저장소에 연결하기

로컬저장소\(C:\gbsb\project1\)와 원격저장소를 연결해서 **원격저장소에 백업**할 수도 있다. 대표적인 원격저장소는 GitHub나 Bitbucket 등이 있다.

#### 1\) 원격저장소 만들기

GitHub 페이지에서 'New repository'하여 원격저장소를 만든다.

#### 2\) 로컬저장소와 원격저장소를 서로 연결하기

소스트리 메뉴에서 \[Repository\] &gt; \[Add Remote\] 를 클릭하면 창이 뜬다. 거기서 \[Add\]를 클릭하면 아래의 창이 뜬다. 

![](https://t1.daumcdn.net/cfile/tistory/2675D33B5970CFF923)

URL / Path 입력란에 GitHub에 명시된 원격저장소 주소를 붙여넣고 \[Ok\] 버튼을 누르자. 이제 로컬저장소와 원격저장소가 연결되었다. 하지만 아직 동기화 되지 않은 상태다. 소스트리에서 \[Push\]를 클릭하고 아래의 단계를 실행한다.

![](https://t1.daumcdn.net/cfile/tistory/254535355970E8F304)

#### 3\) 원격저장소로 업로드 하기

방금전 실행한 \[Push\] 기능이 로컬저장소에서 원격저장소로 업로드하는 방법이다.

### 8. 협업하기

Git과 GitHub를 통해 사람들끼리 협업해야 할 때가 있다. \(예를 들어, 새로 입사한 신입이 원격저장소에서 로컬컴퓨터로 프로젝트를 가져와야할 경우\) 

소스트리의 \[File\] 메뉴에서 \[Clone/New\]를 선택한다. 아래와 같은 순서로 실행하면 원격 저장소가 복제된다.

![](https://t1.daumcdn.net/cfile/tistory/212F10385970F22B15)

하나의 원격저장소를 두고 각자 작업을 진행해야 할 경우가 있다. 작업 시작하기 전에 Pull을 먼저 실행해야 한다. 작업 순서는 pull -&gt; work -&gt; commit -&gt; pull -&gt; push 순으로 진행하자.

