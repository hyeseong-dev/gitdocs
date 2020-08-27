# Django 개념정리

### 목차

#### - MVC, MFV

#### - Django 개념

#### - Projcet와 App

#### - setting.py

#### - manage.py

## MVC & MTV

* Model : 안전하게 데이터를 저장    
* View  : data를 적절하게 유저에게 보여줌   
* Control, Template\(Django\) : 사용자의 입력과 이벤트에 반응하여 Model과 View를 업데이트 

### Django 개념 모형도

Client의 request는 django 프로젝트 안에 있는 urls.py에 처음으로 전달된다. urls.py에서 요청을 views.py로 보내고 저장되어 있는 데이터가 필요하다면 models.py에서 database를 가져와서 models.py로 데이터를 보내고 models.py에서 views.py로 실질적인 데이터를 보낸다. view는 template로 유저에게 보여줄 데이터를 보내고 template가 js나 html과 같은 다양한 형태의 UI형태로 만들어서 Client에게 응답하는 형태가 django의 간단한 흐름이다.

위의 말을 더~~~길게 풀어 써볼게요.

처음 Web Browser에서 사용자가 이것저것 하게 됩니다. 즉, 이벤트가 발생한다는 말이에요.  
\(여기서 말하는 이벤트란?! URL을 click, form에 data를 입력! 다양한 Action을 의미함\)

-&gt; 그럼 두번째로, URL Dispatcher에서 클라이언트가 요청한 URL을 분석해요!

-&gt; 그럼 분석한 URL에 가장 적합한 View로 전달되요.  
이곳 View에서는 사용자의 요청을 받아 처리하는 작업을 하게 됩니다.  
\(1\) DB의 어디에 접근하여  
\(2\) Which 데이터를 가공해서 알려줄것인지를 -&gt; Model에서 실질적인 DB와의 실질적인 connection을통해 데이터를 가져오게 됩니다.

-&gt; 그럼 DB에서 다시 Model로 데이터를 보내주고 -&gt; View에 다시 전달되고, 이 View가 클라이언트가 실질적으로 접하게될 데이터를 template에게 전송함.  
예를들어 Javascript or HTML과 같은 다양한 형태의 유저 인터페이스를 만들어서 다시 웹브라우저에 연결하게 됩니다.

위 과정은 졸라 복잡합니다. 아래 그림을 보면서 차근차근 다시 되새김질하세요.

![django&#xBAA8;&#xD615;](https://media.vlpt.us/images/nhk721/post/9cf4b45c-1317-438b-bbe8-dd786b7e5c5d/image.png)

### 세분화한 Django의 workflow

장고라는 웹 프로젝트를 생성하게 되면, 그 안에는 다양한 파일들이 생성하게 되요.  
우선 녹색으로 표시된 부분이 실질적으로 다루게 될 부분입니다.

빨간색의 웹 브라우저단이 가장 상위에 배치되어 있습니다. 엔진스나 아파치를 웹서버로 사용하게 될것입니다.

그리고 가장 아래쪽 파란색중 DATABASE를 보면 mysql,sqlite등이 있습니다.

회색으로 표시된 부분이 이 middleware가 django를 support하는 역할을 합니다.

우선 브라우저단에서 데이터 요청을 하게되면 -&gt;WSGI로 신호가 들어오게 됩니다.\(실제적으로 WSGI를 건들일은 거의 없습니다.\)

WSGI의 역할은? 웹서버와 Django를 적적하게 결합시켜줘요. 여러분들은 엔진스 혹은 아파치등의 웹서버를 사용하게 될 것입니다. 해당 웹서버의 적절한 설정을 통해서 웹서버와 + Django가 결합하게 되요.

-&gt; URL RESOLUTION\(urls.py\)의 코드에서 WSGI의 신호를 받게 됩니다. url.py는 정규표현식으로 구성되어있습니다.  
-&gt; 정규 표현식에 맞게 -&gt; 특정한 View\(View.py\)로 보내지게 됩니다.

> 그래서 views.py가 저희가 실질적으로 가장 많이 작성하게될 부분이에요.

이제 View에서 요청을 판단하게 됩니다.  
1. 사용자 요청에 의해서 db에 데이터를 입력할지?!  
2. 아니면 db에서 data를 꺼내 와서 사용자에게 리스트를 보여줄건지.

이후 Model\(Models.py\)에 신호를 보냅니다. 그럼 Model은 DB로부터 데이터를 가져와 Class\(여기선 변수!\)로 넣고, 결국 변수를 조작한다는 말이에요.

과거 DB에서 쿼리문을 만들고 변수에 data를 넣고 조작하는 번거로운 과정을 여러번 했습니다. 하지만 이를 통합한 것이 models.py입니다. 즉, models.py에서는 변수만! 지정하게 되면 managers라는 부분이 알아서 models.py &lt;--&gt; DATABASE간의 매개체 역할및 조정자 역할을 한다. 결국 Django를 사용하면서 SQL QUERY를 작성할 필요가 없어요!

이제 다시 View는 DB에 접근하여 데이터를 가져오고 가공을 했습니다. 이후 사용자에게 보여주기위한 UR작업을 진행합니다.  
그러기 위해선 클라이언트가 TEMPLATE\(EXAMPLE.HTML\)를 만들어서 다시 웹서버로 전송하게 됩니다.

TEMPLATE는 HTML파일입니다. HTML파일안에 컨트롤과 관련된 다양한 LOGIC을 삽입할 수 있는데요. 하지만 대단한 복잡한 움직임이 있지는 않아요. 결국 views.py에서 받은 data를 어떻게 HTML로 잘 보여줄지를 결정하는 스크립트 파일들이 이 template\(example.html\)에 담겨지게 됩니다.

이 때 저희는 다양한 form을 작성하게 되겠조? HTML태그를 통해서 파일을 입력하거나, 게시물을 작성할때 쓰는 form들을 만드는데, 이런것들은 FORM\(form.py\)를 통해서 매우 손쉽게 관리 할 수 있습니다.

이는 MODEL\(models.py\)과 TEMPLATE\(example.html\)를 통해서 사용자들이 쓰는 UI가 손쉽게 관리된다라는 말이기도 합니다.

![&#xC7A5;&#xACE0;detail\_image](https://media.vlpt.us/images/nhk721/post/1d18bc5f-a295-4baf-956f-bdd9de00d630/image.png)

하나의 프로젝트는 하나의 웹사이트라고 생각하면 됩니다.  
이 프로젝트에는 다양한 기능들이 존재합니다.  
이 의미있는 기능들이 App하나로 관리 할 수 있습니다. \(예, 1. blog가 하나의 큰 기능이 될 수 있어요.\) 결국 그게 하나의 어플리케이션이 된다는 말이며 쇼핑몰역시 하나의 app이 될수 있어요.  
결국 큰 웹사이트의 블로그, 게시판, 전자상거래와 관련된 기능들을 각각 분리해서 저희들이 프로그래밍을 각각 할 수 있어요.  
어떤 프로젝트에서 만들어진 외부앱은 또 다시 다른 프로젝트에서 하위 어플리케이션으로 재사용 될 수 있어요.

### Project와 App

* 프로젝트 생성

  > django-admin startproject tutorial\(프로젝트이름\)  
  > 그럼 아래와 같은 directory 구조를 볼 수 있습니다.

  * manage.py
  * toturial
    * **init**.py
    * settings.py
    * urls.py
    * wsgi.pyy
    * app 생성

      > ./manage.py startapp community\(앱이름\)
  * community
    * admin.py      : 관리자 권한을 가진 사용자가 볼 수 있는 페이지
    * \_\_init\_\_.py
    * migrations    : db와 관련된 폴더
      * admin.py
    * models.py     : db와 관련된 다양한 역할을 수행함.
    * tests.py
    * views.py      : db로부터 가져온 data를 가공하는 역할
  * manage.py   
  * tutorial 
    * \_\_init\_\_.py  
    * settings.py   
    * urls.py 
    * wsgi.py 

프로젝트 내부에 app 생성

### Settings.py

\(전체 파일들을 설정하는 파일\)

* DEBUG :   

   디버그 모드 설정 ex\) 에러를 확인하고 싶을 때 True로 두면 변수 상태 확인 가능. 그러나 배포시에는 False로 설정해야함   

* INSTALLED\_APPS :     

   pip로 설치한 앱 또는 본인이 만든 app을 추가

* MIDDELWARE\_CLASSES :     

   reqeust와 response 사이의 주요 기능 레이어. 여러분들이 크게 신경쓸 부분은 아니에요. ex\) 인증 보안

* TEMPLATES :  

   django template 관련 설정 , 실제 뷰\(html,변수\)

* DATABASES :  

   데이터베이스 엔진의 연결 설정

* STATIC\_URL :     

   정적 파일의 URL\(css,javascript,image등\)

### manage.py

주요 명령어

* startapp - 앱 생성
* runserver - 서버 실행
* createsuperuser - 관리자 생성
* makemigrations app - app의 모델 변경 사항 체크
* migrate - 변경 사항을 DB에 반영
* shell - 쉘을 통해 데이터를 확인
* collectstatic - static 파일을 한곳에 모음

> ./manage.py runserver 0.0.0.0:8080

\(runserver까지만 딱 쓰면 8000번포트를 기본값으로 잡고 실행됨. 하지만 외부에서 접근할 수 없음. 그래서 8080번포트를 이용해서 외부 접근을 가능하게함.\)목차

#### - MVC, MFV

#### - Django 개념

#### - Projcet와 App

#### - setting.py

#### - manage.py

## MVC & MTV

* Model : 안전하게 데이터를 저장    
* View  : data를 적절하게 유저에게 보여줌   
* Control, Template\(Django\) : 사용자의 입력과 이벤트에 반응하여 Model과 View를 업데이트 

### Django 개념 모형도

Client의 request는 django 프로젝트 안에 있는 urls.py에 처음으로 전달된다. urls.py에서 요청을 views.py로 보내고 저장되어 있는 데이터가 필요하다면 models.py에서 database를 가져와서 models.py로 데이터를 보내고 models.py에서 views.py로 실질적인 데이터를 보낸다. view는 template로 유저에게 보여줄 데이터를 보내고 template가 js나 html과 같은 다양한 형태의 UI형태로 만들어서 Client에게 응답하는 형태가 django의 간단한 흐름이다.

위의 말을 더~~~길게 풀어 써볼게요.

처음 Web Browser에서 사용자가 이것저것 하게 됩니다. 즉, 이벤트가 발생한다는 말이에요.  
\(여기서 말하는 이벤트란?! URL을 click, form에 data를 입력! 다양한 Action을 의미함\)

-&gt; 그럼 두번째로, URL Dispatcher에서 클라이언트가 요청한 URL을 분석해요!

-&gt; 그럼 분석한 URL에 가장 적합한 View로 전달되요.  
이곳 View에서는 사용자의 요청을 받아 처리하는 작업을 하게 됩니다.  
\(1\) DB의 어디에 접근하여  
\(2\) Which 데이터를 가공해서 알려줄것인지를 -&gt; Model에서 실질적인 DB와의 실질적인 connection을통해 데이터를 가져오게 됩니다.

-&gt; 그럼 DB에서 다시 Model로 데이터를 보내주고 -&gt; View에 다시 전달되고, 이 View가 클라이언트가 실질적으로 접하게될 데이터를 template에게 전송함.  
예를들어 Javascript or HTML과 같은 다양한 형태의 유저 인터페이스를 만들어서 다시 웹브라우저에 연결하게 됩니다.

위 과정은 졸라 복잡합니다. 아래 그림을 보면서 차근차근 다시 되새김질하세요.

![django&#xBAA8;&#xD615;](https://media.vlpt.us/images/nhk721/post/9cf4b45c-1317-438b-bbe8-dd786b7e5c5d/image.png)

### 세분화한 Django의 workflow

장고라는 웹 프로젝트를 생성하게 되면, 그 안에는 다양한 파일들이 생성하게 되요.  
우선 녹색으로 표시된 부분이 실질적으로 다루게 될 부분입니다.

빨간색의 웹 브라우저단이 가장 상위에 배치되어 있습니다. 엔진스나 아파치를 웹서버로 사용하게 될것입니다.

그리고 가장 아래쪽 파란색중 DATABASE를 보면 mysql,sqlite등이 있습니다.

회색으로 표시된 부분이 이 middleware가 django를 support하는 역할을 합니다.

우선 브라우저단에서 데이터 요청을 하게되면 -&gt;WSGI로 신호가 들어오게 됩니다.\(실제적으로 WSGI를 건들일은 거의 없습니다.\)

WSGI의 역할은? 웹서버와 Django를 적적하게 결합시켜줘요. 여러분들은 엔진스 혹은 아파치등의 웹서버를 사용하게 될 것입니다. 해당 웹서버의 적절한 설정을 통해서 웹서버와 + Django가 결합하게 되요.

-&gt; URL RESOLUTION\(urls.py\)의 코드에서 WSGI의 신호를 받게 됩니다. url.py는 정규표현식으로 구성되어있습니다.  
-&gt; 정규 표현식에 맞게 -&gt; 특정한 View\(View.py\)로 보내지게 됩니다.

> 그래서 views.py가 저희가 실질적으로 가장 많이 작성하게될 부분이에요.

이제 View에서 요청을 판단하게 됩니다.  
1. 사용자 요청에 의해서 db에 데이터를 입력할지?!  
2. 아니면 db에서 data를 꺼내 와서 사용자에게 리스트를 보여줄건지.

이후 Model\(Models.py\)에 신호를 보냅니다. 그럼 Model은 DB로부터 데이터를 가져와 Class\(여기선 변수!\)로 넣고, 결국 변수를 조작한다는 말이에요.

과거 DB에서 쿼리문을 만들고 변수에 data를 넣고 조작하는 번거로운 과정을 여러번 했습니다. 하지만 이를 통합한 것이 models.py입니다. 즉, models.py에서는 변수만! 지정하게 되면 managers라는 부분이 알아서 models.py &lt;--&gt; DATABASE간의 매개체 역할및 조정자 역할을 한다. 결국 Django를 사용하면서 SQL QUERY를 작성할 필요가 없어요!

이제 다시 View는 DB에 접근하여 데이터를 가져오고 가공을 했습니다. 이후 사용자에게 보여주기위한 UR작업을 진행합니다.  
그러기 위해선 클라이언트가 TEMPLATE\(EXAMPLE.HTML\)를 만들어서 다시 웹서버로 전송하게 됩니다.

TEMPLATE는 HTML파일입니다. HTML파일안에 컨트롤과 관련된 다양한 LOGIC을 삽입할 수 있는데요. 하지만 대단한 복잡한 움직임이 있지는 않아요. 결국 views.py에서 받은 data를 어떻게 HTML로 잘 보여줄지를 결정하는 스크립트 파일들이 이 template\(example.html\)에 담겨지게 됩니다.

이 때 저희는 다양한 form을 작성하게 되겠조? HTML태그를 통해서 파일을 입력하거나, 게시물을 작성할때 쓰는 form들을 만드는데, 이런것들은 FORM\(form.py\)를 통해서 매우 손쉽게 관리 할 수 있습니다.

이는 MODEL\(models.py\)과 TEMPLATE\(example.html\)를 통해서 사용자들이 쓰는 UI가 손쉽게 관리된다라는 말이기도 합니다.

![&#xC7A5;&#xACE0;detail\_image](https://media.vlpt.us/images/nhk721/post/1d18bc5f-a295-4baf-956f-bdd9de00d630/image.png)

하나의 프로젝트는 하나의 웹사이트라고 생각하면 됩니다.  
이 프로젝트에는 다양한 기능들이 존재합니다.  
이 의미있는 기능들이 App하나로 관리 할 수 있습니다. \(예, 1. blog가 하나의 큰 기능이 될 수 있어요.\) 결국 그게 하나의 어플리케이션이 된다는 말이며 쇼핑몰역시 하나의 app이 될수 있어요.  
결국 큰 웹사이트의 블로그, 게시판, 전자상거래와 관련된 기능들을 각각 분리해서 저희들이 프로그래밍을 각각 할 수 있어요.  
어떤 프로젝트에서 만들어진 외부앱은 또 다시 다른 프로젝트에서 하위 어플리케이션으로 재사용 될 수 있어요.

### Project와 App

* 프로젝트 생성

  > django-admin startproject tutorial\(프로젝트이름\)  
  > 그럼 아래와 같은 directory 구조를 볼 수 있습니다.

  * manage.py
  * toturial
    * **init**.py
    * settings.py
    * urls.py
    * wsgi.pyy
    * app 생성

      > ./manage.py startapp community\(앱이름\)
  * community
    * admin.py      : 관리자 권한을 가진 사용자가 볼 수 있는 페이지
    * \_\_init\_\_.py
    * migrations    : db와 관련된 폴더
      * admin.py
    * models.py     : db와 관련된 다양한 역할을 수행함.
    * tests.py
    * views.py      : db로부터 가져온 data를 가공하는 역할
  * manage.py   
  * tutorial 
    * \_\_init\_\_.py  
    * settings.py   
    * urls.py 
    * wsgi.py 

프로젝트 내부에 app 생성

### Settings.py

\(전체 파일들을 설정하는 파일\)

* DEBUG :   

   디버그 모드 설정 ex\) 에러를 확인하고 싶을 때 True로 두면 변수 상태 확인 가능. 그러나 배포시에는 False로 설정해야함   

* INSTALLED\_APPS :     

   pip로 설치한 앱 또는 본인이 만든 app을 추가

* MIDDELWARE\_CLASSES :     

   reqeust와 response 사이의 주요 기능 레이어. 여러분들이 크게 신경쓸 부분은 아니에요. ex\) 인증 보안

* TEMPLATES :  

   django template 관련 설정 , 실제 뷰\(html,변수\)

* DATABASES :  

   데이터베이스 엔진의 연결 설정

* STATIC\_URL :     

   정적 파일의 URL\(css,javascript,image등\)

### manage.py

주요 명령어

* startapp - 앱 생성
* runserver - 서버 실행
* createsuperuser - 관리자 생성
* makemigrations app - app의 모델 변경 사항 체크
* migrate - 변경 사항을 DB에 반영
* shell - 쉘을 통해 데이터를 확인
* collectstatic - static 파일을 한곳에 모음

> ./manage.py runserver 0.0.0.0:8080

\(runserver까지만 딱 쓰면 8000번포트를 기본값으로 잡고 실행됨. 하지만 외부에서 접근할 수 없음. 그래서 8080번포트를 이용해서 외부 접근을 가능하게함.\)

