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



