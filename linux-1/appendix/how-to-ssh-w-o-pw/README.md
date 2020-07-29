# how to ssh w/o pw



비밀번호 입력없이 간편하게 SSH 방식으로 secure하게 login하는 방법에 대해 알아볼게요.   
  
우선 아래 왼쪽은 local환경이고 오른쪽은 remote 환경입니다.

![](../../../.gitbook/assets/image%20%28368%29.png)

## SSH 생성 

### private key & public key 생성 

![](../../../.gitbook/assets/image%20%28369%29.png)

위 해당 명령어를 실행해볼게요. 

```text
Generating public/private rsa key pair.
Enter file in which to save the key 
(/c/Users/이혜성/.ssh/id_rsa):
```

그럼 어디에 저장할지 물어봅니다. default 위치로 저장할게요. 엔터 키 눌러주세요. 

```text
Enter passphrase (empty for no passphrase):
Enter same passphrase again:        
Your identification has been saved in /c/Users/이혜성/.ssh/id_rsa       
Your public key has been saved in /c/Users/이혜성/.ssh/id_rsa.pub       
The key fingerprint is:
SHA256://OOh7SHdONvbciZjz0o9F7CB7Bech38wBWRMK6bBwY leehyeseong@DESKTOP-CF2UBJF
```

그럼 위와 같이 이번에는 압호입력을 요구하는데요. 그냥 빈값으로 둘게요\(엔터 두번 눌러서 넘아가주세요\)

이후 .ssh/폴더 아래 id\_rsa파일과 id\_rsa.pub 파일이 생성되요.

### 생성 확인

![](../../../.gitbook/assets/image%20%28370%29.png)

cd 명령어와 ~\(틸드\)옵션으로 사용자 계정으 디렉토리로 연결됩니다.  
그리고 ls -al 명령어로 .ssh 디렉토리 내의 파일들을 확인할 수 있어요.

![](../../../.gitbook/assets/image%20%28371%29.png)

다음 



