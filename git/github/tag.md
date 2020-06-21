---
description: ligth weight tag vs annotaed tag
---

# Tag

![](../../.gitbook/assets/image%20%28315%29.png)

release를 클릭하면 아래와 같은 화면이 나오는걸 볼 수 있어요.   


![](../../.gitbook/assets/image%20%28300%29.png)

v2.27.0이 보이는데요.  b3d7a52 커밋이라는걸 확인 할 수 있어요.  
결국 이 release 버전이 가리키는 commit id가 달라져서는 안되요.   
왜냐하면 그 release 버전이 언제 어느시점이 만들어 졌는지 가리키고 있어야 하는거에요. 

하지만 master branch가 가리키고 있는 최신 커밋은 매번 달라져야하는거조.\(아래 빨간부분\) 

![](../../.gitbook/assets/image%20%28313%29.png)

즉 branch와 똑같이 tag도 어떤 특정한 커밋 ID를 가리키는, 커밋 버전을 가리키는 것이지만 **tag는 언제나 똑같은 것을 가리킨다. 라는 거에요.** 

## 실습 

## light weight tag

```text
$ git init 
$ echo a>f1.txt 
$ git add f1.txt
$ git commit -m 1

$ echo b>>f1.txt 
$ git commit -am 2

 $ git tag 1.0.0  
```

9번째 줄의 명령어는 내부적으로\(git log 해보면\) 가장 최신 커밋 id와 묶여서 tag화되요. 

1\) git tag 1.0.0   
현재 branch의 최신 커밋을 tag!

2\) git tag 1.0.0 master  
맨 마지막에 본인이 원하는 브렌치 이름을 적음   
  
3\) git tag 1.0.0 &lt;현재 branch의 특정 commit id&gt;   
ex. git tag 1.0.0 987ff98e8g5d1e2a6s5df78ggds

```text
$ git tag 
1.0.0
```

그럼 tag라는 이름을 통해서 1.0.0이라는 태그가 만들어 진걸 확인 할 수 있어요.

```text
$ git log
```

git log 명령어를 통해서도 노란색으로 tag가 이쁘게 달린게 보이조?

![](../../.gitbook/assets/image%20%28297%29.png)





## annotated tag

'주석을 단다. 자세한 정보를 기입한다'라는 의미에요.   


```text
$ git tag -a 1.1.0 -m 'bug fix' 
```

-a\(annotated\) 약자이고 위의 소스코드는 1.1.0버전이며 버그 수정이 완료되었다는 의미이기도 해요. 

```text
$ git tag -v 1.1.0
```

![](../../.gitbook/assets/image%20%28314%29.png)

차이 인지 했나요. 주석을 달수 있냐 없냐라는 큰 차이가 존재해요.   
  
다음은 이제 주석을 달았으니 저장소로 보내야겠조?  
우선 새로운 github에서 새로운 저장소를 만들게요.   
기존 로컬 저장소를 이용하도록 할게요. 

```text
$ git remote add origin <본인 저장소 http, ssh 주소> 
$ git push -u origin master 
```

위 명령어만으로는 tag가 저장되지 않아요. 

```text
$ git push --tags
```

--tags까지 같이 붙여줘야 로컬에서 만든 태그가 원격저장소에 업로드 되요.   


### tag 삭제 방법 

```text
$ vim f1.txt(d추가) 
$ git commit -am 4
$ git tag 1.1.1

$ git tag
1.0.0
1.1.0
1.1.1

$ git tag -d 1.1.1
Deleted tag'1.1.1'(was 23gfde)


```

## 정리 

**태그 목록 보기**

git tag

**태그 생성 \(light weight tag\)**

git tag "태그 이름" \[태그가 가르킬 버전의 커밋 아이디\]

**태그 생성 \(annotated tag\)**

git tag -a "태그 이름" -m "태그에 대한 설명" \[태그가 가르킬 버전의 커밋 아이디\]

**태그 삭제**

git tag -d "삭제할 태그명"

**태그 원격 저장소로 업로드**

git push --tags

