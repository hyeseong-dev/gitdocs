# 수정, 삭제된 파일만 staging 하기

> **modified , deleted된 파일만 stage 상태로 일괄로 처리하고 싶다면?**

### git add -u 

혹은 이미 수정과 커밋을 한 상태라면 

### git commit -a 

**stackoverflow 글**

\*\*\*\*

```text
#!/bin/bash

git add `git status | grep modified | sed 's/\(.*modified:\s*\)//'`
```

Or even better:

```text
$ git ls-files --modified | xargs git add
```

\*\*\*\*[**https://stackoverflow.com/questions/7124726/git-add-only-modified-changes-and-ignore-untracked-files**](https://stackoverflow.com/questions/7124726/git-add-only-modified-changes-and-ignore-untracked-files)\*\*\*\*

