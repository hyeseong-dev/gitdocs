# PHP컨테이너&MySQL컨테이너 연동



PHP와 MySQL 컨테이너를 띄워서 서로 연동해 볼게요. 

###  

 이미 example 폴더에서 Dockerfile을 만들어서 php이미지를 build해 보았어요. 

```text
root@ip-172-31-35-20:/# cd /home/ubuntu/example
root@ip-172-31-35-20:~/example#
root@ip-172-31-35-20:~/example# ls
Dockerfile  html
```

 다시 한번 이 Dockerfile을 작성해 볼게요. 

### Dockerfile 작성 

 우리가 원하는 PHP &lt;-- --&gt; MySQL 연동을 위해선 추가적으로 단하나의 패키지만 더 설치하도록 Dockerfile을 작성해주면 되요. 

그건 바로  **RUN apt-get install -y php5.6-mysql** 입니다.   
이 php5.6-mysql 패키지를 통해서 

{% tabs %}
{% tab title="EC2 server" %}
```text
vi Dockerfile 
```
{% endtab %}

{% tab title="Dockerfile" %}
```
FROM ubuntu:18.04
MAINTAINER Hyeseong lee <hyeseong43@gmail.com>

ENV DEBIAN_FRONTEND=nointeractive

RUN apt-get update
RUN apt-get install -y apache2
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ondrej/php
RUN apt-get update
RUN apt-get install -y php5.6

# Connect PHP & MySQL
RUN apt-get install -y php5.6-mysql

EXPOSE 80

CMD ["apachectl", "-D", "FOREGROUND" ]

~
```
{% endtab %}
{% endtabs %}



