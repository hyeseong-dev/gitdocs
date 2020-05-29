# Find 명령어

## find 명령어란?

 파일을 검색 할 뿐만 아니라, 파일 크기, 소유자 권한등을 이용해서 검색할 수 도있어요. 그리고 exec 등의 옵션과 다른 명령어를 함께 사용하면 소스코드 분석에도 사용되기도해요. 

---

##  find 명령어 구조 

> Usage: find \[-H\] \[-L\] \[-P\] \[-Olevel\] \[-D debugopts\] \[path...\] \[expression\]

주로 path + expression 형태를 많이 사용해요.   
  
expression 형태는 operator, option, action 등이 있어요.   
아래의 예제를 봐주세요.   


```text
$ find --help 

Usage: find [-H] [-L] [-P] [-Olevel] [-D debugopts] [path...] [expression]

default path is the current directory; default expression is -print
expression may consist of: operators, options, tests, and actions:
operators (decreasing precedence; -and is implicit where no others are given):
      ( EXPR )   ! EXPR   -not EXPR   EXPR1 -a EXPR2   EXPR1 -and EXPR2
      EXPR1 -o EXPR2   EXPR1 -or EXPR2   EXPR1 , EXPR2
positional options (always true): -daystart -follow -regextype

normal options (always true, specified before other expressions):
      -depth --help -maxdepth LEVELS -mindepth LEVELS -mount -noleaf
      --version -xdev -ignore_readdir_race -noignore_readdir_race
tests (N can be +N or -N or N): -amin N -anewer FILE -atime N -cmin N
      -cnewer FILE -ctime N -empty -false -fstype TYPE -gid N -group NAME
      -ilname PATTERN -iname PATTERN -inum N -iwholename PATTERN -iregex PATTERN
      -links N -lname PATTERN -mmin N -mtime N -name PATTERN -newer FILE
      -nouser -nogroup -path PATTERN -perm [-/]MODE -regex PATTERN
      -readable -writable -executable
      -wholename PATTERN -size N[bcwkMG] -true -type [bcdpflsD] -uid N
      -used N -user NAME -xtype [bcdpfls]      -context CONTEXT

actions: -delete -print0 -printf FORMAT -fprintf FILE FORMAT -print
      -fprint0 FILE -fprint FILE -ls -fls FILE -prune -quit
      -exec COMMAND ; -exec COMMAND {} + -ok COMMAND ;
      -execdir COMMAND ; -execdir COMMAND {} + -okdir COMMAND ;

Valid arguments for -D:
exec, help, opt, rates, search, stat, time, tree
Use '-D help' for a description of the options, or see find(1)

Please see also the documentation at http://www.gnu.org/software/findutils/.
You can report (and track progress on fixing) bugs in the "find"
program via the GNU findutils bug-reporting page at
https://savannah.gnu.org/bugs/?group=findutils or, if
you have no web access, by sending email to <bug-findutils@gnu.org>.
```

 find 명령어가 뭔지 --help를 뒤에 입력했더니 상당한 양의 친절한 영문 mannual이 나타난걸 확인 할수 있어요. 



##  실습 

> find   
> find .  
> find . -ls

```text
root@ip-172-31-35-20:~/example# find
.
./Dockerfile
root@ip-172-31-35-20:~/example# find .
.
./Dockerfile
root@ip-172-31-35-20:~/example# find . -ls
   294846      4 drwxr-xr-x   2 root     root         4096 May 28 23:49 .
   256582      4 -rw-r--r--   1 root     root          170 May 28 23:37 ./Dockerfile
```

첫 번째 명령어에 옵션없이 입력하고 실행할 경우 디렉토리와 파일의 목록을 출력해요.   
즉 find 명령어 바로 뒤에 경로를 지정하면 해당 경로의 파일과 디렉토리 내용을 출력해서 보여주죠.   


###  파일 검색 

 파일명을 검색 할 때에는 -name 옵션을 추가하여 검색하면 되요. 아래의 명령어는 /etc 위치에서 host.conf 파일을 검색하는 명령어에요. 

```text
find /etc -name 'host.conf' # 혹 안될 경우 아래 명령어를 입력하세요. 
sudo find /etc -name 'host.conf' 
```

####  파일명이 완벽히 생각 안날때\( 와일드 문자 이용 \) 

 host로 시작되는 모든 파일들이 출력되요. 

```text
root@ip-172-31-35-20:~/example# find /etc -name 'host*'
/etc/hostname
/etc/hosts.deny
/etc/cloud/templates/hosts.redhat.tmpl
/etc/cloud/templates/hosts.suse.tmpl
/etc/cloud/templates/hosts.freebsd.tmpl
/etc/cloud/templates/hosts.debian.tmpl
/etc/host.conf
/etc/hosts.allow
/etc/hosts
```

###  파일 크기 검색 

 50MB 이상의 파일을 검색 하려면 아래 처럼 쓰면 되요.   
일정한 사이즈보다 작은 파이릉ㄹ 검색하기 위해선 -기호를 대신 사용해 주세요. 

```text
root@ip-172-31-35-20:~/example# sudo find / -size +50M
/var/lib/snapd/seed/snaps/core_8935.snap
/var/lib/snapd/snaps/core_8935.snap
/var/lib/snapd/snaps/core_9066.snap
/proc/kcore
find: ‘/proc/2030/task/2030/fd/6’: No such file or directory
find: ‘/proc/2030/task/2030/fdinfo/6’: No such file or directory
find: ‘/proc/2030/fd/5’: No such file or directory
find: ‘/proc/2030/fdinfo/5’: No such file or directory
/usr/bin/docker
/usr/bin/dockerd
```

## find 명령어 옵션 

#### exec 명령어 실행 

find명령어와 함께 다른 명령어를 사용 할 수 있어요.  
 파일 \(삭제, 이동 등\) 관리하거나 소스코드를 분석 할때 사용되요.

* 현재 디렉토리에 있는 모든 파일을 grep 명령어로 검사하면서 "DB\_NAME"이라는 문자열이 있을 경우 파일 이름, 라인 번호와 함께 내용을 출력하게 되요. 

```text
$ find ./ -exec grep -Hn "DB_NAME" {} \; 2>dev/null
```

find 명령어를 실행하는데  있어 권한등 여러 문제가 있을 경우 발생하는 에러 메세지는 리다이렉트 시키는 명령어가 포함되어 있어요. 

find 명령어와 함께 grep 명령어를 사용하면 처음 접하는 소스코드를 쉽게 분석할 수 있어요. 

###  

* * *  {} \; 2&gt;/dev/null   

