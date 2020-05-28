# conda 명령어



### I. \[패키지 처리\]

1. 해당 가상환경의 설치된 패키지 버전 목록 확인 

   > pip freeze  
   > pip3 freeze

명령어는 다르지만 둘다 잘 작동하네요.

> conda freeze

1. 한개의 패키지 버전 정보\(버전,섬머리, 홈페이지,작가, 이메일, 라이센스,설치위치,요구사항\)

   > pip show 패키지명  
   > pip3 show 패키지명

2. 패키지 삭제 방법

   > conda remove 패키지명 \(단, 가상환경에 진입해 있을 때!\)  
   > conda remove -n env pygame \(가상환경에 진입해 있지 않을 때\)

3.1. pip로 지울때는 아래와 같은 명령어를 사용하세요.

> pip uninstall 패키지명

1. 가상환경 생성과 동시에 패키지 설치 

> conda create -n 가상환경이름 python=버전 패키지이름 conda create -n pyqt\_env python=3.7 pyqt5

### II. \[가상 환경\]

1. 가상환경 생성

   > conda create -n 가상환경명

2. 패키지 설치

   > conda install --name 패키지명

3. 가상환경 삭제

   > conda remove --name 가상환경명 --all

[leebaro.tistory.com](https://leebaro.tistory.com/entry/anaconda%EC%97%90%EC%84%9C-%EA%B0%80%EC%83%81%ED%99%98%EA%B2%BD-%EC%82%AD%EC%A0%9C%ED%95%98%EA%B8%B0) 해당 내용 출처

1. 최신번저 업데이트 

   > conda update --name="base" --channel="defaults" conda conda update -n base -c defaults conda

에러 사항 해결법 아래는 pygame 패키지로 적용되었습니다. 본인이 원하는 패키지명을 넣어서 실행해보세요.

첫째

> conda install anaconda-client

둘째

> anaconda search -t conda pygame
>
> * 웹사이트의 패키지몇, 버전, 유형, 플랫폼들이 열거되어 나타남

셋째

> conda install --channel [http://conda.anaconda.org/CogSci](http://conda.anaconda.org/CogSci) pygame

