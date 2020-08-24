# SSH와SSL의 차이

**SSH는 보통 Telnet과 같은 원격조종에 있어서의 보안성을 유지시켜줍니다.**

주로 사용되는 포트는 **22번 포트를 사용하고** 있고요.

Secure Shell은 OSI 7계층 구조에서 어플리케이션\(응용\)계층에 속합니다.

즉, 원격접속 패킷을 보낼때 데이터를 암호화 시킨다고 보면 되겠습니다.

자료를 올릴때는 sftp를 사용하겠군요..

**SSL은 Secure Sockets Layer 라고 하여 웹서버 인증이나 서버 인증이라고도 말합니다.**

웹브라우저와 서버간의 통신이 암호화되므로 중간에 패킷을 가로챌 수 없도록 하는 솔루션입니다.

보통 인터넷상에서 결제할때나 인터넷뱅킹과 같은 중요한 일을 할때 사용되는 방식이며

클라이언트가 서버에 접속하게 되면 서버 인증서를 전송받습니다.

클라이언트측에서는 이 서버 인증서를 분석한 후, 신뢰할 수 있는 인증서인지 검토하고 공개키를 추출합니다.

클라이언트가 Session키로 사용 할 임의의 메세지를 서버의 공개키로 암호화 하고 전송합니다.

서버는 자신의 비밀키로 세션키를 복호화시켜 그 키를 사용하고, 대칭키암호방식으로 메세지를 암호화합니다.

이때 사용되는것이 기존의 http가 아닌 https 라는 프로토콜을 사용하게 됩니다.

 ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h1.gif%22&type=m10000_10000) **ssh 사용법 및 기본 명령어**

       
  
    ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000)압축을 푼후 ssh아이콘을 클릭 ..  
![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fssh_install_1.gif%22&type=m10000_10000)  
  
  
   ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000)메시지에 따라 next-&gt;yes....를 클릭하면 설치 완료.  
  
![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fssh_install_2.gif%22&type=m10000_10000)

   ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000)바탕화면에 SSH Secure Shell Client 더블클릭 합니다..  
![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fssh_install_1_2.gif%22&type=m10000_10000)  
  
   ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000)**Add Profiles을 선택 계정설정** 사항을 입력 합니다  
  
![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fssh_install_3.gif%22&type=m10000_10000)   
  
  
   ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000) 다시 **Edit Profiles에서 세부사항** 등록..  
 ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fssh_install_4.gif%22&type=m10000_10000)  
  
   ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000)설정이 끝나면 메인화면에서 **Profiles 클릭후** 조금전 생성한 계정을 클릭  
  
![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fssh_install_5_1.gif%22&type=m10000_10000)   
  
   ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000)화면이 뜨면 신청시 부여 받은 패스워드\(접속 패스워드/ftp와 동일\)를 입력 합니다



  
[![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Ftopofpage.gif%22&type=m10000_10000)](http://mireene.com/webimg/ssh_menual/#)               

   ![](https://dthumb-phinf.pstatic.net/?src=%22http%3A%2F%2Fmireene.com%2Fwebimg%2Fssh_menual%2Fbtn_h2.gif%22&type=m10000_10000)**기본적인 명령어..-&gt; login**  
유닉스 시스템은 기본적으로 multi-user개념에서 시작하였기 때 문에 시스템을 이용하기 위해서는 반드시 로그인을 하여야 합니 다. 로그인은 PC 통신에서도 많이 사용되어져 왔기 때문에 그 개 념 설정에 그다지 어려움이 없을 것입니다. 흔히 말하는 ID를 입 력하는 과정입니다. 유닉스 시스템에서는 영문자의 대소문자 구별이 엄격합니다. 이 점 주의 해주시기 바랍니다. \(login 의 반대는 logout 또는 exit 또는 ctrl-D\)  
  
**-&gt; passwd**  
자신의 패스워드를 바꾸는 명령입니다. 유닉스, 특히 인터넷의 세계에서는 일반 컴퓨팅 상황에 비하여 훨씬 해킹에 대한 위험이 높습니다. 패스워드는 완성된 단어 보다는 단어 중간에 숫자나 키보드의 ^, \#, ' 등과 같은 쉽게 연상 할 수 없는 기호를 삽입하여 만들어 주는 것이 좋습니다.  
  ex\)      \# 위에서 설명한 방법으로 자신의 계정에 접속을 합니다  
            \[htest@ns htest\]$ passwd                 \# passwd 명령  
            Changing password for user htest.       
            Changing password for htest               
            \(current\) UNIX password:                  \# 현재 사용중인 패스워드를 입력 합니다  
            New password:                                \# 변경하고자 하는 패스워드 입력  
            Retype new password:                      \# 확인을 위해 다시 한번 입력  
            passwd: all authentication tokens updated successfully.    \# 패스워드 변경 성공 메시지  
            \# 기존 패스워드와 동일 하거나 자릿수가 적을 때 "BAD PASSWORD:~~"   
  
**-&gt; ls** - 디렉토리의 파일 표시  
도스의 dir명령과 흡사한 명령입니다. 일반적으로 ls라고 입력했 을 때에는 디렉토리와 파일만을 표시해 줍니다. ls에는 도스의 d ir과는 비교할 수도 없을 만큼 옵션이 많습니다.  
몇가지 자주 사용되는 옵션입니다.  
  
**-&gt; ls** -al : Hidden속성의 파일을 표시해주는 a옵션과 파일의 종류, 사용권한 등 자세한 정보를 보여주는 옵션 l을 함께 사용하여 보다 자세한 정보를 보고자 할 때 이용합니다.  
  
**-&gt; ls** -aC : Hidden속성의 파일을 보여주되, 도스의 dir/w명령과 같 이 한줄에 여러개의 정보를 보여주도록 C옵션을 함께 사용하여 이용합니다.  
  
**-&gt; ls** -R : 도스의 dir/s 명령과 같이 서브디렉토리의 모든 명령어 를 보여주는 옵션 R과 같이 사용할 수도 있습니다.  
  
**-&gt; cd** - Change Directory  
cd 명령어는 도스의 cd와 그 쓰임새도 같고 사용할 때에 한가지 만 주의하시면 됩니다. 그것은, 도스에서는 cd\dos와 같이 사용하지만, 유닉스에서는 반 드시 cd 뒤에 한칸을 띄우고 '\' 대신 '/'를 사용한다는 것입니 다.  
예\) cd temp  
  
유닉스의 디렉토리는 말 그대로 거미줄 같이 복잡하게 얽혀 있습 니다. 따라서 개인의 홈디렉토리로의 이동을 위하여 HNCNET에서 는 'cd ~' 또는 그냥 'cd'를 입력하면 자신의 홈디렉토리로 이동을 하도록 준비 가 되어 있습니다. 잘 이용하시면 꽤 쓸모있게 사용될 것입니다.  
  
**-&gt; mkdir** - 도스의 MD, Make Directory  
이 기능 역시 도스의 MD와 같은 기능을 하는 명령어입니다. 옛날 도스책을 보신 분들은 'MD \(Make Directory-MKDIR\)이라는 설명이 기억 나실 수도 있겠는데, 유닉스에서는 md라는 명령어가 아니라 반드시 mkdir로 디렉토리를 만드셔야 합니다.  
**-&gt; rmdir** - 도스의 RD, Remove Directory  
rmdir 명령어는 도스의 RD 명령어와 동일하게 사용하실 수 있는 명령어로 rmdir로 이용하시면 된다는 것외에는 다른 점이 없습니 다. 주의하실 점은 절대로 자신의 홈디렉토리를 지우시면 안된다 는 것입니다. 자신의 홈디렉토리는 '/free/아이디'의 이름으 로 존재합니다.  
  
**-&gt; mv** - move, 도스의 move?  
마치 도스의 move와 같이 사용되는 명령어입니다. 파일을 다른곳 으로 이동시키거나 이름을 바꿀때 이용하는 명령어입니다.  
**-&gt; cp** - copy  
도스의 copy 명령어와 같다라고 생각하시면 됩니다. 그러나 도스 의 일반 옵션을 이용할 수는 없습니다. 일반적으로 옵션을 많이 사용하지는 않지만, 옵션을 보시고 싶으실 때에는 주저없이 man cp라고 입력하십시오. 유닉스에서는 아주 자세한 help파일이 존 재합니다.  
  
rm - remove  
파일을 지울때 사용하는 명령어입니다. 도스의 DEL명령어와 같이 사용하시면 되지만, 주의하실 점은 유닉스에서는 도스와 같이 un delete를 지원하지 않는다는 것입니다.  
  
**-&gt; pwd** - 현재의 디렉토리 표시  
현재 디렉토리를 표시할 필요가 왜 있는지 궁금해 하시는 분들도 계시겠지만, 유닉스 시스템에서는 사용자에게 일일이 현재 디렉 토리를 가르쳐 주지 않는 경우가 많습니다. 도스등 개인 사용자 를 위주로 하는 시스템에서는 디렉토리의 길이가 그리 길지 않아 서 디렉토리를 모두 보여주어도 큰 지장이 없지만 유닉스 시스템 의 경우 아예 디렉토리의 길이만 한줄을 넘기는 경우도 발생할 수 있습니다. 이렇게 현재 자신이 작업을 하고 있는 디렉토리가 어디인지 알수 없을 때 이용하는 명령어입니다.  
  
**-&gt; alias**  
doskey alias와 비슷하게 이용할 수 있는 쉘 명령어 alias는 말그대로 별명입니다. 사용자는 alias를 이용하여 긴 유 닉스 명령어를 간단하게 줄여서 사용할 수도 있습니다. 이들 알리아스는 \[alias ls 'ls -al'\]등과 같이 사용하시면 되는데, 한 번 지정한 alias를 계속해서 이용하시려면, 자신의 홈디렉토리에 있는 .cshrc\(Hidden 속성\)을 pico등의 에디터를 이용하여 변경시 키면 됩니다.  
  
man / info  
Linux의 명령 사용법에 대한 매뉴얼/정보 명령입니다. 예\) man pwd  / info passwd  
파일 목록  
       -rw-rw-rw-   1   kim   users       50  May 17 06:55  test.txt  
       drwxrwxr-x    3   root  users    1024  Jul    6  05:30  work/  
속성 -u   g   o            
  
**-&gt; cat**  
파일의 내용을 보는 명령입니다. DOS의 type과 같습니다.   예\) cat  /etc/hosts    
chmod  
파일의 읽기/쓰기/실행 권한을 설정합니다.  예\) chmod go-r  test.txt   예\) chmod 777 test.txt  
  
**-&gt; more**  
파일의 내용을 페이지 단위로 끊어 보게 해 줍니다. DOS의 more와 같습니다.  예\) more  /etc/secret.txt    
  
**-&gt; rm : remove**  
rm \[-I\]\[-r\] filename 파일을 지울때 사용하는 명령어입니다.  
  
**-&gt; du -h**  
계정의 사용량을 알아보는 명령어  
\[abc@tset\]$ du -h &lt;-- ssh 로 접속후 홈디렉토리에서 du -h 입력

**\[출처\]** [SSH 와 SSL의 차이점](https://blog.naver.com/finsub/50038120013)\|**작성자** [최선을 다하는 삶](https://blog.naver.com/finsub)

