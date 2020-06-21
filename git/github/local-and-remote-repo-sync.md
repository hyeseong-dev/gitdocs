# Local & Remote Repo Sync

하나의 원격 저장소를 중심으로 2개 혹은 다수의 지역 저장소를 동기화 하는 방법을 알아볼게요.   
1\) 협업을 하는 경우   
2\) 본인의 컴퓨터가 다수인 경우   
위 2가지 상황에 따라 매우 유용하게 적용 할 수 있어요. 



```text
$ git clone https://github.com/osori-magu/gitfth.git git_home
```

git\_home 디렉토리가 생성되고 그안에 .git 디렉토리와 원격저장소의 파일을 업로드 혹은 다운로드 하게 되는 상태로 바뀌게 되요.   


```text
$ git clone https://github.com/osori-magu/gitfth.git git_office
```

git\_office 디렉토리가 생성되며 그 안 디렉토리에서는 .git 디렉토리가 생성되고 원격 저장소의 파일을 업로드 혹은 다운로드 할 수 있는 상태가 갖춰지게 되요. 

### 시나리오 1 

1\) 집에서 git\_home 디렉토리에서 작업을 하고 난뒤 add -&gt; commit -&gt; push 명령어를 입력한다. 

2\) 직장, 학교, 원격지에서 본인 노트북을 이용하여 git\_office 디렉토리에서 가장 먼저 집에서 했던 내용들을 pull명령어로 다운받아 진행해준다. \(만약 push 명령어를 먼저 입력하면 충돌 오류가 발생함\)   
그리고 소스 코드를 작성하고 다시 add, commit, push 해줌  
  
3\) 집에와서 다시 git pull 명령어를 자연스럽게 처음부터 땡겨준후 진행한다. 



