# Environment



{% code title="\# 플라스크의 기본 구조" %}
```text

$> mkdir webapp
 /flaskapp (helloflask)
     - /static
         - /css
         - /images
         - /js
     - /templates
     - __init__.py
```
{% endcode %}

**---**

pyweb ---1. helloflask\(5000포트\)  
            ---2. blog\(6000번포트\)   


1번, 2번, ... 전체를 Webapplication이라고 말하고요. 개별적인 하나 하나를 Web Context라고 말해요.    
즉 개별적인 하나하나가 사이트가 될 수 있으며 우리가 구성해서 만들수도 있어요.   
서버 한대로 여러개의 서비스를 구현 하는것도 가능해요. 

flaskapp은 결국 하나의 서비스 안에 static, templates, \_\_init\_\_.py 디렉토라와 파일 구조를 갖고 있어요.   
pyweb 디렉토리의 서브 디렉토리인 helloflask와 blog 역시 웹 서비스가 되고 기본적으로 동일한 디렉토리구조와 파일 구조를 갖고 있을거에요. 

### static 

정적 파일이 존재하는 곳입니다. 예를들어 이미지 파일, js파일 , css파일들은 외부에서 요청이 들어오면 별도의 연산작업없이 주게 되조. 정적상태로 준다는 말이에요. 

### templates 

{% code title="/templates/index.html" %}
```text
ttt 한글 
{%if true %}
    TTT
{% endif %}qqq
pppppppppppppp111
```
{% endcode %}

templates 디렉토리에는 html파일들이 모여 있습니다. helloflask/templates/index.html 이 구조를 가지고 있어요. 

오래전 방식이지만 만약 게시판을 만들고 싶다면 templates 디렉토리안에 bbs라는 디렉토리를 만들어 list.html, detai.html, view.html 파일들을 구성할수 있어요. 

```text
C:.
├─flaskapp(helloflask)    
│  
├─static
│  ├─css
│  ├─images
│  └─js
├─templates
│    │  index.html
│    │
│    └─bbs #게시판
│        ├─list.html
│        ├─detail.html
│        ├─view.html
│
├-start_flask.py 
```

### \_\_init\_\_.py 

flaskapp\(helloflask\)모듈의 시작 지점을 말해요. \_\_init\_\_.py 파이썬의 생성자라고 다들 알고 계시조?  
여기서 \_\_init\_\_.py는 웹 애플리케이션을 구동하는 녀석이에요.   
모든 정보를 가지고 메모리에 올리는 핵심적인 역활을 \_\_init\_\_.py가 하게되요.   




