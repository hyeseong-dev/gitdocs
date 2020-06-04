# \[pip\] requirement.txt  일괄 설치

1. 현재 설치된\(base환경, 특정 가상환경\) 패키지 목록들을 파일로 저장시킴. 

```text
pip freeze > requirements.txt
```

2. requirements.txt 파일로 일괄적으로 패키지들 전부를 설치 시킬수 있어요. 

```text
pip install -r requirements.txt
```

> 만약 2번에서 아래와 같은 오류가 나면
>
> ```text
> The directory '/home/ubuntu/.cache/pip/http' or its parent directory is not owned by
> the current user and the cache has been disabled. 
> Please check the permissions and owner of that directory. 
> If executing pip with sudo, you may want sudo's -H flag.
> ```
>
>  아래 sudo와 -H 옵션을 붙여서 재 실행해보세요.   
> 현재 계정에 권한이 부여되지 않아서 일어나는거라고 
>
> ```text
> sudo -H pip install -r requirements.txt
> ```

