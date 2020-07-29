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

그리고 scp 명령어를 입력할게요.   
비밀번호\(remote\) 입력해주세요.   
  
현재 로컬환경에서 ~옵션으로 path를 입력하고 마지막 선택하려는 파일 이름을 입력할게요 그리고 space로 띄우고 접속하려는 remote 컴퓨터에 user이름, @,  IP주소, 절대경로로 .ssh디렉토리까지 입력하고 저장하고자 하는 파일 이름을 입력하면 로컬의 id\_rsa.pub파일이 다운로드 완료됩니다.

![](../../../.gitbook/assets/image%20%28371%29.png)

다음 **remote terminal 창에서 확인해보면 아래와 같이 파일을 확인 할 수 있어요.**

![](../../../.gitbook/assets/image%20%28373%29.png)

uploaded.key.pub 이름을 아래 명령어를 입력해서 변경할게요.   
&gt;&gt; 기호는 append 기능이 있다는점 유념하세요. 그리고 이름을 

![](../../../.gitbook/assets/image%20%28374%29.png)

파일 생성이 잘 되었는지 확인해 볼게요. 

![](../../../.gitbook/assets/image%20%28372%29.png)

## 리눅스 permission

chmod 명령어를 이용해서 permission 설정을 하도록 할게요.

![](../../../.gitbook/assets/image%20%28375%29.png)

우선 .ssh폴더는 700으로 저장되어야 해요.   
참고로 700은 현재 위치의 모든 파일의 읽기, 쓰기, 실행이 가능한 경우를 말해요.

  
 600 입니다. 여기서 100번대는 소유주, 10번대는 그룹, 1번대는 다른 사용자에게 권한을 주겠다는 뜻입니다. 

나만 사용할 수 있어야 하니까 당연히 100번대에만 권한을 줍니다. 이때 읽기는 4, 쓰기는 2, 실행은 1입니다. 읽고 쓰기가 가능해야 하므로 4+2 = 6 해서 chmod 600 이 되는 것입니다. 



이제 로컬 터미널에서 **ssh osori@ IP주소**

한 후 실행하면 비밀번호 입력없이 잘 접속하는 화면인걸 볼 수 있어요.

### 콘솔 비밀번호 입력 기능 off

sshd\_config 파일을 복사해서 sshd\_config.bat파일로 생성하도록 할게요.  
이유는 원본 파일 백업용이에요.

```text
osori@django-server:~$ sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bat
```

####  파일 수정

```text
sudo nano /etc/ssh/sshd_config
```

나노 편집기로 파일을 열어보면 쭉~ 뭔가 많은 데요. 아래 빨간 부분을 찾아 no로 입력해주세요.  
그리고 저장하고 나가주세요.

![](../../../.gitbook/assets/image%20%28376%29.png)

```text
sudo service ssh restart
```

위 명령어를 실행해서 ssh를 다시 실행할게요. 

