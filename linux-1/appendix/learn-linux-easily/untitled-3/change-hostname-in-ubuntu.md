# Change Hostname in ubuntu

## hostname 확인

**명령어로 확인하기**

다음과 같이 명령하면 hostname을 출력합니다.

```text
hostname
```

**설정 파일 열어서 확인하기**

텍스트 에디터로 /etc/hostname 파일을 열면 hostname이 적혀있습니다.

## hostname 변경

**명령어로 변경하기**

다음과 같이 명령하면 hostname이 abc로 바뀝니다.

```text
hostnamectl set-hostname abc
```

**설정 파일 열어서 변경하기**

텍스트 에디터로 /etc/hostname 파일을 열어서 내용을 abc로 바꾸면 hostname이 abc로 바뀝니다.

#### 재부팅

재부팅을 하면 위에서 설정한 사항들이 반영됩니다.

