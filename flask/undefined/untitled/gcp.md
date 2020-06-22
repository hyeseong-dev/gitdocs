# GCP 배포

![](../../../.gitbook/assets/image%20%28316%29.png)

톱니 바퀴를 누르면 파일 업로드 기능이 있어요. 작업한 파일을 압축해서 편리하게 서버에 업로드 할게요. 

![](../../../.gitbook/assets/image%20%28332%29.png)

```text
$ ls -al 
$ unzip chatbot.zip
```

**unzip** 명령어를 통해서 압축된 파일을 풀 수 있어요. 



**가상환경 생성**

```text
$ python -m venv ( 이 부분에 임의로 가상환경 이름을 정하세요.)
$ source 가상환경이름/bin/activate 
$ pip install flask requests # 두개를 사용했어요. 
```

### 인스턴스 서버 방확벽 off 

```text
$ ctrl + c
$ sudo systemctl stop firewall # 방화벽 off 
```

방화벽을 끄기 위해서 systemctl stop firewall 명령어를 실행했어요.   
  
  
또한 앞서 app.py 부분에 '127.0.0.1' 이 부분을 -&gt; '0.0.0.0'로 바꿀게요. 

### 앱 IP주소 변경 

```text
$ sudo yum -y install     # text 에디터 
$ nano app.py ( '0.0.0.0'로 변경후 ctrl+s, ctrl+x )
```

### Compute Engine 방화벽 끄기 및 포트 설정 

![](../../../.gitbook/assets/image%20%28323%29.png)

![](../../../.gitbook/assets/image%20%28324%29.png)

![](../../../.gitbook/assets/image%20%28322%29.png)

*  '유형' 부분을 고정으로 바꿔주세요. 이후 나오는 팝업창의 제목이나 이름을 flask로 입력하고 저장해주세요. \(그래야 IP가 변동되지 않아요. \) 
* **방화벽 규칙**으로 가서 **'방화벽 규칙 만들기'** 를 클릭해주세요. 



![](../../../.gitbook/assets/image%20%28326%29.png)

![](../../../.gitbook/assets/image%20%28331%29.png)

* 방화벽 규칙만들기 폼에서  5000번 포트를 추가해 보도록 할게요.  
* 1\) 이름 : flask-test
* 쭉쭉 기본 설정으로 두고 **대상** 부분에는 **네트워크의 모든 인스턴스를 선택**
* **소스IP 범위 0.0.0.0/0**
* **지정된 프로토콜 및 범위 둘다\(tcp, udp\) 5000번 포트로 할게요.** 

만들기 버튼을 클릭해주세요. 

이제다시 

1\) 주소창에 본인에게 부여된 IP주소:5000/api/v1/test입력하면 Method Not Allowed가 뜨면 되요.  
본인 IP주소:5000/api/v1/test를 slack에 입력할 건데요.   
**Slash Commands** 수정 버튼을 클릭 하시고 Request URL에 해당 URL을 입력하고 save버튼을 눌러주세요.   
\(혹시 재설치를 요청하는 팝업창이 영문으로 길게 나오면 지시에 따라 재설치를 해주세요. \)   


channel에서 /flasktodo 명령어를 입력하면 빈 문자열이 나와요.   


