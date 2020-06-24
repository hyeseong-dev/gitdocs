---
description: 저장소 이름 삭제후 재등록으로 해결
---

# Push&Pull Error

Github  원격저장소에 merge conflict 오류는 아닌데 push, pull 오류가 발생하는 경우. 

1\) git remote -v 로 정상 등록이 되었는지 확인함.  - 잘 등록 된거 확인함. 

```text
$ git remote -v 
origin  https://github.com/osori-magu/pyweb.git (fetch)
origin  https://github.com/osori-magu/pyweb.git (push)
```

2\) 잘 등록 되었다면 기존의 등록된 저장소 이름을 삭제

```text
$ git remote remove 저장소이
```



