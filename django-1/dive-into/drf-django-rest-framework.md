# DRF\(Django Rest Framework\)

## RESTful이란

RESTful이란 Representational State Transfer의 줄임말이다. 먼저 REST에 대해서 소개를 하자면, http의 url과 http method\(GET, POST, PUT, DELETE\)를 사용해서 API 가독성을 높인 구조화된 시스템 아키텍쳐\(framework\)라고 생각하면 된다. 하나의 URL로 우리는 최소 4가지의 HTTP method를 전송할 수 있다.

스마트폰이 등장하기 전 IT 기업들은 웹 페이지를 보여주는 웹서버만 구현하면 됬다. 그 웹 서버에서 DB 서버의 데이터도 읽어오고 사용자들이 글을 남기면 DB 서버에 저장까지 하는 기능을 모두 담당했다. 하지만 스마트폰이 출시되고, 어플리케이션의 등장으로 더이상 웹으로만 서비스를 제공하는 것에는 한계가 있었다.

따라서 HTML로 렌더링 하는 웹서버가 아닌, JSON 혹은 XML 과 같은 형식을 통해서 데이터를 다루는 별도의 API 서버가 필요했다. 스마트폰 어플과 웹에서 동일한 기능을 제공하는데 기존의 웹서버를 계속 사용하면 매번 HTML을 읽어서 해당 태그에 있는 정보를 찾아내는 일은 정말 미친짓이기 때문이다. \(덜덜\)

따라서 RESTful 아키텍쳐를 HTTP Method와 함께 사용해 웹, 데스크탑 앱, 스마트폰 어플들까지 하나의 API 서버를 생성할 수 있다.

Django 또한 View 클래스 자체가 RESTful 한 서버를 만들기에 최적인 프레임워크다.



## DRF\(Django Rest Framework\)

![](https://blog.kakaocdn.net/dn/dIOe6h/btqwpm6Ok93/fiVWJIWflUJbaKW0kJmP00/img.png)

DRF\(Django Rest Framework\)란 그래서 Django 안에서 RESTful API 서버를 쉽게 구축할 수 있도록 도와주는 오픈소스 라이브러리다.

Django REST framework를 사용하는 이유는 아래와 같다.

* 웹 브라우저 API는 범용성이 크다. 개발을 쉽게 만들어준다.
* 인증 정책에 OAuth1, OAuth2 를 위한 추가적인 패키지가 추가되어 있는 경우
* 시리얼라이즈 기능을 제공해준다. \(DB data -&gt; JSON\)
* 문서화 및 커뮤니티 지원이 잘 되어있다.



#### Serializer 란

DRF의 가장 매력적인 기능으로는 Serializer가 있다.

Serializer란 말 그대로 직렬화하는 클래스로서, 사용자의 DB안에 사용자 프로필 사진, 이메일, 이름, 성별이 있다고 가정하면 사용자 모델 인스턴스를 JSON 형태 혹은 Dictionary 형태로 직렬화 할 수 있다.

예를 보면,

```text
user = User(email="user@user.user", name="user", sex="Female", profile_image="user.png")
UserSerializer(user).data{
	"email" : "user@user.user",
    "name" : "user",
    "sex" : "female",
    "profile_image" : "user.png"
}
```

위와 같은 사용자가 있다면 DRF의 serializer를 통해 모델 인스턴스를 직렬화 할 수 있다.

실 사용시에는 만약 사용자 정보를 열람하는 URL이 /serializer/user/&lt;user id&gt;/가 있고 해당 View에는 user\_id의 해당하는 모델 인스턴스의 정보를 리턴한다고 가정하자. 그렇게 되면 만약 우리가 /serializer/user/1/ 이라는 URL로 요청했을 시 user\_id가 1인 사용자의 정보를 JSON 형태로 응답받을 수 있다.

이는 사용자 프로필 페이지에 접근했을 때 사용하는 View 라고 하면 사용자 페이지에 들어갈 때 마다 해당하는 사용자의 user\_id만 URL에 입력해주게되면 각 사용자의 정보를 JSON 형태로 응답 받을 수 있을 것이다.

위와 같은 기능을 하는 Serializer를 ModelSerializer라고 부른다.



#### Django REST Framework 설치

```text
pip install djangorestframework
```

위의 명령어를 터미널에서 실행시키자.

다음으로는 django settings.py 파일에서 INSTALL\_APP 부분에 'rest\_framework' 를 명시해주자.

```text
INSTALL_APPS = [
	...
    'rest_framework', #add
]
```



### Django REST Framework 튜토리얼 문서

[https://www.django-rest-framework.org/tutorial/quickstart/](https://www.django-rest-framework.org/tutorial/quickstart/)[ Quickstart - Django REST frameworkWe're going to create a simple API to allow admin users to view and edit the users and groups in the system. Create a new Django project named tutorial, then start a new app called quickstart. \# Create the project directory mkdir tutorial cd tutorial \# Crewww.django-rest-framework.org](https://www.django-rest-framework.org/tutorial/quickstart/)

#### 참고한 블로그

[https://yunhookim.tistory.com/7](https://yunhookim.tistory.com/7)[ DRF\(Django Rest framework\) 소개DRF\(Django Rest framework\) 소개 DRF\(Django Rest Framework, http://www.django-rest-framework.org\)란 Django 안에서 RESTful API 서버를 쉽게 구축할 수 있도록 도와주는 오픈 소스 라이브러리이다. RESTful이..yunhookim.tistory.com](https://yunhookim.tistory.com/7)



