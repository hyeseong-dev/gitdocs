# JSON이란?

#### json 파일이 도대체 뭐죠???

   
 새로운 언어나 라이브러리로 코딩 좀 해볼라하면 플렛폼을 먼저 설정해야 하고, 플렛폼 설정 좀 해볼라하면 구글링해가면서 내 os에 맞춰가야 하는데 툭 하면 튀어나오는 것이 json파일이다. 도대체 뭔가 해서 정리해보았다.\(이번에 Ruby를 window에서 해볼라다가 4시간 날렸다.\)  
  
  


**json 이란?**

  
1\) Java Script Object Notation 의 약자이다.  
  
2\) json은 단순한 데이터 포멧이다. **데이터를 표시하는 방법**일 뿐이다.   
  
3\) json을 쓰는 이유 : json파일이 가지고 있는 데이터를 받아서 객체나 변수에 할당해서 사용하기 위함이다  
  
4\) json의 구조  
  1. Object\(객체\)  
     - name/value 의 순서쌍으로 set이다.  
     - {} 로 정의된다. ex\) { "이름" : "홍길동" }  
  2. Array\(배열\)  
     - 그 배열이 맞다. ex\) \[ 10, "array", 32 \]  
  
5\) json의 예  
  
{  
"이름" : "홍길동",  
"나이" : 22,  
"특기" : \["배구", "야구"\]  
}  
  


**6\) json은 왜 쓰는가?**

  
위의 예제 json파일의 이름을 ' 길동info.json '이라고 하자.  
  
 이 정보\(데이터\)를 서로 주고 받기위해 여러가지의 형식으로 넘겨줄 수 있겠지만  
json은 다른 포멧에 비해 경량화된 데이터 포멧이다.  
  
 그렇기에 A가 B에게 홍길동의 정보가 담긴 data를 넘겨주기 위해 json포멧으로 포장하여 넘겨주는 것이다.  
  


**7\) json parsing 이란?**

 A로부터 B가 길동info.json 파일을 받았다고 하면 이 파일에 담긴 data를 찾아 객체나 변수에 할당하기위해 json파일 내에서 특정 data만을 가져와야 한다.  
이렇게 json파일 내의 특정 data만 추출하는 것을 json parsing이라고 한다.  
  
  


**8\) Visual Studio Code 의 예**

  
 vscode의 사용자 설정은 아래와 같인 json파일로 가능하다.  
아래 파일의 이름은 settings.json이다. 그렇다... json파일이다.[![](https://mblogthumb-phinf.pstatic.net/MjAxODA1MTdfMjkw/MDAxNTI2NDkyMjE3NDQx.bYX6ZqCS5cQuFMuyWtyeJunW-yc2bYr64X9mFsbTWf4g.mpD-bLQyBIu8Zakvp0a0B1vaxiNglQJs-RKRIIVwzj0g.PNG.demonic3540/image.png?type=w800)](https://m.blog.naver.com/PostView.nhn?blogId=demonic3540&logNo=221277604043&proxyReferer=https:%2F%2Fwww.google.com%2F#)

json파일이 그러하듯 위에선 Object 내에 name과 value 순서쌍으로 설정요소들이 정리되어 있다.  
  
 그 중 workbench.colorTheme 라는 name의 value를 Red로 바꿔보면 아래와 같이 vscode의 테마가 빨갛게 변한다.  
[![](https://mblogthumb-phinf.pstatic.net/MjAxODA1MTdfMjQ0/MDAxNTI2NDkyMzYxNzY5.eSJ8jHdrcuS49ZoCoL8OYbHlOlzT24_vJ05DwsvpO-Ug.qVjFcquwMjTwwtiOXTkqrKROs0jCn2gRUwtxXxXKPMog.PNG.demonic3540/image.png?type=w800)](https://m.blog.naver.com/PostView.nhn?blogId=demonic3540&logNo=221277604043&proxyReferer=https:%2F%2Fwww.google.com%2F#)

이는 어떻게 해석할 수 있을까??  
  
1\) vscode는 사용자 설정을 json파일에서 읽어들인다.  
2\) setting.json 파일은 vscode의 설정에 대한 데이터를 가지고 있는 포멧이다.  
3\) Theme의 value를 "Red"로 변경하게 되면  
     1. vscode는 setting.json에서 설정 관련 data를 읽어들인다.  
     2. theme가 "Red" 이다.  
     3. 테마의 색을 Red로 변경한다.  
  
4\) 눈이 아파서 Abyss로 다시 변경한다.  
[![](https://mblogthumb-phinf.pstatic.net/MjAxODA1MTdfMjkw/MDAxNTI2NDkyMjE3NDQx.bYX6ZqCS5cQuFMuyWtyeJunW-yc2bYr64X9mFsbTWf4g.mpD-bLQyBIu8Zakvp0a0B1vaxiNglQJs-RKRIIVwzj0g.PNG.demonic3540/image.png?type=w800)](https://m.blog.naver.com/PostView.nhn?blogId=demonic3540&logNo=221277604043&proxyReferer=https:%2F%2Fwww.google.com%2F#)  
  
출처 : 

