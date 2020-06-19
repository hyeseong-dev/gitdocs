# Branch Conflict

branch merge 시, git이 처리하는 작업이 무엇인지 파악하고 자동으로 병합하는 1차적인 방법이 안될 경우 2차적으로 접근하는 수동 방법이 무엇인지 파악해볼게요. 



## 요약 

**충돌이 일어났을 때** 

충돌이 생기면 아래와 같은 메시지가 뜹니다. 

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5123.png)

git status를 하면 충돌이 일어난 파일을 찾을 수 있습니다. 

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5125.png)

 충돌이 발생한 파일을 수정합니다. 아래와 같습니다. 

![](https://s3-ap-northeast-2.amazonaws.com/opentutorials-user-file/module/2676/5126.png)

'&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD' 부터 '=======' 사이의 구간이 현재 체크 아웃된 파일의 내용이고 '=======' 부터 '&gt;&gt;&gt;&gt;&gt;&gt;&gt; exp' 사시의 구간이 병합하려는 대상인 exp 브랜치의 코드 내용입니다.  이 정보를 참고로해서 두개의 코드를 병합한 후에 특수기호들을 제거해주시면 됩니다. 작업이 끝나면 파일을 저장.

충돌 작업을 끝냈다는 것을 깃에게 알려줍니다. 

| 1 | `git add` `'conflicted file name'` |
| :--- | :--- |


