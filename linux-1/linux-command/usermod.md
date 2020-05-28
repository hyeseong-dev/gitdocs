---
description: 사용자계정 속성 변경
---

# usermod

usermod 옵션 계정명

| **옵션**  | **설명**  |
| :--- | :--- |
| -u | 사용자 계정의 UID 생성  |
| -g  | 사용자 계정의 1차 그룹의 GID 지정  |
| -G  | 사용자 계정의 2차 그룹의 GID 지정  |
| -c  | Comment  |
| -d  | 사용자의 홈디렉토리를 지정  |
| -e  | 사용자의 계정 만기일 지정  |
| -f  | 사용자의 계정 유효일 지정  |
| -s  | 로그인 시 사용할 기본 쉘 지정 |

\# cat /etc/passwd \| grep tester  :  tester1 ,tester2 계정 확인

\# usermod -u 700 tester1  :  tester1 계정의 UID 값을 700 변경

\# uesrmod -u 701 tester2  :  tester2 계정의 UID 값을 701 변경

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 계정의 변경된 UID 값 확인

\# cd /home/  :  홈디렉토리로 이동

\# ls -n  :  tester1, tester2 계정의 홈디렉토리로 변경된 UID 값 확인

![](https://postfiles.pstatic.net/20151112_256/kdi0373_1447318475966NOwxr_PNG/31.png?type=w2)

**예제 2\)  옵션 \[ -g \]**

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 계정 확인

\# usermod -g 801 tester1  :  tester1에 GID 값을 801로 변경 \(801 그룹이 없어서 실패\)

\# groupadd -g 801 test\_group1  :  GID 801를 갖는 test\_group1 그룹 생성

\# groupadd -g 802 test\_group2  :  GID 802를 갖는 test\_group2 그룹 생성

\# cat /etc/group \| grep test  :  생성된 그룹 확인

\# usermod -g 801 tester1  :  tester1에 GID 값을 801 변경

\# usermod -g 802 tester2  :  tester2에 GID 값을 802 변경

\# cat /etc/passwd \| grep tester  :  tester1 , tester2의 변경된 GID 값을 확인 \( 변경됨 \)

\# cat /etc/group \| grep test  :  test\_group1, test\_group2에 포함되었는지 확인 \( 변경안됨 \)

\# cd /home/  :  홈디렉토리로 이동

\# ls -n  :  tester1 , tester2의 홈디렉토리 GID 확인 \( 변경안됨 \)

![](https://postfiles.pstatic.net/20151113_70/kdi0373_1447384800579j9M8w_PNG/01.png?type=w2)  
![](https://postfiles.pstatic.net/20151113_42/kdi0373_1447384800834Qu8IU_PNG/02.png?type=w2) 

**예제 3\)  옵션 \[ -G \]**

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 계정 정보 확인

\# groupadd -g 700 test\_group  :  GID 700을 갖는 그룹 test\_group 생성

\# usermod -G 700 tester1  :  test\_group이라는 그룹에  tester1 계정 추가

\# usermod -G 700 tester2  :  test\_group이라는 그룹에 tester2 계정 추가 

\# cat /etc/passwd \| grep tester  :  tester1 , tester2의 계정 정보 확인 \( GID 값 변경 안됨\)

\# cat /etc/group \| grep test  :  test\_group이라는 그룹에 tester1, tester2 계정이 추가 되었는지 확인

\# cd /home/  :  홈디렉토리로 이동

\# ls -n  :  tester1 , tester2의 홈디렉토리 확인 \(GID 값 변경 안됨\) 

![](https://postfiles.pstatic.net/20151113_125/kdi0373_1447391326826TUd96_PNG/03.png?type=w2)

**예제 4\)  옵션 \[ -c \]**

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 계정 정보 확인

\# usermod -c '감시 대상1' tester1  :  tester1의 Commnet를 변경

\# usermod -c '감시 대상2' tester2  :  tester2의 Comment를 변경

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 의 변경된 Comment 확인

![](https://postfiles.pstatic.net/20151113_288/kdi0373_1447392154049yHCQv_PNG/04.png?type=w2)

**예제 5\)  옵션 \[ -d \]**

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 계정 정보 확인

\# usermod -d /home/tester1\_dir tester1  :  tester1의 홈디렉토리를 변경

\# usermod -d /home/tester2\_dir tester2  :  tester2의 홈디렉토리를 변경

\# cat /etc/passwd \| grep tester  :  tester1 , tester2의 변경된 홈디렉토리 확인

\# cd /home/   :  홈디렉토리로 이동

\# ls -n  :  홈디렉토리 확인 결과 계정 정보만 변경 되었지 추가된 디렉토리는 없다.

![](https://postfiles.pstatic.net/20151113_266/kdi0373_1447392805058eHcch_PNG/05.png?type=w2)

**예제 6\)  옵션 \[ -e \]**

\# cat /etc/passwd \| grep tester  :  tester1 , tester2의 계정 정보 확인

\# cat /etc/shadow \| grep tester  :  tester1 , tester2의 만기일 정보 확인

\# date  :  오늘의 날짜 정보 확인

\# usermod -e 2015-11-20 tester1  :  tester1라는 계정에 만기일 변경

\# usermod -e 2015-11-25 tester2  :  tester2라는 계정에 만기일 변경

\# cat /etc/shadow \| grep tester  :  tester1 , tester2 계정의 변경된 만기일 정보 확인

※ 만기일은 1970년 1월 1일을 기준으로 설정 날짜까지의 일수를 말한다. \(단위 : 일\)

![](https://postfiles.pstatic.net/20151113_76/kdi0373_14473935251297K3F5_PNG/06.png?type=w2)

**예제 7\) 옵션 \[ -f \]**

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 계정의 정보를 확인

\# cat /etc/shadow \| grep tester  :  tester1 , tester2 계정의 유효일 확인

\# date :  오늘의 날짜 확인

\# usermod -f 3 tester1  :  tester1의 계정 유효일은 3일로 설정

\# usermod -f 5 tester2  :  tester2의 계정 유효일은 5일로 설정

\# cat /etc/shadow \| grep tester  :  tester1 , tester2의 변경된 계정의 유효일 확인

![](https://postfiles.pstatic.net/20151113_180/kdi0373_1447394260173LGpWh_PNG/07.png?type=w2)

**예제 8\)  옵션 \[ -s \]**

\# cat /etc/passwd \| grep tester  :  tester1 , tester2의 계정 정보 확인 \( 변경 전 계정의 쉘 정보 확인\)

\# cat -n /etc/shells  :  시스템에서 사용할 수 있는 쉘 정류 확인

\# usermod -s /bin/sh tester1  :  tester1의 쉘를 /bin/sh로 설정

\# usermod -s /bin/csh tester2  :  tester2의 쉘를 /bin/csh로 설정

\# cat /etc/passwd \| grep tester  :  tester1 , tester2 의 변경된 쉘 정보  


  
출처: [https://jang8584.tistory.com/243](https://jang8584.tistory.com/243) \[개발자의 길\]  
  


