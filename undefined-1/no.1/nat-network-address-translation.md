---
description: 네트워크 주소 변환
---

# NAT\(Network Address Translation\)

위키백과를 보면 다음과 같이 정의되어 있습니다. 

**네트워크 주소 변환**\(Network Address Translation, 줄여서 **NAT**\)은 컴퓨터 네트워킹에서 쓰이는 용어로서, [IP](http://ko.wikipedia.org/wiki/IP) [패킷](http://ko.wikipedia.org/wiki/%ED%8C%A8%ED%82%B7)의 [TCP](http://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)/[UDP](http://ko.wikipedia.org/wiki/%EC%82%AC%EC%9A%A9%EC%9E%90_%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B7%B8%EB%9E%A8_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C) 포트 숫자와 소스 및 목적지의 [IP 주소](http://ko.wikipedia.org/wiki/IP_%EC%A3%BC%EC%86%8C) 등을 재기록하면서 [라우터](http://ko.wikipedia.org/wiki/%EB%9D%BC%EC%9A%B0%ED%84%B0)를 통해 [네트워크 트래픽](http://ko.wikipedia.org/w/index.php?title=%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC_%ED%8A%B8%EB%9E%98%ED%94%BD&action=edit&redlink=1)을 주고 받는 기술을 말한다. 패킷에 변화가 생기기 때문에 IP나 TCP/UDP의 [체크섬](http://ko.wikipedia.org/wiki/%EC%B2%B4%ED%81%AC%EC%84%AC)\(checksum\)도 다시 계산되어 재기록해야 한다. NAT를 이용하는 이유는 대개 [사설 네트워크](http://ko.wikipedia.org/wiki/%EC%82%AC%EC%84%A4_%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)에 속한 여러 개의 호스트가 하나의 공인 IP 주소를 사용하여 [인터넷](http://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7)에 접속하기 위함이다. 많은 네트워크 관리자들이 NAT를 편리한 기법이라고 보고 널리 사용하고 있다. NAT가 호스트 간의 통신에 있어서 복잡성을 증가시킬 수 있으므로 네트워크 성능에 영향을 줄 수 있는 것은 당연하다.

 \[출처\] [위키피아\(영문\)](http://en.wikipedia.org/wiki/Network_address_translation), [위키피아\(한글\)](http://ko.wikipedia.org/wiki/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC_%EC%A3%BC%EC%86%8C_%EB%B3%80%ED%99%98)

보통 인터넷선으로 부여받은 ip로는 컴퓨터 한대밖에 인터넷이 안됩니다.  여기서 보통 여러대의 컴퓨터로 인터넷을 하려고 사용하는 것이 공유기 입니다. 공유기의 기능은 집으로 들어온 하나의 ip를 여러개의 ip주소로.... 각각의 이름\(주소\)이 다른 ip주소로 배분을 해줍니다. 이 배분해주는 기술을 NAT라고 합니다.

아래는 NAT의 장단점을 기술한 것입니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p><b>Network Address Translation(&#xB124;&#xD2B8;&#xC6CC;&#xD06C; &#xC8FC;&#xC18C; &#xBCC0;&#xD658;)</b>
        </p>
        <p>
          <br />NAT&#xB294; IPv4&#xC758; &#xC8FC;&#xC18C; &#xBD80;&#xC871; &#xBB38;&#xC81C;&#xB97C;
          &#xD574;&#xACB0;&#xD558;&#xAE30; &#xC704;&#xD55C; &#xBC29;&#xBC95;&#xC73C;&#xB85C;&#xC11C;
          &#xACE0;&#xB824;&#xB418;&#xC5C8;&#xC73C;&#xBA70;, &#xC8FC;&#xB85C; &#xBE44;&#xACF5;&#xC778;(&#xC0AC;&#xC124;,
          local) &#xB124;&#xD2B8;&#xC6CC;&#xD06C; &#xC8FC;&#xC18C;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xB294;
          &#xB9DD;&#xC5D0;&#xC11C; &#xC678;&#xBD80;&#xC758; &#xACF5;&#xC778;&#xB9DD;(public,
          &#xC608;&#xB97C; &#xB4E4;&#xBA74; &#xC778;&#xD130;&#xB137;)&#xACFC;&#xC758;
          &#xD1B5;&#xC2E0;&#xC744; &#xC704;&#xD574;&#xC11C; &#xB124;&#xD2B8;&#xC6CC;&#xD06C;
          &#xC8FC;&#xC18C;&#xB97C; &#xBCC0;&#xD658;&#xD558;&#xB294; &#xAC83;&#xC774;&#xB2E4;.
          &#xC989; &#xB0B4;&#xBD80; &#xB9DD;&#xC5D0;&#xC11C;&#xB294; &#xC0AC;&#xC124;
          IP &#xC8FC;&#xC18C;&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xC5EC; &#xD1B5;&#xC2E0;&#xC744;
          &#xD558;&#xACE0;, &#xC678;&#xBD80;&#xB9DD;&#xACFC;&#xC758; &#xD1B5;&#xC2E0;&#xC2DC;&#xC5D0;&#xB294;
          NAT&#xB97C; &#xAC70;&#xCCD0; &#xACF5;&#xC778; IP &#xC8FC;&#xC18C;&#xB85C;
          &#xC790;&#xB3D9; &#xBCC0;&#xD658;&#xD55C;&#xB2E4;. NAT&#xB97C; &#xC0AC;&#xC6A9;&#xD558;&#xBA74;,
          <br
          />
          <br />&#xC7A5;&#xC810;:
          <br />1. &#xACF5;&#xC778; IP &#xC8FC;&#xC18C; 1&#xAC1C;&#xC5D0;, &#xC5EC;&#xB7EC;
          &#xAC1C;&#xC758; &#xBE44;&#xACF5;&#xC778; &#xC8FC;&#xC18C;&#xB97C; &#xB9E4;&#xD551;&#xD560;
          &#xC218; &#xC788;&#xC5B4; &#xBE44;&#xC6A9;&#xC808;&#xAC10; &#xD6A8;&#xACFC;&#xAC00;
          &#xC788;&#xB2E4;.
          <br />2. &#xC0AC;&#xC124; IP &#xC8FC;&#xC18C;&#xB97C; &#xC0AC;&#xC6A9;&#xD568;&#xC73C;&#xB85C;&#xC368;
          &#xC678;&#xBD80;&#xC5D0;&#xC11C; &#xBCFC; &#xB54C; &#xB0B4;&#xBD80;&#xC758;
          &#xB9DD; &#xAD6C;&#xC870;&#xB97C; &#xC54C; &#xC218; &#xC5C6;&#xC5B4; &#xBCF4;&#xC548;
          &#xD6A8;&#xACFC;&#xAC00; &#xC788;&#xB2E4;.
          <br />
          <br />&#xB2E8;&#xC810;:
          <br />&#xC678;&#xBD80;&#xB9DD;&#xACFC;&#xC758; &#xD1B5;&#xC2E0;&#xC2DC; &#xC8FC;&#xC18C;
          &#xBCC0;&#xD658;&#xC744; &#xAC70;&#xCCD0;&#xC57C; &#xD558;&#xBBC0;&#xB85C;
          &#xB290;&#xB824;&#xC9C0;&#xBA70;, &#xC0AC;&#xC6A9;&#xC790;&#xAC00; &#xB9CE;&#xC744;&#xC218;&#xB85D;
          &#xC18D;&#xB3C4; &#xC800;&#xD558;&#xAC00; &#xCEE4;&#xC9C4;&#xB2E4;.
          <br
          />
          <br />&#xC774;&#xB7EC;&#xD55C; NAT &#xAE30;&#xB2A5;&#xC740; &#xBCF4;&#xD1B5;
          &#xB77C;&#xC6B0;&#xD130;&#xB098; &#xBC29;&#xD654;&#xBCBD; &#xB4F1;&#xC5D0;
          &#xC124;&#xCE58;&#xD558;&#xBA70;, &#xB77C;&#xC6B0;&#xD305; &#xC815;&#xCC45;&#xC5D0;
          &#xB530;&#xB77C; &#xC0AC;&#xC124; IP &#xC8FC;&#xC18C;&#xC640; &#xBCC0;&#xD658;&#xB420;
          IP &#xC8FC;&#xC18C;&#xB97C; static&#xD558;&#xAC8C; &#xD639;&#xC740; dynamic&#xD558;&#xAC8C;
          &#xB9E4;&#xD551;&#xD560; &#xC218; &#xC788;&#xC73C;&#xBA70; &#xD14C;&#xC774;&#xBE14;&#xB85C;
          &#xAD00;&#xB9AC;&#xB41C;&#xB2E4;. &#xC2DC;&#xC2A4;&#xCF54; &#xB77C;&#xC6B0;&#xD130;&#xC778;
          &#xACBD;&#xC6B0;,
          <br />
          <br />1. &#xC0AC;&#xC124; IP &#xC8FC;&#xC18C;&#xB97C; &#xC815;&#xC801;&#xC778;
          &#xD558;&#xB098;&#xC758; &#xACF5;&#xC778; IP &#xC8FC;&#xC18C;&#xB85C; &#xB9E4;&#xD551;
          <br
          />2. &#xC0AC;&#xC124; IP &#xC8FC;&#xC18C;&#xB97C; &#xC784;&#xC758;&#xC758;
          &#xACF5;&#xC778; IP &#xC8FC;&#xC18C;&#xB4E4; &#xC911;&#xC5D0;&#xC11C; &#xC5B4;&#xB5A4;
          &#xD558;&#xB098;&#xC640; &#xB9E4;&#xD551;
          <br />3. &#xC0AC;&#xC124; IP &#xC8FC;&#xC18C;&#xC5D0; &#xD2B9;&#xC815; TCP &#xD3EC;&#xD2B8;&#xB97C;
          &#xB354;&#xD55C; &#xAC83;&#xC744; &#xD558;&#xB098;&#xC758; &#xACF5;&#xC778;
          IP &#xC8FC;&#xC18C;&#xB85C; &#xB9E4;&#xD551;
          <br />4. &#xACF5;&#xC778; IP &#xC8FC;&#xC18C;&#xB97C; &#xC0AC;&#xC124; IP &#xC8FC;&#xC18C;
          &#xC911;&#xC758; &#xD558;&#xB098;&#xB85C; (&#xC21C;&#xC11C;&#xB294; &#xB77C;&#xC6B4;&#xB4DC;
          &#xB85C;&#xBE48; &#xBC29;&#xC2DD;&#xC744; &#xC0AC;&#xC6A9;) &#xB9E4;&#xD551;
          &#xD560; &#xC218; &#xC788;&#xB2E4;.
          <br />
        </p>
        <p>[&#xCD9C;&#xCC98;] <a href="http://www.comnetlink.net/bbs2/dict/viewbody.html?code=comnetlink_dic&amp;number=1164&amp;page=2">&#xB124;&#xD06C;&#xC6CC;&#xD06C; &#xC6A9;&#xC5B4;&#xC0AC;&#xC804;</a>
        </p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

