# curl

**\# curl이란?**

![](../../../../.gitbook/assets/image%20%28267%29.png)

서버와 통신할 수 있는 커맨드 명령어 툴입니다. 웹개발에 매우 많이 사용되고 있는 **무료 오픈소스**입니다. curl의 특징으로는 다음과 같은 수 많은 프로토콜을 지원한다는 장점이 있습니다.  
  
**! 다양한 지원 프로토콜들...**  
DICT, FILE, FTP, FTPS, Gopher, HTTP, HTTPS, IMAP, IMAPS, LDAP, LDAPS, POP3, POP3S, RTMP, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, Telnet, TFTP  
  
또한 SSL 인증 방식 역시 가능합니다.   


**\# curl 다운로드 받기**  


curl은 아래 사이트에서 다운로드가 가능합니다. 현재 17년 5월 26 기준 **7.54.0 버전**까지 릴리즈되어있습니다.  
  
**curl 다운로드 바로가기 &gt;** [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html)  


### ! curl에 설정 가능한 옵션보기

아래는 사용 가능한 다양한 옵션들입니다.

* -X : 사용할 방식 메소드 선택하기
* -d : 함께 전달할 파라미터값 설정하기
* -G : 전송할 사이트 url 및 ip 주소
* -H : 헤더 정보를 전달하기
* -i : 사이트의 Header 정보만 가져오기
* -I : 사이트의 Header와 바디 정보를 함께 가져오기
* -u : 사용자 정보  

### ! header 값 설정하기, -H

-H값을 사용히야 헤더에 전달할 값들을 설정합니다.  
- Content-Type을 application/json으로 설정하기  
curl -H "Content-Type: application/json"  
  
- Content-Length를 0으로 설정하기  
curl -H "Content-Length: 0"  
  


### ! curl을 사용하여 파라미터를 전달하기

전달할 파라미터가 있는 경우의 방법입니다. 파라미터값을 전달하는 경우 아래와 같이 url 뒤에 붙이는 get 방식이나 -d 옵션을 사용하여 전달할 수 있습니다.curl -G http://webisfree.com/action/?test=ok  
또 다른 방법으로 -d 옵션을 사용하면 아래처럼 전달합니다. 만약 전달할 값이 아래와 같다면 다음과 같이 수행합니다.  
  
**@ Method / 전달할 값**  
POST / test=ok  
curl -X PUT -G http://webisfree.com/action -d test=ok  


### ! POST 메소드를 사용한 예제

기본값으로 메소드는 POST이므로 -X 설정이 없이 사용할 수 있습니다.  
**@ Method / 전달할 값**  
POST / test=ok, test2=ok  
curl http://webisfree.com/action -d test=ok -d test2=ok  
  
아래와 같이 따옴표를 사용하여 하나로 묶어 사용할 수도 있습니다.curl http://webisfree.com/action -d 'test=ok&test2=ok'  
  


### ! DELETE 메소드를 사용한 예제

아래는 DELETE 메소드로 요청하는 방법입니다.curl -X "DELETE" http://webisfree.com/action/  
예를들어 아래처럼 사용할 수 있습니다.  
curl -X DELETE -H "Accept: application/xml" -H "Content-type: application/xml" -u \[USER:PASS\] -X  
-u를 사용하여 계정 정보를 입력시 아이디만 넘길 수 있습니다. 이 경우 패스워드 입력창이 나타나며 여기에 패스워드를 입력하면 됩니다.  


### ! url이 긴 경우 역슬러쉬 사용하기

리눅스 쉘 환경에서 입력시 명령어 줄이 긴 경우 다음 줄에 나타나기 위해서 역슬러쉬 \ 기호를 많이 사용합니다. 아래 예제를 봐주세요.curl -G http://webisfree.com/action \  
-X DELETE \  
-d id=123  
이처럼 사용할 수 있죠.  


### !  여러개의 파라미터를 전달하는 경우

하나가 아닌 데이터 값이 여러개인 경우 어떻게 할까요? 이 경우 두 가지 방법으로 사용할 수 있습니다. -d id=123 -d name=webisfree -d number=1004  
  
--data "id=123&name=webisfree&number=1004"  
  
-d 또는 --data를 사용하여 여러개의 파라미터를 한 번에 전달할 수 있습니다.  
  


### \#301 Redirect 되는 경우 

만약 301 리다이렉트 되는 경우 **'301 Moved Permanently'와 같이 나타나며 리다이렉트 된 페이지 결과는 출력되지 않습니다**. 하지만 -L을 사용하면 리다이렉트 된 페이지의 결과를 볼 수 있습니다. 즉 L flag 옵션을 사용하는 경우 리다이렉트된 페이지 결과까지 알 수 있습니다. 예를들어 만약 webisfree.com이 redirect되는 경우 아래처럼 사용합니다.  
curl webisfree.com  
  
curl -L webisfree.com  
  
아래 명령어는 redirect 된 페이지의 결과를 출력하게됩니다.

