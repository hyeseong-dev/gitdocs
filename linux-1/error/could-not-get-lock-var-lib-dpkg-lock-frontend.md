# Could not get lock /var/lib/dpkg/lock-frontend

apt 명령어 사용중 아래와 같은 오류가 나타났어요. 

  
E: Could not get lock /var/lib/dpkg/lock-frontend - open \(11: Resource temporarily unavailable\)  
E: Unable to acquire the dpkg frontend lock \(/var/lib/dpkg/lock-frontend\), is another process using it?  
  
구글링 한 결과 방법은 

**첫째 실행중인 apt를 모두 꺼버리는 겁니다**. 

> sudo killall apt apt-get

**둘째 아래 명령어를 모두 실행해서 경로의 디렉토리를 삭제해주세요.** 

> sudo rm /var/lib/apt/lists/lock  
> sudo rm /var/cache/apt/archives/lock  
> sudo rm /var/lib/dpkg/lock\*

전 두 번째 방법에서 해결되었어요. 

출처: [https://www.linuxuprising.com/2018/07/how-to-fix-could-not-get-lock.html](https://www.linuxuprising.com/2018/07/how-to-fix-could-not-get-lock.html)

