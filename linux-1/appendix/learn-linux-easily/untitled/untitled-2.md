# Additional samba explanation

### 삼바\(SAMBA\)란 무엇인가?

만약 우리 회사가 서버는 리눅스로 구성되어 있는데, 회사에서 회사원들에게 일 열심히 하라고 윈도우 기반 노트북을 줬다고 가정합시다. 그런데 리눅스 서버에 올려놓은 파일을 윈도우에서 사용하고 싶어요. \(리눅스가 삼바서버, 윈도우가 클라이언트\) 또는 내가 윈도우 컴퓨터에서 작업한걸 리눅스에서 사용하고 싶을 수 있죠. 

![](https://blog.kakaocdn.net/dn/G1tHK/btqDUSq5BuE/jYPEkKCQxlCsQ5DGFF6vE1/img.png)사진 출처: https://www.samba.org/cifs/docs/what-is-smb.html

이렇게 윈도 시스템이 다른 시스템의 디스크나 프린터 등의 자원을 공유가능하게끔 만든 프로토콜이 SMB입니다. 삼바는 일종의 공유 폴더라고 생각하시면 돼요.

삼바가 편리하긴 하지만 보안이 중요한 회사에서는 잘 사용하지 않습니다. 금융업계같은 경우, 공유폴더를 사용하지 않도록 법이 지정되어 있거든요. 저희 회사같은 경우도 SAMBA를 사용하지는 않아요.ㅎㅎ 필요할 경우 sftp를 이용해서 파일 전송합니다.ㅎㅎ 

삼바를 이용해서 리눅스와 윈도는 디렉터리 및 파일 공유, 프린터, CD-ROM, DVD-ROM, USB 공유가 가능합니다.

현재 SMB 프로토콜은 유닉스와 윈도 환경을 동시에 지원하는 CIFS\(Common Internet File System\)로 확장되었습니다. 

무튼, 삼바가 뭔지 대강 알았으면 삼바를 설치하러 가볼까요? 먼저 리눅스에 삼바를 설치해볼게요 이럴 경우 리눅스가 서버, 윈도우가 클라이언트가 됩니다. 물론 반대로 할 수도 있어요 ㅎㅎ 

### 리눅스에 삼바\(SAMBA\)서버 설치하기

삼바는 설치 명령어로 간단하게 설치할 수 있습니다.

```text
apt-get install -y samba //우분투일 경우
yum install -y samba //centOS일 경우
```

자신의 리눅스 운영체제에 맞게 설치해줍시다. 관리자가 아니라면 당연히 앞에 sudo 명령어 붙여야 하는것 알죠? 이러면 삼바서버 만드는거 끝이예요 ㅎㅎ

![](https://blog.kakaocdn.net/dn/kVKUP/btqDVWl2dXT/xUr7aafkVKKDCWa836F4j1/img.png)

요런 구조가 되겠죠~

### 삼바 사용하기

**▶1. 삼바 계정 추가하기 - smbpasswd 명령어** 

삼바 계정을 먼저 추가해줍시다. 삼바 계정은 smbpasswd 명령어로 추가할 수 있어요.

```text
smbpasswd -a ubuntu
```

ubuntu 계정을 추가해줬어요. 추가하려는 계정은 시스템에 존재하는 계정이여야 합니다. 리눅스 서버에 ubuntu라는 사용자가 없는데 삼바 사용자로 등록할 수는 없어요.

![](https://blog.kakaocdn.net/dn/PlUkr/btqDUSxPo3x/XWX3qIxx5kzcBLeJCeppF0/img.png)

이렇게 존재하지 않는 사용자를 등록했을 경우 'Failed to add entry for user ooo' 가 뜨면서 실패합니다. 이 외에도 sambpasswd 명령어로 사용자를 제거하거나 비활성화 할 수도 있어요. smbpasswd 명령어에 대해 좀더 알아봅시다!

**□ smbpasswd 명령어란?**

삼바 사용자를 생성 및 삭제, 패스워드 변경, 활성 및 비활성화 등 관련 정보를 변경하는 명령어입니다. 그 리눅스 명령어중에 passwd 명령어 있잖아요. 옵션 없이 쓰면 얘와 기능이 똑같습니다. 삼바 유저 비밀번호를 변경하는 역할을 해요.

참고\) passwd 명령어 - [https://jhnyang.tistory.com/260](https://jhnyang.tistory.com/260)[ \[리눅스/Linux\] 패스워드 관리 - 비밀번호 변경, 유효기간 지정 , 만료날짜 passwd, chage 명령어를 알아보자!\[리눅스/유닉스 LINUX/UNIX 목차\] 안녕하세요~! 오늘은 패스워드 관련된 명령어와 파일에 대해 알아보도록 합시다. 대게 보안적인 이슈로 사용자마다 3개월마다 패스워드 변경하기 이런 조건이 있잖아요. 저도 3개..jhnyang.tistory.com](https://jhnyang.tistory.com/260)

**□ smbpasswd 명령어 주요 옵션\(OPTIONS\)**

![](https://blog.kakaocdn.net/dn/xZGFn/btqDUTjeuDr/rF9mfkQQcDKMcYGb8k6Vt1/img.png)우분투 man smbpasswd 화면

| 옵션  | 설명 |
| :--- | :--- |
| -a | 삼바 사용자를 추가할 때 사용합니다. 삼바 사용자는 리눅스 시스템에 존재하는 계정이어야 합니다. |
| -x | 삼바 사용자를 제거할 때 사용합니다. |
| -d | 삼바 사용자를 일시적으로 비활성화할 때 사용합니다. |
| -e | 삼바 사용자를 활성화할 때 사용합니다. |
| -n | 패스워드 없이 로그인이 가능하도록 할 때 사용합니다. smb.conf에 'null passwords = yes'라고 추가로 설정해야 합니다. |

**□ smbpasswd 명령어 사용 예시**

**\# smbpasswd -a jhnyang**

→ jhnyang를 삼바 사용자에 추가하면서 패스워드를 부여합니다. jhyang는 생성된 계정이어야 함.

**\# smbpasswd jhnyang**

→ jhnyang 삼바 패스워드를 변경합니다.

**\# smbpasswd -x jhnyang**

→ jhnyang 삼바 사용자를 제거합니다.

**\# smbpasswd -d jhnyang**

→ jhnyang 삼바 사용자를 비활성화 시킵니다.

**▶2 공유할 디렉터리 만들기**

윈도우에서 접근할 수 있는 즉 삼바로 공유될 디렉터리를 하나 생성해줍시다.

smbdir로 만들었어요. 그리고 안에 smbtest 파일을 하나 만들어줬습니다. 파일에는 HELLO SAMBA를 써줬어요.

![](https://blog.kakaocdn.net/dn/cCxw8c/btqDUSLrhlF/gafYDWa1lAdzfENLGh48x0/img.png)

**▶3 삼바 설정 파일 확인 및 수정 \(사용자별 공유자원 할당\)**

이제 어떤 폴더를 공유하고 싶은지, 사용자를 일일이 추가해서 접근 공간을 다르게 해줄건지, 아님 특정 IP대역을 다 허용할건지,, 이렇게 접근한 자들이 파일을 읽을수만 있게할건지 맘대로 수정까지 가능하게 할거니..등등 설정을 지정해줘야 합니다!

설정할 수 있는게 어떤어떤게 있는지는 좀이따 자세히 분석하도록 하고,

간단하게 2번에서 만들어줬던 디렉터리와 파일을, ubuntu와 jhyang 사용자가 윈도우에서 접근할 수 있도록 설정해볼게요.

**삼바 환경 설정 파일 위치**

/etc/samba/smb.conf 

![](https://blog.kakaocdn.net/dn/RnuWY/btqDUTcrFPr/GKV4fIGKVmKhfTU20rgb80/img.png)

요기 가면 있습니다. 열어주세요.

![](https://blog.kakaocdn.net/dn/cCWRrN/btqDURTlM16/o3k2vDlSTyLL2h8jgW0L71/img.png)

맨 밑으로 가면 요렇게 있습니다.\(shfit + g\)누르면 맨 밑으로 이동해요. 

![](https://blog.kakaocdn.net/dn/cvOxiJ/btqDWsdW58c/od6bFVduhKEKbxZPavdnek/img.png)

요렇게 추가해줍시다. 각각 무엇을 의미하는지 간략히 알아볼게요.

**- \[smbdir\]**

빨간색 네모박스 맨 첫번째 \[smbdir\]에서 대괄호는 섹션을 정의하는 역할을 해요. 윈도우에서 접근할 때 폴더 이름이 세션안의 문자열로 보입니다. 즉 윈도우에서 보여지는 폴더 이름과 리눅스 실제 디렉터리 이름은 다를 수 있어요.

**- comment**

간단한 설명을 설정합니다

**- path** 

공유 디렉터리의 경로를 여기다 적어줘요. \(저는 아까 이 디렉터리를 root디렉터리\('/'\) 밑에 만들어줬거든요 ㅎㅎ

**- read only**

윈도우에서 이 공유폴더 또는 그 안 데이터들을 읽을 수만 있고 함부로 수정이나 삭제하는 것을 막습니다.

**- valid users** 

공유 디렉터리를 이용할 수 있는 사용자를 지정해요.

**▶4 삼바 데몬 프로세스 재시작** 

설정파일을 수정하고 변경 내용이 적용되려면 삼바 데몬 프로세스를 재시작해줘야 해요. 

```text
# service smbd restart
또는
# /etc/rc.d/init.d/smbd restart
```

삼바서버는 2개의 데몬을 사용하는데 smbd가 그 중 하나입니다. smbd는 파일과 프린터 공유, 사용자의 권한 부여 및 확인 등 사용자 인증을 당답하는 데몬이예요. 이를 재시작해줍시다. 

![](https://blog.kakaocdn.net/dn/bxKEwk/btqDWUgVJ9N/fupbKz8ia8viyQgfsK9pa1/img.png)

**▶5 리눅스 서버 IP정보 알기**

'hostname -I'명령어를 치면 간단하게 자신의 IP주소를 알 수 있어요.

![](https://blog.kakaocdn.net/dn/b9cNGR/btqDVdIxpyq/TwwvsBpDph9KvsqcOdkhk1/img.png)

**▶6 윈도우에서 접근 되는지 확인**

이제 윈도우에서 접근해봅시다. 먼저 Ctrl+R을 눌러서 실행창을 켜줍시다.

![](https://blog.kakaocdn.net/dn/MUbtq/btqDURsdoZg/f6UNOkilqpKogN6r1iWZI0/img.png)

그리고 '역슬래시+리눅스서버IP주소'를 입력해주세요. 

![](https://blog.kakaocdn.net/dn/lb34k/btqDVwnDmJK/K3J52h5KOgTfGAucaqfig0/img.png)

그럼 이렇게 '네트워크 자격 증명 입력'창이 뜹니다. 아까 ubuntu와 jhyang 접근을 허용해줬었어요. ubuntu 계정으로 들어가볼게요. 

![](https://blog.kakaocdn.net/dn/bqEdz3/btqDVffiOph/3ppzXe0VY6RnhMchxoEIK0/img.png)

짠! 로그인에 성공하면 우리가 공유하기로 설정했던 smbdir 디렉터리가 뜹니다.

![](https://blog.kakaocdn.net/dn/bqa5si/btqDVdu5NAp/BBpM0uxKGoTK0zqXnXo61k/img.png)

폴더에 들어가면 실제 우리가 작성했던 smbtest 파일도 확인할 수 있어요.

이 파일을 메모장으로 연 다음 수정후 저장을 눌러봅시다. 또는 삭제를 시도해봅시다.

![](https://blog.kakaocdn.net/dn/kXR4P/btqDYvU2Yj7/kXfKP6QC39Z4YzGfSST0x0/img.png)![](https://blog.kakaocdn.net/dn/QNIlE/btqDVeHue8G/kpyI7e2KTNTkG9UbuUjftK/img.png)저장을 시도했을 때\(왼\) 삭제를 시도했을 때\(오\)

고럼 이렇게 저장할 권한이 없다고 떠요. 이유는 우리가 앞에서 read only 옵션을 yes로 설정해줬기 때문이예요.

혹시 수정을 가능케 하고 싶다면 read only 옵션 대신에  'writable = yes' 를 추가해주면 된답니다! 

jhyang 사용자로도 접근 가능한지 확인해보려면, 삼바 사용자에 추가해준 후, 동일하게 들어가보면 돼요! ㅎㅎ

### \[share\] 섹션 설정시 사용가능한 주요 옵션들

위에서 설정한 옵션들 외에도 어떤 설정을 할 수 있을까 궁금하신 분들이 있을거예요.

| 옵션 | 설명 |
| :--- | :--- |
| comment | 간단한 설명을 설정합니다. |
| path | 공유 디렉터리의 경로를 설정합니다. |
| read only | 공유 디렉터리를 읽기 전용으로 설정합니다. |
| writable, wirte ok | 공유 디렉터리를 쓰기 가능하게 설정합니다. |
| valid users | 공유 디렉터리를 이용할 수 있는 사용자를 지정합니다. |
| write list | 공유 디렉터리에 접근 및 쓰기 권한을 행사할 수 있는 사용자를 지정합니다. 그룹인 경우에는 @를 붙입니다. |
| public, guest ok | 다른 사용자들이 이용할 수 있도록 설정할 때 사용합니다. |
| browseable, browsable | 공유 디렉터리의 리스트를 보여줄 때 설정합니다. |
| printable | 공유 디렉터리에 스풀 파일을 지정할 때 사용합니다. |
| create mask, create mode | 파일을 생성할 때 허가권을 지정할 때 설정합니다. |

### 기출문제

**\[리눅스마스터 1급 1차 필기 1902회\]**

삼바 서버의 환경 설정 파일에서 ihduser와 kaituser만 접근할 수 있도록 설정하려고 한다. 다음 \(괄호\)안에 들어갈 내용으로 알맞은 것은?

----------------------------------------------------

\[www\]

comment = share

path = /web

\(괄호\) = ihduser kaituser

writable = yes

----------------------------------------------------

① users ② smbusers ③ valid users ④ public users

답: 3번

**\[리눅스마스터 1급 1차 필기 1901회\]**

삼바 서버의 설정이 다음과 같은 경우에 윈도우에서 접근할 때 나타나는 폴더명으로 알맞은 것은?

----------------------------------------------------

\[www\]

comment = share

path = /web

public = yes

write list = @insa

----------------------------------------------------

① www ② share ③ web ④ insa

답: 1번

