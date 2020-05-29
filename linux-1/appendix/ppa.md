# PPA

## PPA 

PPA는 Personal Package Archives \(개인 패키지 보관소\)의 약자 입니다. 개인이나 단체 또는 기업에서 패키지를 보관 하는 장소가 됩니다.

우분투에서 제공하는 것 들이 아니기 때문에 버전이 다르거나 cpu 에 따라 오동작을 일으킬 소지가 있다고 합니다. 그래서 이런 패키지보관소가 신뢰 할 수 있는 곳의 ppa 를 등록해서 사용 하는 것이 좋습니다.

PPA를 통한 프로그램 설치 방법 터미널 창에 아래와 같이 명령을 입력해 실행 합니다.

\# sudo add-apt-repository ppa:저장소명 

\# sudo apt-get update 

\# sudo apt-get install 패키지명

add-apt-repository ppa:저장소명 --&gt; 저장소를 하나르 추가하는 명령 apt-get update --&gt; 저장소의 내용을 업데이트   
apt-get install 패키지명 --&gt; 패키지 설치

삭제 방법 PPA 를 이용해서 프로그램을 설치하면 지우기 위해서 ppa-purge 를 사용 해야 합니다. 먼저 ppa-purge 를 설치 합니다.

\# sudo apt-get install ppa-purge

이제 이를 이용해 설치했던 패키지를 삭제 하면 되겠습니다.

삭제 하는 명령 \# sudo ppa-purge ppa:저장소명

