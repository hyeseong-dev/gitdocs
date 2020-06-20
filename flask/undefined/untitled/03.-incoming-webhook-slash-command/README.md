# 3. Incoming Webhook, Slash Command 활성화

#### 이번 페이지에서 다룰 내용 

#### 1\) Incoming Webhook & 2\) Slash Command 활성화

### Incoming Webhook

![](../../../../.gitbook/assets/image%20%28280%29.png)

우선 **Activate** **Incoming** **Webhooks** 를 On으로 활성화 시켜주세요.   
그 다음으로 가장 아래  **Add** **New** **Webhook** **to** **Workspace 클릭 새로운 Webhook을 생성하는 화면으로 전환되요.**   


> #### Webhook?  
>
> #### Webhook에서 특정한 URL을 주게되요. 그 URL에 DATA를 전달 하였을때 메시지를 보내준다고 했는데요. Slack에는 Channel이라는 여러 개념이 있어요. 그리고 DM\(Direct Message\)으로 직접 사용자에게 보낼수도 있고 그리고 비밀, Private 채널을 만들수 있기도해요.  즉, 채팅방이 여러개 있기 때문에 Webhook은 어떤 채널에 메시지를 보낼지 알려주게되요.  그래서 1\)Channel 2\) DM을 보낼지 선택하게 되요.

이후 webhook URL 생성화면에서 flaskdev 채널을 선택하면 URL이 생성되게되요. \(위 스샷에서 아래에서 2번째 줄이 그거에요.\)  
  


![](../../../../.gitbook/assets/image%20%28289%29.png)

flaskbot was added to \#flaskdev by LEE HYE SEONG. 라는 부분이 대화창에 나타나게 됩니다.   


#### Webhook URLs for Your Workspace 사용해보기. 

아래 sample curl request를 copy해서 flaskdev channel에서 챗봇이 어떤 반응을 하는지 살펴 볼게요. 

 **Sample curl request to post to a channel:**

```text
curl -X POST -H 'Content-type: application/json' \
--data '{"text":"Hello, World!"}' \
https://hooks.slack.com/services/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
```

cmd or Powershell을 실행시켜 위 명령어를 복붙해서 실행해주세요.   
그럼 아래에 OK라고 리턴된 문자가 보이나요?  
\(저의 경우 cmd와 powershell이 명령문을 인식하지 못해 git bash로 했어요.\)  


![](../../../../.gitbook/assets/image%20%28258%29.png)

![&#xCC57;&#xBD07;&#xC774; &#xBA85;&#xB839;&#xC5B4;&#xC5D0; &#xB300;&#xD55C; &#xBC18;&#xC751;\(Hello World!\)](../../../../.gitbook/assets/image%20%28261%29.png)

위 flaskdev 채널로 다시 가보면 챗봇이 Hello World라고 반응한걸 보실수 있어요.   
  
우선 위에서 제가 입력하였던 명령어를 아는데까지 분석해볼게요.   
**Sample curl request to post to a channel:**

```text

curl -X POST -H 'Content-type: \
application/json' --data '{"text":"Hello, World!"}' \
https://hooks.slack.com/services/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

```

#### 1\) curl :  서버와 통신할 수 있는 커맨드 명령어 툴. 웹개발에 매우 많이 사용되고 있는 **무료 오픈소스**

**2\) -X : 요청 메소를 지정\(옵션이 없으면 기본값은 GET\)  
3\)  -H : 요청 헤더를 지  
4\) Content-type: application/json 형태로 지정   
5\)** --data '{"text":"Hello, World!"}' Json 형태의 내용을 입력하게 되요.   
6\)  보내는 URL은 WebHook URL이에요.  
  
일단 이 정도로  Incoming Webhook을 알아보고 **Slash** **Command** 를 알아볼게요.   


### Slash Command

![](../../../../.gitbook/assets/image%20%28270%29.png)

#### Slash Commands -&gt; Create New Command 버튼 클릭

![](../../../../.gitbook/assets/image%20%28267%29.png)

#### 

#### Create New Command 버튼 클릭시 입력란이 나오게 되요. 

1. 명령어 이름을 지정
2. 요청할 URL 주소\(임의로 Naver로 했어요. 추후에 바꿀거에요.\)
3. 명령문에 대한 짧은 설명
4. 사용 힌트 

그리고 Save 버튼을 클릭하면 slash 커맨드 완성되요.   
즉, 이전 Incomming Webhook은 파이썬에서 사용하는 명령어라면 지금 생성한 slash 커맨드의 경우 slack에서 사용한 명령어를 **Request URL 로 보내지게 되요.**

![](../../../../.gitbook/assets/image%20%28259%29.png)

완성된 Slash Commads가 등록된걸 볼수 있어요. 수정과 삭제도 가능해요.  
 



