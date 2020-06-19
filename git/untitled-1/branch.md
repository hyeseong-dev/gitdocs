# Branch 만들기



```text
git init
```

git init을 하게 되면 현재 디렉토리에 저장소가 만들어져요. 

```text
vim f1.txt
```

vim에디터로 a라는 글자를 입력할게요.  그리고 !wq!를 입력하고 저장하고 나올게요. 

```text
git add f1.txt
git commit -m '커밋 메시지 입력'
```

```text
vim f1.txt

<vim editor> 
b #입력후 저장 
```

```text
git commit -a -m '2' # -a 옵션은 git add f1.txt

# 위 1번 코드의 옵션을 축약하면 -am이라고 적용해도 되요. 
git commit -am '2' 
```

