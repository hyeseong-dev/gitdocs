# 1\_ls\_cd\_pwd

학습 목차

**ls 명령어   
cd 명령어  
pwd 명령어  
ls 명령어**

ls명령어는 가장 많이 리눅스에서 사용되어요. list의 줄임말이라는거 참 직관적이조.

ls 명령어를 통해서 폴더의 포함된 파일들을 볼수 있는것 뿐만 아니라 파일권한\(디렉토리, 폴더 및 파일권한\)등 여러 정보등도 볼 수 있어요.

\(1\) 명령 형식

> ls \[option\]

\(2\) 옵션값인 Parameters

| Parameter | 내용 |
| :--- | :--- |
| -a | -all list 숨겨진 모든 파일들까지 구석구석 해당 디렉토리의 내용들을 보여줘요. |
| -l | 파일이름 뿐만 아니라. 소유주, 파일사이즈 등 자세히 나와요 |
| -d | -directory 디렉토리만 보여줘요 |
| -h | –human-readable List file sizes in an easy-to-understand format \(eg 1K 234M 2G\) |
| -t | –human-readable List file sizes in an easy-to-understand format \(eg 1K 234M 2G\) |

\(3\)  
예1: / home 폴더에있는 모든 파일 및 디렉토리의 세부 사항을 출력해볼게요.

> ls -a -l /home  
> ls -al /home

테스트 결과를보다 쉽게 ​​볼 수 있도록 먼저 테스트 파일을 만듭니다.  
여기서는 cd 및 touch 명령을 사용합니다.

> cd /home  
> sudo touch labex.txt  
> ![](https://labex.io/upload/T/E/K/Rk1kvFP4ITAw.png)

![](https://labex.io/upload/S/D/N/L7aY20UTiKUD.png)

위의 빨간색 박스에서, **d**는 디렉토리이고, **-** 파일입니다.  
디렉토리와 파일의 색깔이 다르니, 잘 확인해주세요.

예2: 현재 디렉토리에서 'd'로 시작하는 모든 파일을 해당 디렉토리에서 보여줘요.

> ls -l d\*

실습을 위해 2개의 텍스트 파일을 만들어 볼게요. touch 명령어는 여기서 사용해요.

> sudo touch data.txt sudo touch date.txt

![](https://labex.io/upload/U/S/R/3VBtEbGpyc3f.png)

예3: /home 디렉토리에 있는 모든 파일들의 크기를 출력해줘요.

> ls -alh /home  
> ![](https://labex.io/upload/U/I/X/kuXClZ2sh8m1.png)

예4. 1. /

