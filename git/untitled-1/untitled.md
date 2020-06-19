# Exercise

## Fast Forwarding 방식 V.S Non-fast forwarding



```text
$ git checkout -b iss53 
```

위 chekout 명령어에 -b 옵션은 아래 2가지 명령어를 한번에 입력하고 실행한것과 같아요. 

> git branch iss53  
> git checkout iss3

![](../../.gitbook/assets/image%20%28255%29.png)

```text
$ vim index.html 
$ git commit -am 'added a new footer (issue 53)'
```

![](../../.gitbook/assets/image%20%28265%29.png)

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

![](../../.gitbook/assets/image%20%28284%29.png)

여기서 hotfix 브렌치와 iss53 브렌치는 master라는 공통의 부모 커밋을 가지는 브렌치가 된다는점 유의하세요. 





출처 : [https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88](https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88)

