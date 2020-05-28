# 10. 경로확인 및 변경

리눅스에서는 \_\_디렉토리 == 폴더\_\_ 라는거 명심하세요. 

### 현재 위치 확인 방법 첫번

![&#xD2F8;&#xB4DC;&#xB294; home &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xB97C; &#xB9D0;&#xD574;&#xC694;.](../../.gitbook/assets/image%20%28180%29.png)

  


 참고로 유닉스에서  디렉토리는 자신만의 사용자를 가져요

![&#xC0AC;&#xC6A9;&#xC790;&#xBCC4; &#xD648;&#xB514;&#xB809;&#xD1A0;&#xB9AC;](../../.gitbook/assets/image%20%2873%29.png)

결국 그 홈 디렉토리는 독립된 파일과 디렉토리를 또 가지게 되는거조.  


 다시 터미널로 돌아가보면 노란색부분이 사용자 이름을 나타낸거에요.

![&#xD574;&#xB2F9;&#xD658;&#xACBD;&#xC758; &#xC0AC;&#xC6A9;&#xC790; &#xC774;&#xB984;](../../.gitbook/assets/image%20%28146%29.png)

![&#xC791;&#xC5C5; &#xC704;&#xCE58;&#xAC00; &#xBC14;&#xB00C;&#xBA74; &#xD2F8;&#xB4DC;&#xAC00; &#xBC14;&#xB01C;](../../.gitbook/assets/image%20%28195%29.png)





###  현재 위치 확인방법 두 번째

![pwd\(print the name of working directory\)](../../.gitbook/assets/image%20%28122%29.png)

 아래 처럼 pwd를 입력하면 슬러시로 표시된 현재 위치가 표시되요. 

![&#xD604;&#xC7AC; &#xC704;&#xCE58; &#xCD9C;&#xB825;](../../.gitbook/assets/image%20%28197%29.png)

![&#xD2F8;&#xB4DC;&#xC640; /Users/&#xB294; &#xAC19;&#xC740;&#xB73B;](../../.gitbook/assets/image%20%28134%29.png)

 맨 왼쪽 슬러쉬 의미가 없는게 아니에요. 디렉토리 중에서 가장 원조가 되는 루트, 최상위라는 명칭이 붙어 있어요.

![](../../.gitbook/assets/image%20%284%29.png)



 이 루트 디렉토리 안에서 수많은 디렉토리들이 파생되고 파일들이 담겨져 있는걸 알수 있어요. 

![&#xB8E8;&#xD2B8; &#xB514;&#xB809;&#xD1A0;&#xB9AC;&#xC758; &#xD2B8;&#xB9AC;&#xAD6C;&#xC870;](../../.gitbook/assets/image%20%28137%29.png)

---

###  디렉토리 변경 명령어 cd

![](../../.gitbook/assets/image%20%2864%29.png)

 cd 명령어는 그 뒤에 가고 싶은 경로를 인자로 넣어줘요.  


> cd /User/hs/Pictures

![pwd&#xC640; cd &#xBA85;&#xB839;&#xC5B4; &#xC0AC;&#xC6A9;](../../.gitbook/assets/image%20%2816%29.png)

