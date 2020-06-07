# docker-compose

##  삭제 방법 

 도화지 상태에서 최신 버전과 매칭하기 위해서 일단 삭제 명령어를 실행합니다. 

```text
sudo apt remove docker-compose
```

## 설치 방법 

```text
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

##  버전확인 

```text
sudo docker-compose -v
```

## docker-compose.yml 작성과 활용 

디렉토리를 만들고 docker-compose.yml 파일을 작성해볼게요.   
vi or nano 에디터로 만들면 노가다이니, jupyter notebook 이용하면 복붙하면 금방이겠조?  
  
파일 내용을 살펴보면, 워드프레스에서 사용할 MySQL와 워드프레스를 설치하고 MySQL 도커 컨테이너와 연결하게 되요. 

{% code title="docker-compose.yml" %}
```text
version: '3.3'
services:
   db:
     image: mysql:5.7
     volumes:
       - db_data:/var/lib/mysql
     ports:
       - "3306:3306"
     restart: always
     environment:
       MYSQL_ROOT_PASSWORD: somewordpress
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD: wordpress
   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     restart: always
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD: wordpress
       WORDPRESS_DB_NAME: wordpress
volumes:
    db_data: {}
```
{% endcode %}

## Docker-compose 실행 

```text
sudo docker-compose up -d
docker ps
```

위 명령어를 실행하면 아래와 같이 컨테이너 2개가 잘 생성 된걸 확인 할수 있어요.

![](../.gitbook/assets/image%20%28231%29.png)



