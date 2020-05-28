---
description: Advanced Package Tool은 Debian 시스템에 포함된 핵심 도구들의 집합체
---

# apt가 뭐에요?

Debian 이 리눅스 배포판 중에서 최고\(사실 상, 최상의 유닉스 버전\)로 손꼽히는 이유의 대부분은 Debian 시스템의 핵심인 자체 패키지 관리에서 기인한다. Debian 의 모든 것 - 응용프로그램, 컴포넌트 등 - 전부 - 은 패키지로 빌드되며 결국 \(설치 유틸리티, 혹은 유저에 의해 직접적으로\) 시스템에 설치된다.

Debian 에는 리눅스 커널에서 시작하여 게임까지 2만 5천개 이상의 소프트웨어 패키지가 존재한다.

**차례**

1. [Apt 란 무엇인가?](https://wiki.debian.org/ko/Apt#Apt_.2Bt4A_.2BuzTFx8d4rAA.3F)
2. [Further Reading](https://wiki.debian.org/ko/Apt#Further_Reading)
3. [패키지 검색이 안될 때](https://wiki.debian.org/ko/Apt#A.2B0yjQpMnA_.2BrIDAycd0_.2BxUi0IA_.2BtUw-)

### Apt 란 무엇인가? <a id="Apt_.2Bt4A_.2BuzTFx8d4rAA.3F"></a>

Apt _\(**A**dvanced **P**ackage **T**ool 의 약어\)_ 는 Debian 시스템에 포함된 핵심 도구들의 집합체이다. Apt 로 다음과 같은 작업들을 처리할 수 있다:

* 응용 프로그램 설치
* 응용 프로그램 삭제
* 응응프로그램을 항상 최신버전으로 유지하기
* 그 이상 작업들...

기본적으로 Apt 는 [패키지](https://wiki.debian.org/Package) 간 의존성 문제에 대한 해법을 제시하고 이에 요구되는 [패키지](https://wiki.debian.org/Package)를 찾아내며, 실질적으로 \(응용 프로그램\) 패키지 설치와 삭제를 담당하는 [dpkg](https://wiki.debian.org/dpkg) 라는 별개의 도구와 함께 동작한다. Apt 는 **매우** 강력하며, 주로 \(콘솔/[가상 터미널](https://wiki.debian.org/terminal)\)을 통해 명령행에서 사용된다. 하지만, 명령행 인터페이스를 거치지 않고도 [GUI/그래픽적인 방법으로](https://en.wikipedia.org/wiki/GUI) 손쉽게 사용할 수 있도록 도와주는 도구들이 많이 존재한다.

현 시점에서 APT 집합체들과 유연하게 사용되어 권장되는 도구로 [aptitude](https://wiki.debian.org/aptitude) 가 있다. APT 도구들은 aptitude 로 처리하기 힘든 특수 관리 액션을 처리할 때, 또는 특히 의존성 문제로 더욱 민감한 상황일 때 사용되는 편이다.

### Further Reading <a id="Further_Reading"></a>

* [AptCLI](https://wiki.debian.org/AptCLI) - 명령행으로 Apt 를 사용하는 방법
* [AptTools](https://wiki.debian.org/ko/AptTools) - 더 많은 apt 도구들과 트릭
* [apt-get](https://wiki.debian.org/apt-get)
* [SecureApt](https://wiki.debian.org/SecureApt)
* [AptConf](https://wiki.debian.org/AptConf)
* [AptPreferences](https://wiki.debian.org/AptPreferences)
* [aptitude](https://wiki.debian.org/ko/Aptitude)

### 패키지 검색이 안될 때 <a id="A.2B0yjQpMnA_.2BrIDAycd0_.2BxUi0IA_.2BtUw-"></a>

현 작업환경에서 원하는 패키지를 찾기 힘들 때에는 [apt-get.org](http://www.apt-get.org/) 에 접속하길 권한다. 여기서 원하는 패키지가 보관된 저장소 위치를 찾아서 당신의 [SourcesList](https://wiki.debian.org/SourcesList) 에 추가하면 된다.

출처 : [https://wiki.debian.org/ko/Apt](https://wiki.debian.org/ko/Apt)

