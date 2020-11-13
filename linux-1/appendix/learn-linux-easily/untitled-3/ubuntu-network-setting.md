# ubuntu network setting

리눅스 ubuntu에서 네트워크 설정하기

쉘에서는 /etc/network/interfaces 파일을 에디터로 열어 네트워크를 설정할 수 있다.

설정된 네트워크 정보를 확인하기 위해서 ifconfig 명령어를 아래와 같이 사용한다.[![](https://postfiles.pstatic.net/MjAxOTExMjFfMTI1/MDAxNTc0MzE5NTQ2NzAy.ChDWKIMr7ghQZQizDtAb4FVjGEf1U3Eihq2-v38bAVQg.b69X15_Y5y7rFuKlVOE9Tqb_S0svS1DWAVJrj_nw128g.PNG.mincoding/image.png?type=w773)](https://blog.naver.com/PostView.nhn?blogId=mincoding&logNo=221714411887&parentCategoryNo=&categoryNo=36&viewDate=&isShowPopularPosts=true&from=search#)

/etc/network/interfaces

사용자가 사용하는 시스템의 네트워크 기본정보가 설정되어 있는 파일이다.

현재 웹서버의 interfaces를 에디터로 실행 시킨 화면 이다.[![](https://postfiles.pstatic.net/MjAxOTExMjFfMTMw/MDAxNTc0MzE5NjM2NzYz.g4JzbnpgIg-GiwA946thYVd31KRf0QgVaVqeJ30kiRUg.fb-Th4m6LMrPiwhHqKdxnl23zj6D8_bRtExQ-FUn7mgg.PNG.mincoding/image.png?type=w773)](https://blog.naver.com/PostView.nhn?blogId=mincoding&logNo=221714411887&parentCategoryNo=&categoryNo=36&viewDate=&isShowPopularPosts=true&from=search#)

가장 위에 있는 auto라는 키워드를 가진 lo 라는 물리적인 네트워크에 대해 자동으로 인지 한다는 뜻이다.

LoopBack 이란?

lo는 loopback interface의 약자이고, localhost 즉 자기 자신을 가리킨다.

IP Address : 127.0.0.1 **\(LoopBack\)**

​

ubuntu man page 에서 interfaces의 정의

ifup 과 ifdown을 위한 네트워크 인터페이스 설정하는 파일이다.

ifup / ifdown / ifquery / ifconfig 는 리눅스 시스템에서 사용할 수 있는 명령어이다.

​

ifup : interface 파일에 저장 되어 있는 네트워크 정보로 이더넷 카드에 적용시켜 디바이스를 구동 시킨다.

ifdown : 이더넷 카드 장치를 종료 한다. 일반적으로 새로운 네트워크 설정을 적용하기 위에 ifdown을 사용하여 디바이스를 종료시키고 ifup명령어를 통해 새로운 설정을 적용한다.

​[![](https://postfiles.pstatic.net/MjAxOTExMjFfMjEz/MDAxNTc0MzE5ODY2Mjc0.DNqQIFJXIdxlKozhpY1mBBztM9QW4PNrn2m-RiJ8UeAg.iv2zum0oJ7THa3p-m0ElZLvBw0nYeFNlG-frQs1H6iEg.PNG.mincoding/image.png?type=w773)](https://blog.naver.com/PostView.nhn?blogId=mincoding&logNo=221714411887&parentCategoryNo=&categoryNo=36&viewDate=&isShowPopularPosts=true&from=search#)

​

interfaces 파일에서 사용되는 용어

**auto**

부팅시에 네트워크 해당 인터페이스를 이더넷 카드 장치에 자동으로 올리게 설정 한다.

ifup 명령어를 사용할때 -a 옵션을 더하여 auto 인터페이스를 활성화 시킬 수 있다. 이러한 ifup -a 명령어가 기본적으로 system을 부팅할때 사용하는 시스템 스크립트 내에 저장되어 있다. 여러개의 auto 인터페이스를 설정할 수 있고, 부팅시 순서대로 인터페이스 연결을 시도하게 된다.

​

**allow-**

다양한 서브시스템을 사용할때, 자동으로 인터페이스를 적용시키기 위해 사용한다. Ex\) ifup --allow=hotplug eth0 eth1

hotplug 이벤트가 발생하게 되면 인터페이스를 자동으로 시작하게 된다. hotplug 는 kernel/udev 장치 관리 파일시스템에서 하드웨어가 감지 되었을때 발생하는 이벤트이다. USB-to-Ethernet 등의 장치가 USB를 통해 PC에 연결 되었을때 이 이벤트를 감지하고, 인터페이스를 새로 재설정 한다.

​

**source**

다른 파일에서 네트워크 설정을 가져올때 사용한다. 파일의 경로를 입력하면 쉘에서 파일에 들어있는 설정들을 이용할 수 있다.

​

**source-directory**

특정한 파일을 정하는것이 아니라 source 파일이 들어있는 디렉토리 내에서 여러 파일들을 접근할 수 있다.

​

**mapping**

논리적인 인터페이스 이름이 어떻게 물리적 인터페이스를 불러올지에 대한 것을 명시한다.

​

**iface**

논리적인 인터페이스이다.

mapping을 제외하고 간단한 설정들이 있는데, 예를들어 inet 은 TCP/IP를 나타내며 ipx는 IPX networking을 지원한다. inet6는 IPv6를 지원하는 인터페이스 이다. 이는 물리적인 인터페이스에 어떤 인터페이스가 적용되는지를 나타낸다.﻿\# The primary network interface auto eth0 iface eth0 inet static // TCP/IP 를 지원하는 논리적 인터페이스auto wlan0 iface eth0 inet dhcp // TCP/IP 이며 dhcp 로 설정하는 것을 의미한다.

