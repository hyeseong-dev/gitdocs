# curl이 뭔가요?\(feat.linux\)

## 정의

한마디로 command line 기반의 웹 요청 도구에요.   
Unix, Linux, Windows등의 주요 OS에서 구동 가능하며 HTTP/HTTPS/FTP/LDAP/SCP/TELNET/SMTP/POP3등 핵심 프로토콜을 지원하기 때문에 유용하게 사용되요.   
DOWNLOAD와 UPLOAD모두 유용하게 사용되요. 

## 옵션 



<table>
  <thead>
    <tr>
      <th style="text-align:left">short</th>
      <th style="text-align:left">long</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
      <th style="text-align:left">&#xBE44;&#xACE0;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">-k</td>
      <td style="text-align:left">--insecure</td>
      <td style="text-align:left">https &#xC0AC;&#xC774;&#xD2B8;&#xB97C; SSL certificate &#xAC80;&#xC99D;&#xC5C6;&#xC774;
        &#xC5F0;&#xACB0;&#xD55C;&#xB2E4;.</td>
      <td style="text-align:left">wget &#xC758; --no-check-certificate &#xACFC; &#xBE44;&#xC2B7;&#xD55C;
        &#xC5ED;&#xD560; &#xC218;&#xD589;</td>
    </tr>
    <tr>
      <td style="text-align:left">-l</td>
      <td style="text-align:left">--head</td>
      <td style="text-align:left">HTTP header &#xB9CC; &#xBCF4;&#xC5EC;&#xC8FC;&#xACE0; content &#xB294;
        &#xD45C;&#xC2DC;&#xD558;&#xC9C0; &#xC54A;&#xB294;&#xB2E4;</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-D</td>
      <td style="text-align:left">--dump-header &lt;file&gt;</td>
      <td style="text-align:left">&lt;file&gt; &#xC5D0; HTTP header &#xB97C; &#xAE30;&#xB85D;&#xD55C;&#xB2E4;.</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-L</td>
      <td style="text-align:left">--location</td>
      <td style="text-align:left">
        <p>&#xC11C;&#xBC84;&#xC5D0;&#xC11C; <a href="http://en.wikipedia.org/wiki/HTTP_301">HTTP 301 </a>&#xC774;&#xB098;
          <a
          href="http://en.wikipedia.org/wiki/HTTP_302">HTTP 302</a>&#xC751;&#xB2F5;&#xC774; &#xC654;&#xC744; &#xACBD;&#xC6B0;
            redirection URL &#xB85C; &#xB530;&#xB77C;&#xAC04;&#xB2E4;.</p>
        <p>--max-redirs &#xB4A4;&#xC5D0; &#xC22B;&#xC790;&#xB85C; redirection &#xC744;
          &#xBA87; &#xBC88; &#xB530;&#xB77C;&#xAC08;&#xC9C0; &#xC9C0;&#xC815;&#xD560;
          &#xC218; &#xC788;&#xB2E4;. &#xAE30;&#xBCF8; &#xAC12;&#xC740; 50&#xC774;&#xB2E4;</p>
      </td>
      <td style="text-align:left">
        <p>curl -v daum.net &#xC744; &#xC2E4;&#xD589;&#xD558;&#xBA74; &#xACB0;&#xACFC;&#xAC12;&#xC73C;&#xB85C;
          &#xB2E4;&#xC74C;&#xACFC; &#xAC19;&#xC774; HTTP 302 &#xAC00; &#xB9AC;&#xD134;&#xB41C;&#xB2E4;.</p>
        <p>&lt; HTTP/1.1 302 Object Moved
          <br />&lt; Location: <a href="http://www.daum.net/">http://www.daum.net/</a>
        </p>
        <p>-L &#xC635;&#xC158;&#xC744; &#xCD94;&#xAC00;&#xD558;&#xBA74; <a href="http://www.daum.net/">www.daum.net</a> &#xC73C;&#xB85C;
          &#xC7AC;&#xC811;&#xC18D;&#xD558;&#xC5EC; &#xACB0;&#xACFC;&#xB97C; &#xBC1B;&#xC544;&#xC624;&#xAC8C;
          &#xB41C;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">-d</td>
      <td style="text-align:left">--data</td>
      <td style="text-align:left">HTTP Post data</td>
      <td style="text-align:left">FORM &#xC744; POST &#xD558;&#xB294; HTTP&#xB098; JSON &#xC73C;&#xB85C;
        &#xB370;&#xC774;&#xD0C0;&#xB97C; &#xC8FC;&#xACE0;&#xBC1B;&#xB294; REST
        &#xAE30;&#xBC18;&#xC758; &#xC6F9;&#xC11C;&#xBE44;&#xC2A4; &#xB514;&#xBC84;&#xAE45;&#xC2DC;
        &#xC720;&#xC6A9;&#xD55C; &#xC635;&#xC158;&#xC774;&#xB2E4;</td>
    </tr>
    <tr>
      <td style="text-align:left">-v</td>
      <td style="text-align:left">--verbose</td>
      <td style="text-align:left">&#xB3D9;&#xC791;&#xD558;&#xBA74;&#xC11C; &#xC790;&#xC138;&#xD55C; &#xC635;&#xC158;&#xC744;
        &#xCD9C;&#xB825;&#xD55C;&#xB2E4;.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-J</td>
      <td style="text-align:left">--remote-header-name</td>
      <td style="text-align:left">&#xC5B4;&#xB5A4; &#xC6F9;&#xC11C;&#xBE44;&#xC2A4;&#xB294; &#xD30C;&#xC77C;
        &#xB2E4;&#xC6B4;&#xB85C;&#xB4DC;&#xC2DC; <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec19.html">Content-Disposition Header</a> &#xB97C;
        &#xD30C;&#xC2F1;&#xD574;&#xC57C; &#xC815;&#xD655;&#xD55C; &#xD30C;&#xC77C;&#xC774;&#xB984;&#xC744;
        &#xC54C; &#xC218; &#xC788;&#xC744; &#xACBD;&#xC6B0;&#xAC00; &#xC788;&#xB2E4;.
        -J &#xC635;&#xC158;&#xC744; &#xC8FC;&#xBA74; &#xD5E4;&#xB354;&#xC5D0; &#xC788;&#xB294;
        &#xD30C;&#xC77C; &#xC774;&#xB984;&#xC73C;&#xB85C; &#xC800;&#xC7A5;&#xD55C;&#xB2E4;.</td>
      <td
      style="text-align:left">curl 7.20 &#xC774;&#xC0C1;&#xBD80;&#xD130; &#xCD94;&#xAC00;&#xB41C; &#xC635;&#xC158;</td>
    </tr>
    <tr>
      <td style="text-align:left">-o</td>
      <td style="text-align:left">--output FILE</td>
      <td style="text-align:left">curl &#xC740; remote &#xC5D0;&#xC11C; &#xBC1B;&#xC544;&#xC628; &#xB370;&#xC774;&#xD0C0;&#xB97C;
        &#xAE30;&#xBCF8;&#xC801;&#xC73C;&#xB85C;&#xB294; &#xCF58;&#xC194;&#xC5D0;
        &#xCD9C;&#xB825;&#xD55C;&#xB2E4;. -o &#xC635;&#xC158; &#xB4A4;&#xC5D0;
        FILE &#xC744; &#xC801;&#xC5B4;&#xC8FC;&#xBA74; &#xD574;&#xB2F9; FILE &#xB85C;
        &#xC800;&#xC7A5;&#xD55C;&#xB2E4;. (download &#xC2DC; &#xC720;&#xC6A9;)</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-O</td>
      <td style="text-align:left">--remote-name</td>
      <td style="text-align:left">file &#xC800;&#xC7A5;&#xC2DC; remote &#xC758; file &#xC774;&#xB984;&#xC73C;&#xB85C;
        &#xC800;&#xC7A5;&#xD55C;&#xB2E4;. -o &#xC635;&#xC158;&#xBCF4;&#xB2E4; &#xD3B8;&#xB9AC;&#xD558;&#xB2E4;.</td>
      <td
      style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">-s</td>
      <td style="text-align:left">--silent</td>
      <td style="text-align:left">&#xC815;&#xC219; &#xBAA8;&#xB4DC;. &#xC9C4;&#xD589; &#xB0B4;&#xC5ED;&#xC774;&#xB098;
        &#xBA54;&#xC2DC;&#xC9C0;&#xB4F1;&#xC744; &#xCD9C;&#xB825;&#xD558;&#xC9C0;
        &#xC54A;&#xB294;&#xB2E4;. -o &#xC635;&#xC158;&#xC73C;&#xB85C; remote data
        &#xB3C4; /dev/null &#xB85C; &#xBCF4;&#xB0B4;&#xBA74; &#xACB0;&#xACFC;&#xBB3C;&#xB3C4;
        &#xCD9C;&#xB825;&#xB418;&#xC9C0; &#xC54A;&#xB294;&#xB2E4;</td>
      <td style="text-align:left">HTTP response code &#xB9CC; &#xAC00;&#xC838;&#xC624;&#xAC70;&#xB098; &#xD560;
        &#xACBD;&#xC6B0; &#xC720;&#xB9AC;</td>
    </tr>
  </tbody>
</table>출처 : [https://www.lesstif.com/software-architect/curl-http-get-post-rest-api-14745703.html\#curl%EC%84%A4%EC%B9%98%EB%B0%8F%EC%82%AC%EC%9A%A9%EB%B2%95-HTTPGET/POST,RESTAPI%EC%97%B0%EA%B3%84%EB%93%B1-%EC%A3%BC%EC%9A%94%EC%98%B5%EC%85%98](https://www.lesstif.com/software-architect/curl-http-get-post-rest-api-14745703.html#curl%EC%84%A4%EC%B9%98%EB%B0%8F%EC%82%AC%EC%9A%A9%EB%B2%95-HTTPGET/POST,RESTAPI%EC%97%B0%EA%B3%84%EB%93%B1-%EC%A3%BC%EC%9A%94%EC%98%B5%EC%85%98)



---

1.HTTP : Hyper Text Transfer Protocol,  **인터넷에서 데이터를 주고받을 수 있는 프로토콜\(규칙\)**  
2. HTTPS :  HTTP over Secure Socket Layer,  HTTPS는 SSL이라는 보안 프로토콜 위에서 동작하는 HTTP에요.  
3. FTP : File Transfer Protocol로 대량의 파일을 네트워크를 통해 주고 받을때 쓰는 파일 전송 전용 서비스   
4. LDAP : Lightweight Directory Access Protocol, 인터넷 기반의 분산 디렉터리 서비스를 제공하는 공개된 프로토콜  
5. SCP :  **SCP 프로토콜**은 [BSD](https://ko.wikipedia.org/wiki/BSD) [RCP 프로토콜](https://ko.wikipedia.org/wiki/Rlogin) 기반의 [통신 프로토콜](https://ko.wikipedia.org/wiki/%ED%86%B5%EC%8B%A0_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)로서[\[2\]](https://ko.wikipedia.org/wiki/%EC%8B%9C%ED%81%90%EC%96%B4_%EC%B9%B4%ED%94%BC#cite_note-2), 네트워크 상의 호스트 간 [파일 전송](https://ko.wikipedia.org/w/index.php?title=%ED%8C%8C%EC%9D%BC_%EC%A0%84%EC%86%A1&action=edit&redlink=1)을 지원  
6. TELNET : 원격 접속 서비스로서 특정 사용자가 네트워크를 통해 다른 컴퓨터에 연결하여 그 컴퓨터에서 제공하는 서비스를 받을 수 있도록 하는 인터넷 표준 프로토콜  
7. SMTP : SMTP\(Simple Mail Transfer Protocol\) 인터넷에서 메일을 주고 받기위한 프로토콜  
8. POP3 : 전자우편을 수신하기 위한 표준 프로토콜, POP3는 인터넷 서버가 사용자를 위해 전자우편을 수신하고 그 내용을 보관하기 위해 사용되는 클라이언트/서버 프로토콜  
9. RCP : remote copy protocol, 사용자에게 네트워크상에 있는 서버나 원격 호스트의 파일 시스템 혹은 파일 시스템으로부터 파일의 복사를 허용하는 프로토콜. 

---



