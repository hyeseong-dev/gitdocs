# Docker img로 Apache & PHP 개발환경 구축

## PHP 개발환경 구축



#### docker ps -a 

```text
docker ps -a # 도커 컨테이너 리스트를 모두 출력
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
e8bfedabc155        example             "apachectl -D FOREGR…"   23 hours ago        Up 23 hourshours         0.0.0.0:80->80/tcp   serene_bose
```

이전 시간에 만들었던 아파치 컨테이너 하나가 있습니다. 

#### **docker rm -f $\(docker ps -a -q\)**

-f \(force\) 강제로 모두 지우겠다는 옵션이며 뒤의 $\(docker ps -a -q\)는 도커 컨테이너 전부를 의미해요.   

```text
docker rm -f $(docker ps -a -q) # $(명령문)은 컨테이너 전부를 삭제함                                       
e8bfedabc155
```

삭제된 컨테이너의 id가 출력되네요.   
시작에 앞서서  불필요한 컨테이너들을 말끔히 정리했습니다. 



#### Dockerfile 수정 

이전 시간 "Docker 설치 및 Dockerfile로 웹 서버 구동'에 만들었던 Docker파일을 수정 할 게요. 

```text
root@ip-172-31-35-20:/# cd /home/ubuntu/example
root@ip-172-31-35-20:~/example# ls
Dockerfile
root@ip-172-31-35-20:~/example# vi Dockerfile
```

Dockerfile 내부를 보면 Apache2만 설치한 모습이 보이조?  
이제는 **아파치 설치 이후 PHP까지 설치할수 있게 추가적으로 RUN명령어를 입력**해볼게요. 

{% code title="수정 전 Dockerfile" %}
```text
FROM ubuntu:18.04
MAINTAINER Hyeseong lee <hyeseong43@gmail.com>

RUN apt-get update
RUN apt-get install -y apache2

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND" ]
```
{% endcode %}



{% code title="수정한 Dockerfile" %}
```text
FROM ubuntu:18.04
MAINTAINER Hyeseong lee <hyeseong43@gmail.com>

RUN apt-get update
RUN apt-get install -y apache2
RUN apt-get -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND" ]
```
{% endcode %}

 이전 버전인 PHP5.6 설치를 위해 먼저 software-properties-common이라는 명령어 6번째 줄의에  입력할게요. 

> software-properties-common은 제 블로그글에서 검색해서 관련 내용을 확인해보세요.



7번째 줄에는 PHP5.6을 설치할수 있도록하는 추가 명령어를 입력할게요. 







---



## Volume 공유를 통한 PHP 소스코드 동작 

Becoming a super hero is a fairly straight forward process:

```
$ give me super-powers
```

{% hint style="info" %}
 Super-powers are granted randomly so please submit an issue if you're not happy with yours.
{% endhint %}

Once you're strong enough, save the world:

{% code title="hello.sh" %}
```bash
# Ain't no code for that yet, sorry
echo 'You got to trust me on this, I saved the world'
```
{% endcode %}



