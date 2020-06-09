# virtualenv install, activate, deactivate

### 가상환경 구성

![](https://dojang.io/pluginfile.php/14099/mod_page/content/4/047006.png)

### Windows에서 설치

그럼 먼저 Windows에서 가상 환경을 만드는 방법을 알아보겠습니다. 가상 환경은 venv 모듈에 가상 환경 이름을 지정해서 만듭니다.

venv는 파이썬 3.3이상부터 사용 가능

* **python -m venv 가상환경이름**

여기서는 C:\project 폴더 아래에 가상 환경을 만들겠습니다. 다음과 같이 명령 프롬프트에서 example 가상 환경을 만들고 example 폴더 안으로 이동합니다. 그다음에 Scripts 폴더 안의 activate.bat 파일을 실행하면 가상 환경이 활성화됩니다.

Windows 명령 프롬프트

```text
C:\project>python -m venv example
C:\project>cd example
C:\project\example>Scripts\activate.bat
(example) C:\project\example>
```

Windows PowerShell에서는 Activate.ps1 파일을 실행합니다\( ps1 스크립트를 실행할 수 없을 때는 Windows PowerShell을 관리자로 실행한 뒤 Set-ExecutionPolicy RemoteSigned를 입력하고 Y를 입력\).

Windows PowerShell

```text
PS C:\project> python -m venv example
PS C:\project> cd example
PS C:\project\example> .\Scripts\Activate.ps1
(example) PS C:\project\example>
```

프롬프트 앞을 보면 \(example\)과 같이 가상 환경의 이름이 표시됩니다.

이 상태에서 pip로 패키지를 설치하면 C:\project\example\Lib\site-packages 안에 패키지가 저장됩니다\(dir로 파일과 폴더 확인해보기, /B는 최소 포맷 옵션\).

###  ubuntu linux 

os별 파이썬 가상환경 설치가 너무 다르다는 점. 꼭 명심하세요.  
이렇게하면 bin디렉토리에 activate 파일이 만들어져요.    


#### 출처 [https://askubuntu.com/questions/1202547/problem-with-source-env-bin-activate](https://askubuntu.com/questions/1202547/problem-with-source-env-bin-activate)

```text
virtualenv --python=python3.8(버전) pyvenv(가상환경이름)
```

```text
python -m virtualenv pyenv(가상환경 이름)
```



###  가상환경 종료 

```text
deactivate
```



###             패키지 목록 관리하기

특히 가상 환경에 설치된 패키지는 목록을 저장해 두었다가 나중에 다시 설치할 수 있습니다. 다음과 같이 pip freeze로 패키지 목록과 버전 정보를 requirements.txt 파일에 저장합니다\(git 등으로 버전 관리를 할 때 저장소에 설치된 패키지를 모두 추가하지 않고, requirements.txt 파일만 관리하면 됩니다\).

```text
(example) C:\project\example>pip freeze > requirements.txt
```

requirements.txt 파일의 내용대로 패키지를 설치하려면 pip install에서 -r 또는 --requirement 옵션을 사용합니다.

```text
(example) C:\project\example>pip install -r requirements.txt
```

requirement.txt 파일의 내용대로 패키지를 삭제하려면 pip uninstall에서 -r 또는 --requirement 옵션을 사용합니다.

```text
(example) C:\project\example>pip uninstall -r requirements.txt
```

###            가상 환경별로 파이썬 버전 구분하기

만약 가상 환경별로 파이썬 인터프리터 버전을 다르게 만들고 싶다면 해당 버전의 파이썬 인터프리터로 venv 모듈을 실행하면 됩니다. 다음은 파이썬 3.4를 사용하는 가상 환경을 만듭니다\(파이썬 3.4를 설치했다고 가정\).

```text
C:\project>C:\Python34\python.exe -m venv example3
```

이렇게 하면 venv 모듈을 실행한 파이썬 실행 파일\(인터프리터\)이 가상 환경 안에 들어갑니다.

###         리눅스와 macOS에서 가상 환경 만들기

이번에는 리눅스와 macOS에서 가상 환경을 만드는 방법입니다. 다음과 같이 python3으로 venv 모듈을 실행하여 가상 환경을 만들고, source로 bin 디렉터리 안의 activate 파일을 적용하여 가상 환경을 활성화합니다.

리눅스, macOS

```text
~$ python3 -m virtualenv example
~$ cd example
~/example$ source bin/activate
(example) ~/example$
```

리눅스와 macOS에서도 pip 사용 방법은 앞에서 설명한 것과 같습니다.

####    가상 환경 폴더를 다른 곳으로 이동시켰다면?

가상 환경을 사용할 때 주의할 점이 있는데, 가상 환경을 만들고 나서 폴더\(디렉터리\)를 다른 곳으로 이동시키면 활성화가 안 됩니다. 왜냐하면 가상 환경을 활성화하는 activate.bat, Activate.ps1, activate 파일 안에 현재 가상 환경 폴더의 경로가 내장되어 있기 때문입니다. 만약 가상 환경 폴더를 다른 곳으로 이동시켰다면 activate.bat, Activate.ps1, activate 파일 안의 VIRTUAL\_ENV 부분을 이동시킨 폴더 경로로 수정해줍니다.

###    아나콘다 가상 환경 만들기

아나콘다에서 venv를 사용해도 되지만 아나콘다는 전용 가상 환경을 제공하므로 이 환경을 사용하는 것을 권장합니다.

아나콘다에서는 conda를 사용하여 가상 환경을 만듭니다. conda는 아나콘다 설치 폴더의 Scripts 안에 들어있습니다.

* **conda create --name 가상환경이름**

```text
C:\project>C:\Users\dojang\Anaconda3\Scripts\conda.exe create --name example
```

만약 가상 환경에 특정 파이썬 버전을 설치하고 싶다면 python=3.5처럼 버전을 지정해줍니다. 이때는 64비트 파이썬이 설치됩니다.

```text
C:\project>C:\Users\dojang\Anaconda3\Scripts\conda.exe --name example python=3.5
```

32비트 파이썬을 설치하려면 CONDA\_FORCE\_32BIT에 1을 지정한 뒤 conda로 가상 환경을 만들면 됩니다\(반드시 명령 프롬프트에서 실행\).

```text
C:\project>set CONDA_FORCE_32BIT=1
C:\project>C:\Users\dojang\Anaconda3\Scripts\conda.exe --name example python=3.5
```

conda는 venv와는 달리 가상 환경을 현재 폴더에 생성하지 않고 아나콘다 설치 폴더의 envs 안에 생성합니다.

* 예\) C:\Users\dojang\Anaconda3\envs\example

가상 환경을 활성화할 때는 아나콘다 설치 폴더의 Scripts\activate에 가상 환경 이름을 지정하여 실행해야 합니다\(반드시 명령 프롬프트 cmd에서 실행\).

* **activate 가상환경이름**

```text
C:\project>C:\Users\dojang\Anaconda3\Scripts\activate example
(example) C:\project>
```

아나콘다 가상 환경에 패키지를 설치할 때는 pip 대신 conda를 사용해야 합니다. 만약 pip를 사용하면 아나콘다 설치 폴더의 Lib/site-packages 안에 패키지가 저장되므로 주의해야 합니다.

* **conda install 패키지**

```text
(example) C:\project>conda install numpy
```

다음은 conda의 주요 명령입니다.

* **conda info**: 현재 환경 정보 출력
* **conda search 패키지**: 패키지 검색
* **conda install 패키지=버전**: 특정 버전의 패키지를 설치\(예: conda install numpy=1.11.3\)
* **conda install 패키지=버전=파이썬버전**: 파이썬 버전을 지정하여 특정 버전의 패키지를 설치\(예: conda install numpy=1.11.3=py36\_0\)
* **conda update 패키지**: 패키지 업데이트
* **conda list**: 패키지 목록 출력
* **conda remove 패키지**: 패키지 삭제
* **conda list --export &gt; package-list.txt**: 패키지 목록 및 버전 정보 저장:
* **conda install --file package-list.txt**: 패키지 목록으로 설치

###        가상 환경을 사용하는 IDLE 실행하기

venv, conda 가상 환경을 사용하는 IDLE을 실행하려면 가상 환경을 활성화 시킨 뒤 idlelib 모듈을 실행하면 됩니다. 이렇게 하면 IDLE에서도 현재 가상 환경의 패키지를 사용할 수 있습니다.

Windows

```text
(example) C:\project\example>pythonw.exe -m idlelib
```

macOS, 리눅스

```text
(example) ~/example$ python3 -m idlelib
```

출처: [https://dojang.io/mod/page/view.php?id=2470](https://dojang.io/mod/page/view.php?id=2470)

