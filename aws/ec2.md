# 키페어 없이 EC2 접속

####  EC2 Key Pair 없이 비밀번호로 접속 <a id="AWS-EC2-Key-Pair-&#xC5C6;&#xC774;-&#xB300;&#xC2E0;-&#xBE44;&#xBC00;&#xBC88;&#xD638;&#xB85C;-&#xC811;&#xC18D;&#xD558;&#xAE30;"></a>

원래 AWS EC2 인스턴스를 만들고 터미널에서 접속하려면 기본 명령어는 `ssh -i [KeyPairName].pem ubuntu@[인스턴스 IPv4 IP 주소]` 이다.  
하지만, 다양한 PC나 심지어 모바일에서 접속할 때 Key Pair를 가지고 있지 않다면 루트 사용자로 로그인조차 할 수 없다는 단점이 있다.  
이를 해결하기 위해 Key Pair 없이 Password만으로 인스턴스 SSH에 접속할 수 있는 방법을 쉽게 써보려고 한다.

인스턴스 AMI는 EC2 Ubuntu 16.04.3 LTS 기준이다. 또한, 사용자 이름은 Default Setting인 `ubuntu`로 설명하겠다.

![1](https://user-images.githubusercontent.com/37604501/42146948-16988ed6-7e06-11e8-86d3-ffc746ae34e3.png)

1. 윈도우 기준으로 `윈도우 키 + cmd 입력 + 명령 프롬프트 오른쪽 버튼 - 관리자 권한으로 실행`로 터미널 실행 고고

![2](https://user-images.githubusercontent.com/37604501/42146937-14dd09a0-7e06-11e8-9e04-ac74fcdd40c5.png)

1. 우선 `Key Pair 파일`이 있는 폴더로 가서 Key Pair로 로그인

![3](https://user-images.githubusercontent.com/37604501/42146938-150aa4aa-7e06-11e8-8e5b-8e9d78a2e186.png)

1. `sudo passwd ubuntu` 입력\(ubuntu가 아닌 다른 사용자 계정이라면 그 이름 입력\) 후 `Password` 입력\(입력이 되지 않는것처럼 나오겠지만 일부러 안보이게 처리된다.\)

![4](https://user-images.githubusercontent.com/37604501/42146939-15343ad6-7e06-11e8-8952-49e75f00489e.png)

1. `sudo vi /etc/ssh/sshd_config` 입력

![5](https://user-images.githubusercontent.com/37604501/42146940-155f3920-7e06-11e8-8595-2416ae408914.png)

1. `/PasswordAuth` 입력

![6](https://user-images.githubusercontent.com/37604501/42146941-158ae002-7e06-11e8-920d-36c332802bd7.png)  
![7](https://user-images.githubusercontent.com/37604501/42146942-15b66920-7e06-11e8-8962-6c8386817ca9.png)  
![8](https://user-images.githubusercontent.com/37604501/42146944-15e1f4f0-7e06-11e8-9ab1-10987dfc413a.png)

1. `i` 눌러서 INSERT MODE로 바꾸고 `PasswordAuthentication no`에서 `no`를 `yes`로 바꿈

![9](https://user-images.githubusercontent.com/37604501/42146945-160d1f04-7e06-11e8-83d5-5fecd7894198.png)

1. 다시 `i` 누른 후 `:wq` 입력하고 나옴
2. 나중에 Key Pair로 로그인 할 때를 위해 Key Pair를 복사하자.

   |  |  |
   | :--- | :--- |

3. SSH를 다시 시작해주자.

   |  |  |
   | :--- | :--- |

4. `exit` 입력해서 로그아웃을 해주고

![10](https://user-images.githubusercontent.com/37604501/42146946-16402fac-7e06-11e8-9f46-e991310d6893.png)

**11. `ssh ubuntu@[인스턴스 IPv4 IP주소]` 로 로그인을 해본다.**

1. 아까 설정한 `Password`를 입력해주면..

![11](https://user-images.githubusercontent.com/37604501/42146947-166ba3a8-7e06-11e8-9c10-c8b3ab27316c.png)

1. 접속 완료!

이전과 비교해서 엄청나게 간단해졌당.

* AWS KEY 없이도 어떤 Device에서도 접속 가능하다.
* SSH 명령어가 매우 간소화되었다.

반대급부로 Password 뚫리면 그말싫.. 위험해진다..  
비밀번호는 반드시 어려운걸로!  
이제 행ㅋ복ㅋ EC2 인스턴스를 사용해보자.

