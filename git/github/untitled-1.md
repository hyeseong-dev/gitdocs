---
description: 'clone, log --reverse, checkout commit ID'
---

# git remote reposi

###  git의 소스코드를 지역저장소로 가져오기

방법1\) 현재 디렉토리에 저장소이름을 폴더이름을 갖고 안에 내용물\(파일,폴더\)을 담아서 클론하여 설치하기. 

git clone https://github.com/git/git.git   
  
방법2\) 현재 디렉토리에 gitsrc 디렉토리명을 저장소 디렉토리명으로 지정하여서 클론하기. 

git clone https://github.com/git/git.git gitsrc

### 로그를 거꾸로 출력하기

git log --reverse

### git의 첫번째 커밋으로 체크아웃하기

git checkout e83c5163316f89bfbde7d9ab23ca2e25604af290

