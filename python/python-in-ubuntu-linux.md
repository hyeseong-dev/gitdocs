# Python 버전 변경 in Ubuntu Linux



우분투\(Ubuntu\)를 설치하면 python path가 2.7로 설정되어 있습니다. 리눅스의 `Alternatives`를 이용하면 python 버전을 쉽게 변경하고 관리할 수 있습니다.

Alternatives는 기본 커맨드의 심볼릭 링크를 관리해주는 리눅스 프로그램입니다. 데비안 계열의 리눅스\(우분투\)에서는 `update-alternatives`가 제공됩니다.

update-alternatives에 대한 자세한 설명과 명령어는 [manpages](http://manpages.ubuntu.com/manpages/trusty/man8/update-alternatives.8.html)를 참고해주세요.

### 파이썬의 실행 위치 및 Alternative 설명

`which python` 명령어를 사용하면 현재 사용하는 파이썬이 어디에 설치되어있는지 알 수 있습니다. 파일 이름을 보면 실제 위치가 아니라, 심볼릭 링크이고 파이썬이 실제 설치된 위치를 가리킬 것 같습니다.

```text
$ python -V
Python 2.7.14

$ which python
/usr/bin/python
```

`ls -al /usr/bin/python`로 어떤 파일을 가리키는지 확인할 수 있습니다. 이 파일이 가리키는 파일은 `/usr/bin/python2.7`입니다.

```text
$ ls -al /usr/bin/python
lrwxrwxrwx 1 root root 24  4월 18 19:28 /usr/bin/python -> /usr/bin/python2.7
```

그리고 `ls /usr/bin/`를 보면 다양한 버전의 파이썬 실행파일들이 있습니다.

```text
$ ls /usr/bin/ | grep python
python
python2
python2.7
python3
python3.6
.....
```

아시겠지만 PC에는 여러버전의 파이썬이 설치되어있고 Alternative로 주로 사용할 파이썬을 선택하는 방식으로 관리를 하고 있습니다.

update-alternatives는 다음과 같은 기능을 하여 버전 관리를 쉽게할 수 있습니다.

* 현재 /usr/bin/python =&gt; /usr/bin/python2.7 를 가리키고 있습니다.
* 파이썬3.6로 변경하려면 /usr/bin/python =&gt; /usr/bin/python3.6 를 가리키도록 변경해야 합니다.
* 파이썬3.7로 변경하려면 /usr/bin/python =&gt; /usr/bin/python3.7 를 가리키도록 변경해야 합니다.

update-alternatives에 여러버전의 파이썬을 등록하고 변경하는 것을 해보겠습니다.

### Update-alternatives로 파이썬 버전 등록 및 변경

먼저 파이썬을 등록하기 전에 이미 등록된 것이 있는지 확인해야 합니다.

`update-alternatives --config python` 옵션은 python 버전을 변경하는 옵션입니다. 만약 아래 error 로그처럼 설정된 것이 없다고 한다면 아무것도 등록된 것이 없다는 의미입니다.

```text
$ sudo update-alternatives --config python
update-alternatives: error: no alternatives for python
```

`update-alternatives --install [symbolic link path] python [real path] number` 명령어는 실행파일을 등록하는 명령어입니다.

아래와 같이 입력하면 2.7과 3.6버전이 update-alternatives에 등록됩니다. 물론 파이썬 2.7과 3.6이 설치되어 있어야 합니다. 만약 설치위치가 저와 다르다면 자신의 PC에 설치된 path로 변경하셔야 합니다.

```text
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python2.7 1
$ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.6 2
```

그리고 `update-alternatives --config python`을 다시 입력하면 등록한 파이썬 버전을 선택하는 메뉴가 나옵니다.

```text
$ sudo update-alternatives --config python
There are 2 choices for the alternative python (providing /usr/bin/python).

  Selection    Path                Priority   Status
------------------------------------------------------------
* 0            /usr/bin/python3.6   2         auto mode
  1            /usr/bin/python2.7   1         manual mode
  2            /usr/bin/python3.6   2         manual mode

Press <enter> to keep the current choice[*], or type selection number: 2
```

원하는 메뉴의 번호를 입력하고 파이썬 버전을 확인해 보세요. 파이썬의 link를 따라가보면 alternatives 명령어로 설정한 `/usr/bin/python3.6`를 가리킵니다.

```text
$ python --version
Python 3.6.3

$ ls -al /usr/bin/python
lrwxrwxrwx 1 root root 24  4월 18 19:28 /usr/bin/python -> /etc/alternatives/python

$ ls -al /etc/alternatives/python
lrwxrwxrwx 1 root root 18  9월  2 13:59 /etc/alternatives/python -> /usr/bin/python3.6
```

### 정리

Alternatives는 파이썬뿐만 아니라 Java 등의 모든 프로그램의 버전을 관리하는데 사용할 수 있습니다. 여기서는 파이썬을 예로 들었습니다.

### 참고

* update-alternatives에 대한 자세한 설명은 [Ubuntu manpage](http://manpages.ubuntu.com/manpages/trusty/man8/update-alternatives.8.html)를 참고해주세요.
* 우분투에 파이썬3.7을 설치하는 방법은 [Python3.7 설치\(Ubuntu18.04\)](https://codechacha.com/ko/install-python37-in-ubuntu1804/)를 참고해주세요.

