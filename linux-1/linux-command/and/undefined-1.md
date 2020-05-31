# 네트워크 명령어

일반적으로 네트워킹이 정상적으로 이루어지려면 OS에 IP주소, 서브넷 마스크, 게이트웨이 주소, DNS 서버주소를 입력해야해요. 

* window키 + R -&gt; 'cmd'입력 -&gt;ipconfig명령어 실행
* VMnet8 확인 
* 만약 VMnet8이 안보이면 ipconfig/all 명령어 실행 
* VMware Virtual Ethernet Adapter for Vmnet8 부분을 확인함. 

IP주소 : 192.168.OOO.3 ~192.168.OOO.254  
넷마스크 : 255.255.255.0  
게이트웨이 : 192.168.OOO.2  
DNS서버 : 192.168.OOO.2

> 참고로 IP주소중 세 번째 숫자는 VMware를 설치할 때마다 0 ~255 중 하나가 임의로 할당 되므로 VMware를 재설치하면 이 숫자가 바뀌게 되요.

