# ssh 로그인 기능

 이번에는 secure shell 줄여서 sssh를 이용해서 원격저장소에 접근하는 방법을 알아 볼게요.   
우리는 원격 저장소, github을 이용해서 여러 서비스를 이용해요. 

![](../../.gitbook/assets/image%20%28303%29.png)

 관심을 가지고 있었다면 2번에 해당하 Use SSH에 대해 알아보고 이용도 해봤을거에요.   
오늘은 이 부분을 확실히 조져 볼게요.   
  
HTTPS VS SSH   
참고로 두 가지다 대등한 다른 방식의 통신방법일뿐 SSH는 자동로그인 기능이 아니에요. 

### 실습 

```text
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/이혜성/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/이혜성/.ssh/id_rsa
Your public key has been saved in /c/Users/이혜성/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:fAvkPFt660TMYyISatLVuYh58lXC/51dP31fNApRW40 이혜성@DESKTOP-CF2UBJF
The key's randomart image is:
+---[RSA 3072]----+
|             . o.|
|     o .    . E .|
|    o = o  . .   |
| . = o X o  .    |
|. B + + S O.   .o|
| o + o . % +.o.o+|
|    .   o = o...=|
|         o .    =|
|         .o     .|
+----[SHA256]-----+

```

다른 컴퓨터로 접속 할 수 있는 비밀번호가 생성된 거에요. 하지만 이 방식은 기계적으로 굉장히 복잡한 비밀번호를 만든거에요.   
하지만 여러분이 1234로만든 비밀번호는 너무나 쉽게 뚫리게 되요. 하지만 이방식은 현재 기술 방식으로는 절대 뚫리지 않는다고 해요.   


비밀번호\(파일2개\)는 아래 경로에 저장되어 있어요. 

```text
/c/Users/이혜성/.ssh/id_rsa
/c/Users/이혜성/.ssh/id_rsa.pub
```

해당 경로에 가볼게요. 아래 명령어를 쭉 따라 쳐보세요. 

![](../../.gitbook/assets/image%20%28304%29.png)

![](../../.gitbook/assets/image%20%28310%29.png)

쉽게 보면 .ssh 폴더에 id\_rsa, id\_rsa.pub 파일 2개가 존재하는거에요. 

#### id\_rsa\(public key\) : 공개키 

#### id\_rsa.pub\(private key\): 비밀키 

![](../../.gitbook/assets/image%20%28311%29.png)

키가 2개 생성되고 나의 컴퓨터에는 private key가 다른 서버의 컴퓨터에는 public key가 주어지게 되는거에요. 

### github에 ssh키 등록 

#### 1\) id\_rsa.pub 비밀번호 확인

```text
$ cat id_rsa.pub
```

![](../../.gitbook/assets/image%20%28309%29.png)

#### 2\) settings\(github site\) -&gt; SSH&GPG KEY -&gt; New SSH key  

![](../../.gitbook/assets/image%20%28312%29.png)

![](../../.gitbook/assets/image%20%28307%29.png)

본인 SSH키 이름과 Key를 넣어 주세요. 

![](../../.gitbook/assets/image%20%28305%29.png)

그럼 잘 등록되게 되요. 



### ssh 키로 로그인 

우선 새로운 원격 저장소를 만들고 ssh버튼을 누르고 copy버튼을 눌러주세요. 

![](../../.gitbook/assets/image%20%28306%29.png)

빈 디렉토리를 만들어 주세요.   


![](../../.gitbook/assets/image%20%28308%29.png)

```text
$ git clone 'ssh버튼을 누르고 카피한 주소 입력'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~? yes 하면 되요. 

$ echo a>f1.txt
$ git status # 로컬 저장소에서 git이 파일 추적이 되는지 안되는지 확인
$ git add f1.txt
$ git commit -m 'git test for ssh key'
$ git push 


```

위 명령어를 입력하면 정상적으로 사용된걸 확인 할 수 있어요. 

![](../../.gitbook/assets/image%20%28298%29.png)

## 결론 

1\) 안전한 ssh 통신방법으로 서버에 로그인

2\) ssh키를 github사이트에 등록해야함

3\) 

