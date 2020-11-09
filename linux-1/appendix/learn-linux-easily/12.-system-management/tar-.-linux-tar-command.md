# 리눅스 tar 명령어 사용법. \(Linux tar command\) - 파일 압축 및 해제



#### 1. tar 명령어. \(Tape ARchiver\) <a id="1-tar-&#xBA85;&#xB839;&#xC5B4;-tape-archiver"></a>

![&#xB9AC;&#xB205;&#xC2A4; tar &#xBA85;&#xB839;&#xC5B4;](https://t1.daumcdn.net/cfile/tistory/997F4C355C330EC626)

**tar**는 여러 개의 파일을 하나의 파일로 묶거나 풀 때 사용하는 명령입니다. "테이프 아카이버\(Tape ARchiver\)"의 앞 글자들을 조합하여 "tar"라는 이름으로 명명됩니다.

"테이프 아카이버\(Tape ARchiver\)"의 "아카이버\(Archiver\)"는 통상적으로 "여러 개의 파일을 하나의 파일로 합치는 프로그램"을 의미합니다. 저장 장치에 파일을 저장하거나 네트워크를 통해 파일을 전송할 때 파일이 여러 개 있으면 관리가 복잡해지기 때문에, 여러 파일을 하나로 합쳐서 처리하기 위한 목적으로 만들어진 프로그램이죠. 그리고 "테이프\(Tape\)"에서 알 수 있듯이, 과거에 저장 장치로 사용되었던 테이프\(Tape\)에 파일을 백업하기 위해 만들어진 프로그램이라는 것을 유추할 수 있습니다.

![&#xB9AC;&#xB205;&#xC2A4; tar &#xB3D9;&#xC791;](https://t1.daumcdn.net/cfile/tistory/99A1D43B5C330EC618)

보통 리눅스에서 파일을 압축 파일을 다룰 때, "tar로 압축\(compress\)한다"는 표현을 쓰는 경우가 많은데, 정확히 말하자면 tar 자체는 "데이터의 크기를 줄이기 위한 파일 압축"을 수행하지 않습니다. 앞서 설명했듯이, 여러 파일을 하나의 파일로 묶는 용도로 사용될 뿐이죠. 대신, tar를 통해 하나로 합쳐진 파일을 gzip 또는 bzip2 방식을 사용하여 압축할 수 있는데, 이 때 gzip 또는 bzip2 명령을 따로 수행하지 않고 tar 명령의 옵션으로 처리할 수 있습니다. 이런 이유로, "tar로 압축한다"는 표현이 통용될 수 있는 것이고, "tar 압축"이라는 말이 사용자 입장에서는 아주 잘못된 표현은 아니라고 할 수 있죠.

tar 명령을 통해 만들어지는 파일은 보통 ".tar" 확장자를 사용합니다. 그리고 gzip 또는 bzip2으로 압축된 경우, 파일 뒤에 ".gz" 또는 ".bz2" 확장자를 추가하여 ".tar.gz" 또는 ".tar.bz2"로 파일 이름을 지정하거나, 드물지만 좀 더 간략하게, tar + gzip을 ".tgz"로, tar + bzip2를 ".tb2", ".tbz", "tbz2" 등으로 지정하기도 합니다.

tar가 널리 쓰이게 이유 중 한 가지는, 단순 아카이버 기능에 더해, tar로 묶여지기 전 파일들의 속성과 심볼릭 링크, 디렉토리 구조 등을 그대로 가져갈 수 있는 특징 때문입니다. 그래서 최근에는 리눅스 용 프로그램, 데이터, 소스 및 라이브러리 등을 배포하는 용도로 많이 사용됩니다.

#### 2. tar 명령어 옵션. <a id="2-tar-&#xBA85;&#xB839;&#xC5B4;-&#xC635;&#xC158;"></a>

tar 명령은 그 범용성 만큼이나 많은 실행 옵션을 가지고 있습니다. 하지만 모든 옵션을 외울 필요는 없고, 몇 가지 주요 옵션에 대한 조합만 익히고 있어도 tar 명령을 사용하는데 있어 큰 어려움이 없습니다.

tar 명령의 주요 옵션은 아래와 같습니다. \(더 자세한 옵션은 "tar --help" 명령을 통해 확인할 수 있습니다.\)

```text
    tar [OPTION...] [FILE]...
        -f     : 대상 tar 아카이브 지정. (기본 옵션)
        -c     : tar 아카이브 생성. 기존 아카이브 덮어 쓰기. (파일 묶을 때 사용)
        -x     : tar 아카이브에서 파일 추출. (파일 풀 때 사용)
        -v     : 처리되는 과정(파일 정보)을 자세하게 나열.
        -z     : gzip 압축 적용 옵션.
        -j     : bzip2 압축 적용 옵션.
        -t     : tar 아카이브에 포함된 내용 확인.
        -C     : 대상 디렉토리 경로 지정.
        -A     : 지정된 파일을 tar 아카이브에 추가.
        -d     : tar 아카이브와 파일 시스템 간 차이점 검색.
        -r     : tar 아카이브의 마지막에 파일들 추가.
        -u     : tar 아카이브의 마지막에 파일들 추가.
        -k     : tar 아카이브 추출 시, 기존 파일 유지.
        -U     : tar 아카이브 추출 전, 기존 파일 삭제.
        -w     : 모든 진행 과정에 대해 확인 요청. (interactive)
        -e     : 첫 번째 에러 발생 시 중지.
```

#### 3. tar 명령 사용 예제. <a id="3-tar-&#xBA85;&#xB839;-&#xC0AC;&#xC6A9;-&#xC608;&#xC81C;"></a>

아래 표는 tar 명령 사용 시, 주로 사용하게 되는 옵션 조합입니다. 각 항목의 링크를 선택하면, 좀 더 자세한 예제를 확인할 수 있습니다.

| tar 사용 예 | 명령어 옵션 |
| :--- | :--- |
| [현재 디렉토리의 모든 파일과 디렉토리를 tar로 묶기](https://recipes4dev.tistory.com/146#31-%ED%98%84%EC%9E%AC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EC%9D%98-%EB%AA%A8%EB%93%A0-%ED%8C%8C%EC%9D%BC%EA%B3%BC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A5%BC-tar%EB%A1%9C-%EB%AC%B6%EA%B8%B0) | `tar cvf T.tar *` |
| [대상 디렉토리를 포함한 모든 파일과 디렉토리를 tar로 묶기](https://recipes4dev.tistory.com/146#32-%EB%8C%80%EC%83%81-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A5%BC-%ED%8F%AC%ED%95%A8%ED%95%9C-%EB%AA%A8%EB%93%A0-%ED%8C%8C%EC%9D%BC%EA%B3%BC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A5%BC-tar%EB%A1%9C-%EB%AC%B6%EA%B8%B0) | `tar cvf T.tar [PATH]` |
| [파일을 지정하여 tar 아카이브로 묶기](https://recipes4dev.tistory.com/146#33-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EC%A7%80%EC%A0%95%ED%95%98%EC%97%AC-tar-%EC%95%84%EC%B9%B4%EC%9D%B4%EB%B8%8C%EB%A1%9C-%EB%AC%B6%EA%B8%B0) | `tar cvf T.tar [FILE_1] [FILE_2]` |
| [tar 아카이브를 현재 디렉토리에 풀기](https://recipes4dev.tistory.com/146#34-tar-%EC%95%84%EC%B9%B4%EC%9D%B4%EB%B8%8C%EB%A5%BC-%ED%98%84%EC%9E%AC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EC%97%90-%ED%92%80%EA%B8%B0) | `tar xvf T.tar` |
| [tar 아카이브를 지정된 디렉토리에 풀기](https://recipes4dev.tistory.com/146#35-tar-%EC%95%84%EC%B9%B4%EC%9D%B4%EB%B8%8C%EB%A5%BC-%EC%A7%80%EC%A0%95%EB%90%9C-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EC%97%90-%ED%92%80%EA%B8%B0) | `tar xvf T.tar -C [PATH]` |
| [tar 아카이브의 내용 확인하기](https://recipes4dev.tistory.com/146#36-tar-%EC%95%84%EC%B9%B4%EC%9D%B4%EB%B8%8C%EC%9D%98-%EB%82%B4%EC%9A%A9-%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0) | `tar tvf T.tar` |
| [현재 디렉토리를 tar로 묶고 gzip으로 압축하기](https://recipes4dev.tistory.com/146#37-%ED%98%84%EC%9E%AC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A5%BC-tar%EB%A1%9C-%EB%AC%B6%EA%B3%A0-gzip%EC%9C%BC%EB%A1%9C-%EC%95%95%EC%B6%95%ED%95%98%EA%B8%B0) | `tar zcvf T.tar.gz *` |
| [gzip으로 압축된 tar 아카이브를 현재 디렉토리에 풀기](https://recipes4dev.tistory.com/146#38-gzip%EC%9C%BC%EB%A1%9C-%EC%95%95%EC%B6%95%EB%90%9C-tar-%EC%95%84%EC%B9%B4%EC%9D%B4%EB%B8%8C%EB%A5%BC-%ED%98%84%EC%9E%AC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EC%97%90-%ED%92%80%EA%B8%B0) | `tar zxvf T.tar.gz` |
| [현재 디렉토리를 tar로 묶고 bzip2로 압축하기](https://recipes4dev.tistory.com/146#39-%ED%98%84%EC%9E%AC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EB%A5%BC-tar%EB%A1%9C-%EB%AC%B6%EA%B3%A0-bzip2%EC%9C%BC%EB%A1%9C-%EC%95%95%EC%B6%95%ED%95%98%EA%B8%B0) | `tar jcvf T.tar.bz2 *` |
| [bzip2로 압축된 tar 아카이브를 현재 디렉토리에 풀기](https://recipes4dev.tistory.com/146#310-bzip2%EB%A1%9C-%EC%95%95%EC%B6%95%EB%90%9C-tar-%EC%95%84%EC%B9%B4%EC%9D%B4%EB%B8%8C%EB%A5%BC-%ED%98%84%EC%9E%AC-%EB%94%94%EB%A0%89%ED%86%A0%EB%A6%AC%EC%97%90-%ED%92%80%EA%B8%B0) | `tar jxvf T.tar.bz2` |
| [tar 아카이브 묶거나 풀 때 파일 별 진행 여부 확인하기](https://recipes4dev.tistory.com/146#311-tar-%EC%95%84%EC%B9%B4%EC%9D%B4%EB%B8%8C-%EB%AC%B6%EA%B1%B0%EB%82%98-%ED%92%80-%EB%95%8C-%ED%8C%8C%EC%9D%BC-%EB%B3%84-%EC%A7%84%ED%96%89-%EC%97%AC%EB%B6%80-%ED%99%95%EC%9D%B8%ED%95%98%EA%B8%B0) | `tar cvfw T.tar *` |

**3.1 현재 디렉토리의 모든 파일과 디렉토리를 tar로 묶기.**

"cvf" 옵션에 "\*"를 사용하여, 현재 디렉토리 내 모든 파일과 디렉토리를 tar 아카이브로 묶을 수 있습니다.

```text
$ ls
DIR_1  FILE_1  FILE_2
$ tar cvf T.tar *
DIR_1
FILE_1
FILE_2
```

**3.2 대상 디렉토리를 포함한 모든 파일과 디렉토리를 tar로 묶기.**

"cvf" 옵션에 대상 디렉토리를 지정하여, 지정된 대상 경로를 포함한 모든 파일과 디렉토리를 tar 아카이브로 묶을 수 있습니다. 이 때, tar 아카이브에는 대상 디렉토리 경로가 포함되는 것에 주의하시기 바랍니다.

```text
$ ls ./files
DIR_1  FILE_1  FILE_2
$ tar cvf T.tar files
files/
files/DIR_1
files/FILE_1
files/FILE_2
```

**3.3 파일을 지정하여 tar 아카이브로 묶기.**

"cvf" 옵션에 지정된 파일을 tar 아카이브로 묶을 수 있습니다.

```text
$ ls
DIR_1  FILE_1  FILE_2
$ tar cvf T.tar FILE_1 FILE_2
FILE_1
FILE_2
```

**3.4 tar 아카이브를 현재 디렉토리에 풀기.**

"xvf" 옵션으로 tar 아카이브를 현재 디렉토리에 풀 수 있습니다.

```text
$ tar xvf T.tar
FILE_1
FILE_2
```

**3.5 tar 아카이브를 지정된 디렉토리에 풀기**

"xvf" 옵션과 "-C" 옵션을 조합하여 tar 아카이브를 지정된 디렉토리에 풀 수 있습니다.

```text
$ ls
files  T.tar
$ tar xvf T.tar -C ./files/
FILE_1
FILE_2
$ ls ./files
FILE_1  FILE_2
```

**3.6 tar 아카이브의 내용 확인하기**

"tvf" 옵션을 사용하여 tar 아카이브의 내용을 확인할 수 있습니다. tar 아카이브를 풀기 전, 미리 아카이브에 들어 있는 내용을 확인할 때 사용합니다.

```text
$ tar tvf T.tar
-rw-rw-r-- ppotta/ppotta       0 2018-12-28 19:44 FILE_1
-rw-rw-r-- ppotta/ppotta       0 2018-12-28 19:44 FILE_2
```

**3.7 현재 디렉토리를 tar로 묶고 gzip으로 압축하기.**

"zcvf" 옵션을 사용하여 현재 디렉토리를 tar로 묶은 다음, gzip으로 압축합니다.

```text
$ tar zcvf T.tar.gz *
DIR_1/
FILE_1
FILE_2
$ ls
DIR_1  FILE_1  FILE_2  T.tar.gz
```

**3.8 gzip으로 압축된 tar 아카이브를 현재 디렉토리에 풀기.**

"zxvf" 옵션으로, gzip으로 압축된 tar 아카이브를 현재 디렉토리에 풀 수 있습니다.

```text
$ tar zxvf T.tar.gz
DIR_1/
FILE_1
FILE_2
```

**3.9 현재 디렉토리를 tar로 묶고 bzip2으로 압축하기.**

"jcvf" 옵션을 사용하여 현재 디렉토리를 tar로 묶은 다음, bzip2로 압축할 수 있습니다.

```text
$ tar jcvf T.tar.bz2 *
DIR_1/
FILE_1
FILE_2
$ ls
DIR_1  FILE_1  FILE_2  T.tar.bz2
```

**3.10 bzip2로 압축된 tar 아카이브를 현재 디렉토리에 풀기.**

"jxvf" 옵션으로, bzip2로 압축된 tar 아카이브를 현재 디렉토리에 풀 수 있습니다.

```text
$ tar jxvf T.tar.gz
DIR_1/
FILE_1
FILE_2
```

**3.11 tar 아카이브 묶거나 풀 때 파일 별 진행 여부 확인하기**

tar 옵션에 "w"를 추가하여 tar 아카이브를 묶거나 풀 때 파일 단위로 진행 여부를 확인할 수 있습니다. 묶거나 풀려면 "y" 또는 "yes"를 입력하고 엔터를 입력하면 됩니다.

```text
$ tar cvfw T.tar *
add `DIR_1'?y
DIR_1/
add `FILE_1'?y
FILE_1
add `FILE_2'?y
FILE_2
```

#### 4. 문제 해결. <a id="4-&#xBB38;&#xC81C;-&#xD574;&#xACB0;"></a>

**4.1 tar 압축 포맷 지정 오류. gzip: stdin: not in gzip format**

리눅스에서 파일 이름은 파일 종류 식별을 위한 참고 자료일 뿐, 파일 이름이 해당 파일의 특성을 온전히 결정하지는 않습니다. 그래서 때로는 오해의 여지가 있는 파일 이름 지정으로 인해 사용자에게 혼동을 주는 상황이 발생할 수 있는데요. tar 압축 포맷 지정 시, 그러한 문제가 발생할 수 있죠. 예를 들어, bzip2로 압축된 파일에 ".gz" 확장자를 붙이는 경우입니다.

사용자는 ".gz" 확장자를 보고 자연스럽게 gzip 압축 방식이라고 생각하여 "tar zxvf" 옵션을 사용하려고 할텐데, 이 때 아래와 같은 에러가 발생하죠. \(파일 이름이 "T.tar.gz"이지만 bzip2 방식으로 압축된 파일인 경우입니다.\)

```text
$ tar zxvf T.tar.gz

gzip: stdin: not in gzip format
tar: Child returned status 1
tar: Error is not recoverable: exiting now
```

이런 경우, 사용자는 파일이 잘못되었다고 판단하여 다른 파일을 찾거나, 해당 파일을 지워버릴텐데요. 파일을 지우기 전에, 파일의 형식을 확인하면 파일을 다시 찾아다니는 수고로움을 덜 수 있습니다.

리눅스에서 파일의 형식을 확인하는 명령은 "file" 명령이며, 아래와 같이 tar 아카이브 파일의 형식을 확인할 수 있습니다.

```text
$ file T.tar
T.tar: POSIX tar archive (GNU)
$ file T.tar.gz
T.tar.gz: gzip compressed data, from Unix, last modified: Fri Dec 28 22:14:24 2018
$ file T.tar.bz2 
T.tar.bz2: bzip2 compressed data, block size = 900k
```

출처: 개발자를 위한 레시피  
[https://recipes4dev.tistory.com/146](https://recipes4dev.tistory.com/146)

[https://recipes4dev.tistory.com/146](https://recipes4dev.tistory.com/146)

