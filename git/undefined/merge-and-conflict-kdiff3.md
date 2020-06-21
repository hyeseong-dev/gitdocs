# Merge&Conflict원리 및 kdiff3

```text
# 빈디렉토리에
$ git init 
$ vi f1.txt( function (){ return 'common'} )
$ git add f1.txt 
$ git commit -m 1

$ git checkout -b exp
$ vim f1.txt ( 'common' -> 'exp' ) 
$ git add f1.txt 
$ git commit -am 'common -> exp' 

 $ git checkout master 
 $ vim f1.txt( 'common -> master' ) 
 $ git commit -am 'common -> master' 
 
 $ git merge exp 
 Auto-merging f1.txt
CONFLICT (content): Merge conflict in f1.txt
Automatic merge failed; fix conflicts and then commit the result.
```

 위 merge exp 명령어로 충돌을 발생시켰어요. 이 동작의 구성 원리가 무엇인지 파악하고 해결 방법을 찾아 볼게요. 

#### 방법1\) 직접 문제가 되는 파일들을 찾아서 타입핑함. 

#### 방법2\) kdiff3 tool을 이용하여 해결 

{% tabs %}
{% tab title="kidff3 설정방법" %}
```text
# 윈10 kdiff3 설치 후
# 설정 

$ git config --global --add merge.tool kdiff3
$ git config --global --add mergetool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
$ git config --global --add mergetool.kdiff3.trustExitCode false

$ git config --global --add diff.guitool kdiff3
$ git config --global --add difftool.kdiff3.path "C:/Program Files/KDiff3/kdiff3.exe"
$ git config --global --add difftool.kdiff3.trustExitCode false


# 실행 
$ git mergetool
```

kdiff3 tool을 설정하고 실행하는 명령어에요.   
하는 목적은 kdiff3 GUI tool을 이용하여 merge conflict를 해결하는 방법을 찾는거에요. 
{% endtab %}
{% endtabs %}

![](../../.gitbook/assets/image%20%28297%29.png)

실행 하면 위와 같은 화면이 나타나요.   
좌측 상단 화면 부터 base -&gt; Local -&gt; Remote 그리고 하단에 Output화면창이 있어요.   
Base는 master 브렌치가 바꾸기전 사항과 exp 브렌치가 바꾸기전인 공통적인 사항을 말해요.\(common에 해당\)  
  
위에 A, B, C, 형태의 버튼이 보여요. 이것들중 원하는것 하나 혹은 다수를 선택하여 Output을 설정하고 save 버튼을 클릭하면 병합을 계속 진행할수 있고요.   
  
혹은 A,B,C 모두 원하지 않는다면 기본적으로 A를\(base\) 선택하시고 원하는 소스코드를 입력하시고 저장버튼을 눌러 진행해도 되요.   
  
다음 아래 명령어를 입력하면 f1.txt가 modified 된걸 볼 수 있어요. 

```text
$ git status 
$ git commit 
```

![](../../.gitbook/assets/image%20%28298%29.png)

git commit 명령어를 입력하면 merge commit 화면이 나타나고 비로소 merge conflict 문제를 해결하고 병합문제를 해결하게 되는거에요. 









