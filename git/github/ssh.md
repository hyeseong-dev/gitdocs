# ssh 로그인 기능

 이번에는 secure shell 줄여서 sssh를 이용해서 원격저장소에 접근하는 방법을 알아 볼게요.   
우리는 원격 저장소, github을 이용해서 여러 서비스를 이용해요. 

![](../../.gitbook/assets/image%20%28300%29.png)

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

