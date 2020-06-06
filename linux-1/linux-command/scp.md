# scp

## scp란?

Secure Copy의 약자로, 네트워크가 연결되어 있는 원격지에 파일을 간편하고 안전하게 전송할 수 있는 명령어 SSH와 동일한 22번 포트를 사용하여 전송하기 때문에 보안도 뛰어나며 디렉토리 전송도 간편한 것이 장점.

```text
scp ubuntu@home.hkit.xyz:/home/ubuntu/aaa.txt ./
```

## **명령어**

cp 명령어와 틀은와 같다. 

> **scp \[옵션\] \[원본 대상\] \[복사할 지점\]**

**방법1** 

> **scp \[옵션\] \[원본 대상\] \[원격지계정@IP:/파일생성지점\]**

방법2 

> **scp \[옵션\] \[원격지계정@IP:/복사해올파일\] \[/붙여넣을경로\]**

자신의 파일과 디렉토리를을 원격지에 복사하거나 원격지에 있는 파일을 자신의 서버로 끌어오는 것이 가능하다.

![](../../.gitbook/assets/image%20%28227%29.png)

![](../../.gitbook/assets/image%20%28226%29.png)

### 제3 컴퓨터로 이용  

#### 바로 위 이미지 참고

**심지어 제 3의 서버에서 1번 서버에 있는 파일을 2번 서버에 붙여넣기도 가능하다.**

그러니까 좀 더 정확한 옵션은

**scp \[옵션\] \[원본서버계정@IP:/원본 대상\] \[목적지계정@IP:/복사할 지점\]** 

**단, 로컬일 경우 계정과 IP정보는 기입하지 않아도 된다.**

\*\*\*\*

## 정리 

#### 리눅스\(우분투\) 원격 접속

PS&gt; ssh [hkit0x@home.hkit.xyz](mailto:hkit0x@home.hkit.xyz)



#### pyvenv가상환경만듬

$ python3 -m venv pyvenv



#### 최신 pip 버전 받기

$ pip instal pip --upgrade



#### 플라스크 설치

$ pip install flask

#### 

#### Windows에서 리눅스로 폴더 복사

ps&gt; scp -r ./minicafeweb [hkit0x@home.hkit.xyz](mailto:hkit0x@home.hkit.xyz):/home/hkit0x

#### 

#### 소스 편집

$ nano minicafeweb.py app.run\(host='0.0.0.0', port=50xx\)

#### 

#### 플라스크 시작하기

$ python minicafeweb.py

#### 

#### 크롬에서 [http://hkit0x.hkit.xyz:50xx로](http://hkit0x.hkit.xyz:50xx%EB%A1%9C/) 접속하기



