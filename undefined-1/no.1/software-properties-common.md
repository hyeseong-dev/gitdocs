---
description: 'PPA,'
---

# software-properties-common



## **software-properties-common** 

> As described in **`apt-show software-properties-common`**
>
> > This software provides an abstraction of the used apt repositories. It allows you to easily manage your distribution and independent software **vendor software sources**.
>
> In practice that means it provides some useful scripts for adding and removing **PPA**s:
>
> ```text
> $ dpkg -L software-properties-common | grep 'bin/'
> /usr/bin/add-apt-repository
> /usr/bin/apt-add-repository
> ```
>
> plus the DBUS backends to do the same via the Software and Updates GUI.
>
> Without it, you would need to add and remove repositories \(such as PPAs\) manually by editing `/etc/apt/sources.list` and/or any subsidiary files in `/etc/apt/sources.list.d`

SsS

## PPA\(Personal Package Archive\)

PPA는 Personal Package Archive의 약자이며 개인 패키지 저장소 라고도 불립니다.

유식한 말로는 다음과 같이 정의되어 있네요.

PPA는 런치패드에서 제공하는 우분투의 공식 패키지 저장소에 없는 서드파티 소트웨어를 위한 개인용 소프트웨어 패키지 저장소 이다.

간단히 말하자면, 열성적인 프로그래머 분들이 공식 패키지가 나오기 전에 소프트웨어를 만들어서 개인용 저장소에 올려놓는다!

그렇게 하면 우리는 공식적인 패지키 저장소에 올라오기전에 소프트웨어를 받아서 사용할 수 있겠죠?

우리는 지금 우분투 패키지를 만드는 중이죠?

그렇다면 먄약 내가 우분투 패지키를 만들었다 가정하면, 

내가 만든 우분투 패키지는 어떻게 다른 사람들에게 공개 하고 사용하도록 할 수 있을까요?

정답은 PPA에 내 우분투 패키지를 등록하는 것입니다. 

위에서 PPA는 "런치패드에서 제공하는" 이라고 이야기 했었죠?

아마도 PPA는 '런치패드'라는 것을 이용하는 것 같습니다. 

그렇다면 '런치패드'가 무엇인지 알아야할 필요가 있겠죠?

## 런치패드\(Launchpad\)

런치패드는 유식한말로 다음과 같이 정의되어 있습니다.

사용가자 소프트웨어를 개발할 때 사용하는 '웹사이트' 혹은 "웹 어플리케이션"이다. 특히 자유 소프트웨어를 개발할 때 많이 사용하며, 

캐노니컬이 개발하였다. 원래는 운영체제인 우분투 개발에 사용되었다.

라고 정의 되어 있네요 ^^

여기서 알 수 있는 사실은 런치패드는 웹사이트 라는 것을 알 수 있습니다. 

당연히 들어가 봐야겠지요? 필요하다면 가입도 불사 해야합니다!!

런치패드의 공식 사이트는 다음과 같습니다.

[https://www.launchpad.net/](https://www.launchpad.net/)





sources : [https://askubuntu.com/questions/1000118/what-is-software-properties-common](https://askubuntu.com/questions/1000118/what-is-software-properties-common)

