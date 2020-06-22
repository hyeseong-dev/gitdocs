# GCP 배포

![](../../../.gitbook/assets/image%20%28316%29.png)

톱니 바퀴를 누르면 파일 업로드 기능이 있어요. 작업한 파일을 압축해서 편리하게 서버에 업로드 할게요. 

![](../../../.gitbook/assets/image%20%28327%29.png)

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





