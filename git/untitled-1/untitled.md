# Exercise

## Fast Forwarding 방식 V.S Non-fast forwarding



```text
$ git checkout -b iss53 
```

위 chekout 명령어에 -b 옵션은 아래 2가지 명령어를 한번에 입력하고 실행한것과 같아요. 

> git branch iss53  
> git checkout iss3

![](../../.gitbook/assets/image%20%28256%29.png)

```text
$ vim index.html 
$ git commit -am 'added a new footer (issue 53)'
```

![](../../.gitbook/assets/image%20%28268%29.png)

갑자기 급하게 처리해야할 일이 있어서 마스터 브렌치에서 다시 브렌치를 뺄거에요. 그러기 위해선 먼저!! git checkout master 를 해줘야해요.    
이후 git checkout -b hotfix 명령어를 실행하여 새로운 브렌치를 만들어줘요.   


```text
$ git checkout master 
$ git checkout -b hotfix
```

그 다음 vim 에디터를 이용해서 index.html 파일을 생성할게요. 

```text
$ vim index.html 
$ git commit -am 'c4 fixed the broken email address'
```

![](../../.gitbook/assets/image%20%28291%29.png)

여기서 hotfix 브렌치와 iss53 브렌치는 master라는 공통의 부모 커밋을 가지는 브렌치가 된다는점 유의하세요.   
마스터 브렌치로 병합을 하려고 하면 일단 

```text
$ git ckeckout master 
$ git merge hotfix 
Updating 6efd70b..f499d0c
Fast-forward
 index.html | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html

```

merge를 했을때 4번째줄에 "Fast-forward"가 나타나요. 한글로는 빨리 감기라는 의미에요. 

![](../../.gitbook/assets/image%20%28255%29.png)

이제 master 브치는 hotfix 브랜치의 commit을 가리키게 되요.   
그리고 별도의 commit을 가리키지 않아요! 

#### 우리가 이전 병합을 할때는 별도의 commit을 생성했는데! 

Fast-forward에서는 병합 커밋이 일어나지 않게되요. 단순히 master가 가르키는 commit이 누구인지 가르킬 뿐이에요. 

#### hotfix와 master 브렌치가 현재 상태에 공존 할 필요 없으니 hotfix를 지울게요.\(그게 더 깔끔하게 브렌치를 관리하는 방법\)

```text
$ git branch -d hotfix
Deleted branch hotfix (was f499d0c).

```

그럼 이제 다시 원래 작업하던 iss53 브렌치 작업을 진행 해야겠조?

```text
$ git checkout iss53 
$ vim index.html 
$ git commit -a -m 'finished the new footer [issue 53]'
[iss53 ad82d7a] finished the new footer [issue 53]
1 file changed, 1 insertion(+)
```

![](../../.gitbook/assets/image%20%28290%29.png)

```text
$ git checkout master 
$ git merge iss53
CONFLICT (add/add): Merge conflict in index.html
Auto-merging index.html
Merge made by the 'recursive' strategy.
 index.html | 2 ++
 1 file changed, 2 insertions(+)

```

Merge made by the 'recursive' strategy 문구가 뜨는게 보이조? 이전에는 Fast-forward였는데 말이조?!   


![](../../.gitbook/assets/image%20%28283%29.png)

issu53이 master로부터 독릭한 이후 master는 c2에서 c4로 커밋 변화가 일어났어요. 이러한 경우에는 Fast-forward를 할 수 없어요.   
그런 깃은 내부적으로 동작을 하게되요.   
  
1\) git은 master와 iss53의 공통 조상을 찾게되요. 3 way merge라는 내부적인 방법을 이용해서 c4와 c5를 합치고 이 2개를 합쳤다는 정보를 알려주는 별도의 정보를 알려줘요. 즉 C6가 아래 스샷 처럼 만들어 지게 되는거에요.   


![](../../.gitbook/assets/image%20%28261%29.png)

위의 C6는 C5와 C4에 대한 정보를 모두 공통으로 갖는 부모를 가지게 되는거에요.   


### Fast-forward V.S Recursive 방식 간 차이 

#### 1\) Fast-forward는 커밋 생성\(X\)  2\) Recursive 방식은 merge commit을 생성\(O\)









출처 : [https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88)

