# 인터넷작동

## 인터넷 어떻게 작동하는대요?

### 요약

인터넷은 모두\(모든 인간들이\) 함께 통신하는 대규모 컴퓨터 네트워크이에요.

모질라웹에서는 인터넷의 역사는 모호하다라고 서두를 시작하지만 일반적으로 1960년대 미국 군대가 연구 프로젝트를 하면서 시작했다고 하네요. 그리고 1980년대에 대학과 사기업의 지원으로 공공 인프라로 발전했다고 해요.

결국 인터넷은 컴퓨터를 모두 함께 연결하고 어떤 일이 있어도 연결 상태를 유지하고 그 방법을 찾는 거라고 보면 되요.  
걍, 모든 사람을 이어주는 물건이라고 보면 되요.

### 추가 학습

[How the Internet Works in 5 Minutes](https://www.youtube.com/watch?v=7_LPdttKXPc)  
5분만에 잛게 설명한 인터넷 작동 원리 유투브 영상이에요.

[How does the INTERNET work? \| ICT \#2](https://www.youtube.com/watch?v=x3c1ih2NJEg) 이건 8분짜리

### 심화 학습

**simple network**

컴퓨터 2대가 통신하는 경우 물리적\(일반적으로 Ethernet cable 사용\) 또는 무선\(Wifi or Bluetooth\)으로 연결해요.  
모든 최신 컴퓨터는 이러한 연결을 하게되조.

![&#xCEF4;&#xD4E8;&#xD130; 2&#xB300; &#xC5F0;&#xACB0; &#xBAA8;&#xC2B5;](https://mdn.mozillademos.org/files/8441/internet-schema-1.png)

위의 두대만 연결 된게 아니라 만약 10대의 컴퓨터가 연결되면 아래와 같을거에요.  
9개의 플러그가 있는 45개의 케이블이 필요한것 처럼 말이지요.

![10&#xB300;&#xC758; &#xCEF4;&#xD4E8;&#xD130; 9&#xAC1C;&#xC758; &#xD50C;&#xB7EC;&#xADF8; 45&#xAC1C;&#xC758; &#xCF00;&#xC774;&#xBE14;](https://mdn.mozillademos.org/files/8443/internet-schema-2.png)  
딱! 봐도 케이블 낭비가 엄청 심하겠조? 결국 **라우터**가 이때 필요한거에요.  
10대의 컴퓨터와 10개의 플러그 10개의 케이블만 있으면 되거든요.

![10&#xB300;&#xC758; &#xCEF4;&#xD4E8;&#xD130;&#xC640; 10&#xAC1C;&#xC758; &#xD50C;&#xB7EC;&#xADF8; 10&#xAC1C;&#xC758; &#xCF00;&#xC774;&#xBE14;&#xB9CC;](https://mdn.mozillademos.org/files/8445/internet-schema-3.png)

**A netwrok of network**

만약 100대, 1000대, 10억대의 컴퓨터를 연결한다면요? 라우터 한대로는 못하겠조. 아래 추가 개념을 살펴 봅시다.  
일단 아래 그림의 라우터 두대를 연결하는 과정을 살펴 봐요.

![&#xB77C;&#xC6B0;&#xD130; &#xB450;&#xB300; &#xC5F0;&#xACB0;](https://mdn.mozillademos.org/files/8447/internet-schema-4.png)

다음 컴퓨터와 라우터, 라우터와 라우터를 연결하면 무한히 그 범위를 확장 할 수 있어요.

![&#xCEF4;&#xD4E8;&#xD130;&#xC640; &#xB2E4;&#xC218;&#xC758; &#xB77C;&#xC6B0;&#xD130;&#xAC04; &#xC5F0;&#xACB0;](https://mdn.mozillademos.org/files/8449/internet-schema-5.png)

위의 그림이 결국 우리가 소위 부르는 인터넷 연결과 매우 밀접한거에요.  
사실 집에 전화선이 일반적인 경우에는 모두 깔려져있습니다. 전화 인프라는 이미 전 세계의 거의 모든 사람과 집을 연결하니 인터넷 네트워크망을 구성하는 최적의 환경이 될수 있어요.  
어떻게 활용할까요? 바로 **모뎀**이라는 특수한 장비가 필요합니다.\(지금은 모뎀 안쓰조?\)  
이 모뎀 네트워크의 정보를 전화 인프라에서 관리 할 수 있는 정보로 바꾸고 그 반대도 마찬가지에요.

![&#xB77C;&#xC6B0;&#xD130;&#xC640; &#xBAA8;&#xB380; &#xC5F0;&#xACB0;](https://mdn.mozillademos.org/files/8451/internet-schema-6.png)

자 이제 전화 인프라에 연결되어 있어요. 다음 단계는 네트워크에 도달하려는 네트워크 메시지를 보내는거에요. 이를 위해 네트워크를 ISP\(Internet Service Provider\)에 연결하는거에요. ISP는 서로 연결된 일부 특수 라우터를 관리하고 다른 ISP의 라우터에도 액세스 할 수 있는 **회사**에요. 따라서 네트워크의 메시지는 ISP네트워크를 통해 다시 다른 네트워크로 전달되요.  
아래 그림을 보면 한눈에 전체 네트워크를 이해 하기 쉬워요.

![ISP&#xC640; &#xB2E4;&#xB978; ISP&#xAC04;&#xC758; &#xC5F0;&#xACB0;&#xACFC; &#xC804;&#xCCB4; &#xB124;&#xD2B8;&#xC6CC;&#xD06C; &#xADF8;&#xB9BC;](https://mdn.mozillademos.org/files/8453/internet-schema-7.png)

**컴퓨터 찾기**

수십억대의 컴퓨터가 있는대, 그놈이 그놈인대 어떻게 찾을까요? 사실 모든 컴퓨터에는 **IP**주소라는\(Internet Protocol\)이라는 주소가 있어요. 마치 우리집 주소에 고유 우편번호가 있는것처럼 말이지요. 주로 IPV4라는 주소가 있는데 4자리로 구성되어 있어요. \(예, 192.168.2.10\)

컴퓨터는 이런 IPV4주소를 완벽하게 읽지만 인간은 이런 다수의 숫자를 외우고 수십개의 IP를 외워서 웹사이트에 접속하는것에 한계가 있어요. 그래서 우리는 **도메인** 주소라는 개념을 도입한거에요. DNS\(Domain Netwrok Server\) 예를들어 구글 들어가는데 일반적인 경우 google.com이라고 치면 바로 딱!나오조. 하지만 IP주소로는 216.58.197.174라고 주소창에 쓰는 경우는 매우 드물어요.

![ip-ip](https://mdn.mozillademos.org/files/8405/dns-ip.png)

