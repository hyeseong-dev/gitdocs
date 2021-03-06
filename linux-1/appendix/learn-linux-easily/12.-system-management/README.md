# 12. System Management

## 학습을 시작하기 전에 

![](../../../../.gitbook/assets/image%20%28892%29.png)

## 하드디스크 관리 

![](../../../../.gitbook/assets/image%20%28873%29.png)

![](../../../../.gitbook/assets/image%20%28899%29.png)

###  하드디스크 추가 

#### fdisk로 하드디스크 분할 

![](../../../../.gitbook/assets/image%20%28933%29.png)

#### 하드 디스크 분할 영상 

{% embed url="https://cdn.e-koreatech.ac.kr/Portal/Sources/Contents/2015/old/contents/service/1756/12/03L/12\_07\_01.htm" %}

#### 파일 시스템 포맷

![](../../../../.gitbook/assets/image%20%28924%29.png)

#### mount하

![](../../../../.gitbook/assets/image%20%28901%29.png)

####  /etc/fstab

![](../../../../.gitbook/assets/image%20%28874%29.png)

### RAID 

![](../../../../.gitbook/assets/image%20%28915%29.png)

```text
김과장 : RAID가 뭐죠?
나박사 : RAID는 여러 개의 디스크를 묶어서 하나의 논리적인 하드디스크로 모아 놓은 집합입니다.
         데이터도 분산되어 저장되는데 RAID의 장점으로 데이터 스토리지의 비용을  줄일 수 
         있습니다. 또한 여러 디스크에 분산 저장 되기 때문에, 성능비가 좋은 하드디스크를 모아 
         대용량 디스크처럼 사용하기 때문에 신뢰성 및 성능을 향상 시킬 수 있습니다.

```

![](../../../../.gitbook/assets/image%20%28890%29.png)

**RAID를 구현하는 방법, 하드웨어적 구현과 소프트웨어적 구현**

**\[하드웨어적인 방법의 특징\]** 

호스트로부터 독립적이며 하나의 디스크 장치로 인식이 되어 컨트롤러를 설치 한 후 컨트롤러에 디스크를 연결해서 사용합니다. 

**&lt;장점&gt;** 시스템 자원을 사용하지 않고 운영체제에 독립적임 

**&lt;단점&gt;** 비용이 많이듬.

**\[소프트웨어 RAID\]**

 소프트웨어 RAID는 시스템 자원을 소모하며 운영체제에 의존적이나 저렴한 비용으로 구현이 가능하다는 장점이 있습니다.



![](../../../../.gitbook/assets/image%20%28895%29.png)

![](../../../../.gitbook/assets/image%20%28885%29.png)

![](../../../../.gitbook/assets/image%20%28922%29.png)



Level3과 4는 구조가 비슷합니다. 하나의 디스크에 패리티 정보를 저장하고 나머지 드라이브에 데이터를 적은 단위로 분산 저장합니다. 3은 데이터를 비트단위로 분산하지만 4는 블록 단위로 분산하고, 따라서 용량이 큰 데이터 저장에는 4가 유리합니다.

![](../../../../.gitbook/assets/image%20%28889%29.png)



Level 5는 3,4의 단점을 보완 한 것으로 패리티 정보를 모든 디스크에 분산하여 저장함으로써 병목현상을 방지하게 됩니다.

![](../../../../.gitbook/assets/image%20%28913%29.png)

## 백업 

![](../../../../.gitbook/assets/image%20%28891%29.png)

![](../../../../.gitbook/assets/image%20%28904%29.png)

![](../../../../.gitbook/assets/image%20%28921%29.png)

백업 방법으로는 크게 **Full Backup** 과 **Incremental Backup** 2가지로 나눌 수 있습니다.

#### 1\) Full Backup 은 말 그대로 하드디스크의 모든 내용을 백업하는 것으로 사용하는 디스크 용량 이상의 백업 미디어 용량이 필요합니다.

#### 2\) Incremental Backup은 최종 백업된 이후에 변경된 파일만 백업하는 것을 말하죠.

### tar을 사용하여 백업하기

####  -cvf 옵션 사용

![](../../../../.gitbook/assets/image%20%28879%29.png)

![](../../../../.gitbook/assets/image%20%28909%29.png)

![](../../../../.gitbook/assets/image%20%28903%29.png)



![](../../../../.gitbook/assets/image%20%28911%29.png)

## 로그 파일 관리 

![](../../../../.gitbook/assets/image%20%28871%29.png)

![](../../../../.gitbook/assets/image%20%28917%29.png)

###  로그파일 개

![](../../../../.gitbook/assets/image%20%28908%29.png)

###  시스템 로그 파일의 이해 

```text


1) messages로그는 메일, 뉴스를 제외한 시스템의 모든 사항을 기록하는데 순서대로 날짜,
         시간, 호스트명, 프로세스명, 설명이 기록되어 있습니다.

2) maillog는 메일 교환이 기록되어 
         어떤 메일이 오고 갔는지 알려주어 메일이 오고 간 ① 시간, ② 호스트, ③ 데몬, ④ 사용자, 
         ⑤ 크기 등을 체크 할 수 있습니다. 

3) secure 로그는 사용자의 사적인 로그인 정보가 
         기록되는데 순서대로 날짜, 시간, 호스트 ,프로세스명, 설명으로 이루어집니다. 

4) boot.log는 시스템에서의 서비스 데몬들의 부트에 관련된 정보가 기록되는 파일입니다. 
         부팅과 shutdown 시의 서비스 데몬의 실행 정보도 기록됩니다. 

5) cron 로그에는 
cron이 실행된 것들에 대한 정보가 기록되며 이를 통해 cron이 제대로 실행되는지 확인 할 수 
있습니다. 

6) dmesg 로그에는 시스템이 부팅 할 때 보이는 정보 메시지들이 기록되며, 
         부팅 시 에러메시지가 나오면 여기서 확인 할 수 있습니다. 

7) lastlog는 사용자가 마지막으로
         로그인한 기록을 보여주는데 다른 로그와 달리 lastlog를 실행함으로써 볼 수 있습니다. 
         ‘-t’ 옵션은 숫자만큼의 최근 기간 동안의 로그인을 보여주며, ‘-u’ 옵션은 특정사용자의 
         마지막 로그인 기록을 보여줍니다. 

8) xferlog는 
FTP를 사용하여 파일을 주고 받았을 경우 그 기록이 남는 로그로서 한줄에 들어가는 이때까지의
 로그에 비하여 많습니다. 날짜와 시간 및, 전송에 걸린시간 ,호스트명, 전송타입, 접속모드 등 
 FTP에 관련된 모든 내용이 들어가있습니다.

```

![](../../../../.gitbook/assets/image%20%28914%29.png)

![](../../../../.gitbook/assets/image%20%28918%29.png)

![](../../../../.gitbook/assets/image%20%28900%29.png)

![](../../../../.gitbook/assets/image%20%28916%29.png)

![](../../../../.gitbook/assets/image%20%28896%29.png)

![](../../../../.gitbook/assets/image%20%28880%29.png)

![](../../../../.gitbook/assets/image%20%28897%29.png)

![](../../../../.gitbook/assets/image%20%28931%29.png)

### syslogd를 이용 로그제어 

![](../../../../.gitbook/assets/image%20%28927%29.png)

![](../../../../.gitbook/assets/image%20%28902%29.png)

## 지름길 보기 

![](../../../../.gitbook/assets/image%20%28928%29.png)

![](../../../../.gitbook/assets/image%20%28878%29.png)

![](../../../../.gitbook/assets/image%20%28906%29.png)



## 탈출하기 

![](../../../../.gitbook/assets/image%20%28870%29.png)

![](../../../../.gitbook/assets/image%20%28883%29.png)

![](../../../../.gitbook/assets/image%20%28919%29.png)

![](../../../../.gitbook/assets/image%20%28893%29.png)

## 다음 목적지

![](../../../../.gitbook/assets/image%20%28910%29.png)

