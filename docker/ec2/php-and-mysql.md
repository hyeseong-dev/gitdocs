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
이 php5.6-mysql 패키지를 통해서 php와 mysql을 서로 연동할수 있게 되는거에요. 

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



Dockerfile을 위와 같이 작성하고 Vim에디터를 나와주세요. 

### Docker 이미지 빌드 

```text
docker build -t example . 
```

 도커 이미지가 정상적으로 빌드되었으면,  아래 명령어로 example 이미지 이름을 찾을 수 있게 될거에요. 

```text
docker images 
```

####  Run명령어로 컨테이너를 만들고 실행해볼게요. 

아래 명령어로 컨테이너를 구동해 볼게요. 

```text
docker run -p 80:80 -v /home/ubuntu/example/html:var/www/html example
```



주피터 노트북에서 터미널을 하나 더 새롭게 만들어 주세요.   
그리고 php문서를 작업해 볼게요.  ls명령어를 실행해보면 이전에 우리가 작없했던 index.php파일이 보일거에요.

```text
> cd /home/ubuntu/example/html
> ls 
index.php
> cat index.php # 해당 파일의 내용을 출력하게함cat(concatenate)  
<?php phpinfo(); ?>
```

### index.php 파일 수정

vi에디터로 index.php파일을 수정하는데에는 한계가 있다면 긴 소스코드를 작성하는데 있어요. 

```text
vi index.php
```

vi 에디터로 수정하는거 대신 Jupyter로 간편하게 수정해볼게요. 

/home/ubuntu/example/html 경로로 가시면 되요. 

![](../../.gitbook/assets/image%20%28215%29.png)

php 소스코드를 작성해볼게요.   
php5.6에서 mysql에 접속하는 기본적인 문법을 다뤄 볼게요.

일반적으로 $conn객체를 만들어 mysql 접속 관련 객체 초기화 할수 있어요.   

{% tabs %}
{% tab title="index.php" %}
```text
<?php 
    $conn = mysqli_connect(
    '{3.22.225.2}',
    'test',
    'password',
    'TEST',
    '9876'
    );
    if(mysqli_connect_errno()){
        echo "Failed to connect to MySQL: ".mysqli_connect.error()
    }
?>

```
{% endtab %}
{% endtabs %}

