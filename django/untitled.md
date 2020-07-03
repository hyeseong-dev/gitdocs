# Project Setup

본격적인 프로젝트 구성을 진행해 볼게요.   
이를 위해 **가상환경**을 만들어 볼게요. 



### 가상환경

#### 1\) 설치 

```text
$ python -m venv 가상환경이름

예. $ python -m venv fc_venv
```

#### 2\) 실행

```text
$ source 가상환경명/bin/activate (mac, 리눅스 사용자)

또는 

$ 가상환경명/Script/activate (window 사용자)
```

### Django 패키지 설치 

```text
$ pip install django
```

## 프로젝트 & 앱 설치 및 구

#### 프로젝트 시작 

```text
django-admin startproject 프로젝트명

예. django-admin startproject fc_django
```

그럼 fc\_django라는 root 디렉토리가 생성되요. cd 명령어로 안으로 들어가보면 다시 동일한 이름의 fc\_django라는 프로젝트 폴더가 보일거에요.   
또한 manage.py라는 파일 역시 보여요. 

#### 앱 시작 

쇼핑몰 웹을 만들것이기에 사용자, 상품, 주문 이 세가지 앱을 만들어 볼거에요. 

```text
django-admin startapp 앱이름

예. 
django-admin startapp fcuser
django-admin startapp product
django-admin startapp order
```



