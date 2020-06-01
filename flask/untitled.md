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



