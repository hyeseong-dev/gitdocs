# 리눅스 기본 명령어

## 기본 명령어 

#### man 명령어를 이용하면 자세한 내용을 확인 할 수 있어요. 

### 1. ls 

```text
ls                         # 현재 디렉토리의 파일 목록을 보여줌
ls /etc/systemd            # /etc/systemd 디렉토리의 목록을 보여줌
ls -a                    # 현재 디렉토리의 숨김 목록 파일까까지 포함해서 보여줌
ls -l                     # 현재 디렉토리의 목록을 자세히 보여줌 
ls *.conf                 # 확장자가 conf인 목록을 보여줌
ls -l /etc/systemd/b*    # /etc/systemd 디렉토리에 있는 목록중 앞 글자가 b인것을 보여줌
```

> 참고로 리눅스에서는 디렉토리 역시 파일의 범주에 포함되요.

### 2. cd 

Change Directory의 약자로 디렉토리를 이동하는 명령어 

```text
cd # 현재 사용자의 홈 디렉토리로 이동. 만약 현재 사용자가 root면 /root 디렉토리로 이동
cd ~ubuntu # ubuntu 사용자의 홈디렉토리로 이동 
cd .. # 현재 디렉토리의 바로 위 디렉토리로 이동(상대경로)
cd /etc/systemd # (절대경로) 해당 경로로 이동함
cd ../etc/systemd (상대경로) 상위 디렉토리로 이동후 etc/systemd 디렉토리로 이동함 

```

### 3. pwd 

Print Working Directory의 약자로 혀냊 디렉토리의 전체 경로를 화면에 나타냄 

```text
pwd # 현재 작업중인 ㄷㅣ렉토리의 절대 경로 출력
```

### 4. touch 

 크기가 0인 새파일을 생성하거나, 이미 파일이 존재한다면 파일의 최종 수정 시간을 변경함. 

```text
touch abc.txt # 파일이 없으면 aabc.txt를 생성하고 있다면 파일의 수정시간을 변경함 
```

### 5. mkdir

Make Directory의 약자로 새로운 디렉 토리를 생성. 생성된 디렉토리는 명령을 실행한 사용자의 소유가 됨.

```text
mkdir abc # 현재 디렉토리 아래에 abc디렉토리를 생성
mkdir -p /def/fgh 만약 fgh의 부모 디렉토리인 /def 디렉토리가 없으면 자동생성(p : parents)
```

### 6. rmdir 

ReMove Directory의 약자로 디렉토리를 삭제함.   
디렉토리가 비워져있고, 디렉토리에 대한 삭제 권한이 있어야함. \(잘 사용안함\) 

> 'rm -r'을 실행함

```text
rmdir abc # 빈 abc 디렉토리 삭제 
```

### 7. cp 

Copy의 약자로 파일이나 디렉토리를 복사함.   
새로 복사된 파일은 복사한 사용자의 소유감 됨.   
그래서 명령을 실행하는 사용자에게 해당 파일의 읽기 권한이 있어야함. 

```text
cp abc.txt cba.txt # abc.txt파일을 cba.txt로 이름만 바꾸어서 복사함
cp -r abc cba # 디렉토리 복사. 
```

### 8. rm 

remove의 약자로 파일이나 디렉토리를 삭제함 사용자에게 해당 파일이나 디렉토리의 삭제 권한이 있어야함. root사용자\(관리자\)의 경우 모든 권한을 가지고 있기 때문에 이 명령을 사용하는 데 있어 제약이 없음. 

```text
rm abc.txt        # 해당 파일 삭제( 내부적으로 rm -f로 연결)
rm -i abc.txt     # 삭제 시 정말 삭제할 지 확인하는 메시지 출력 
rm -f abc.txt     # 삭제시 확인하지 않고 바로 삭제(f : force) 
rm -r abc         # abc 디렉토리와 그 하위 디렉토리를 강제로 모두 삭제.(r: recursive)
```

### 9. mv 

move의 약자로 파일이나 디렉토리의 이름을 변경하거나 다른 디렉토리로 이동할 때 사용함. 

```text
mv abc.txt /etc/systemd/  # abc.txt를 /etc/systemd/ 디렉토리로 이동
mv aaa bbb ccc ddd        # aaa, bbb, ccc 3개파일을 /ddd 디렉토리로 옮김 
mv abc.txt www.txt        # abc.txt 파일명 --> www.txt 파일 이름으로 변경 
```

### 10. cat 

concatenate의 약자로 파일의 내용을 화면에 띄움.   
명령어 뒤에 여러 개의 파일명을 나열하면 파일을 연결해서 파일의 내용을 화면에 출력함. 

```text
cat a.txt b.txt a텍스트 파일을 먼저 띄우고 다음으로 b텍스트 파일 내용을 보여줌. 
```

### 11. head, tail 

텍스트 형식으로 작성된 파일의 앞 10행 또는 마지막 10행만 화면에 출력함 

```text
head /etc/systemd/bootchart.conf # 파일의 앞 10행만 출력
head -3 /etc/systemd/bootchart.conf # 파일의 앞 3핸만 출력
tail -5 /etc/systemd/bootchart.conf # 파일 내용의 마지막 5행만 출력 
```

### 12. more

텍스트 형식으로 작성된 파일을 페이지 단위로 화면에 출력.  
**Space bar**를 누르면 다음 페이지로 이동하고, **B**를 누르면 이전 페이지로 이동하며, **Q**를 누르면 종료

```text
more /etc/systemd/system.conf
more +10 /etc/systemd/system.conf # 파일의 10행부터 출력함 
```

### 13. less 

more 명령어와 용도가 비슷하지만 더 확장된 기능의 명령어. More 명령어에서 사용하는 키도 사용할 수 있고 추가로 up,down.left, right, pageup, pagedown 도 사용 할 수 있음. 

```text
less /etc/systemd/system.conf
less +10 /etc/systemd/system.conf # 파일의 10행부터 출력함 
```

### 14. file 

어떤 종류의  파일인지 보여줌. 

```text
file /etc/systemd/system.conf # system.conf파일은 텍스트 파일임으로 아스키(ASCII)파일로 표시됨
file /bin/gzip                # gzip은 실행 파일이라서 ELF 64-bit LSB excutable파일로 표시
```

### 15. clear 

 현재 터미널을 깔끔하게 정리해버림

```text
clear 
```

