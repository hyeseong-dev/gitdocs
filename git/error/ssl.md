# SSL 인증서 오류

## git 에서 https repository 연결시 SSL 인증서 오류 해결법

### TL;DR[![Link to TL;DR](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-TL;DR) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-TL;DR"></a>

신뢰할 수 있는 사이트라면 아래 명령어로 SSL 인증서 검증을 끄는 게 가장 간편

```text
git config --global http.sslVerify false
```

Copy

또는 shell 의 환경 변수에 GIT\_SSL\_NO\_VERIFY 을 0 으로 설정해도 SSL 검증을 하지 않음.

```text
export GIT_SSL_NO_VERIFY=0
```

Copy

### 개요[![Link to &#xAC1C;&#xC694;](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-%EA%B0%9C%EC%9A%94) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-&#xAC1C;&#xC694;"></a>

git 은 https repository 연결시 curl 을 사용하여 연결하는데 curl 의 SSL 인증서 검증 옵션때문에 오류가 발생하는 경우가 있는데  주요 원인은 아래의  2 가지이다.

### CA 인증서 묶음 파일인 CA bundle 파일이 없거나 경로가 잘못됨[![Link to CA &#xC778;&#xC99D;&#xC11C; &#xBB36;&#xC74C; &#xD30C;&#xC77C;&#xC778; CA bundle &#xD30C;&#xC77C;&#xC774; &#xC5C6;&#xAC70;&#xB098; &#xACBD;&#xB85C;&#xAC00; &#xC798;&#xBABB;&#xB428;](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-CA%EC%9D%B8%EC%A6%9D%EC%84%9C%EB%AC%B6%EC%9D%8C%ED%8C%8C%EC%9D%BC%EC%9D%B8CAbundle%ED%8C%8C%EC%9D%BC%EC%9D%B4%EC%97%86%EA%B1%B0%EB%82%98%EA%B2%BD%EB%A1%9C%EA%B0%80%EC%9E%98%EB%AA%BB%EB%90%A8) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-CA&#xC778;&#xC99D;&#xC11C;&#xBB36;&#xC74C;&#xD30C;&#xC77C;&#xC778;CAbundle&#xD30C;&#xC77C;&#xC774;&#xC5C6;&#xAC70;&#xB098;&#xACBD;&#xB85C;&#xAC00;&#xC798;&#xBABB;&#xB428;"></a>

git 이 사용하는 curl 에 등록된 인증기관 인증서\(ca certificate\) 정보는 다음 명령어로 확인할 수 있다. \(참고 [http://curl.haxx.se/docs/sslcerts.html](http://curl.haxx.se/docs/sslcerts.html)\)

```text
$ git config --global http.sslCAInfo
/bin/curl-ca-bundle.crt
```

Copy

Windows 용 git 의 경우 _http.sslCAInfo_ 이 없을 경우 git 이 설치된 경로에서 ca bundle 파일을 찾게 되는데 이 파일이 없는 경우 아래와 같이 _"error setting certificate verify locations"_ 에러가 발생한다.

```text
$ git clone https://mygit.example.com/lesstif/testprj.git/


fatal: unable to access 'https://mygit.example.com/lesstif/testprj.git/': error setting certificate verify locations:

  CAfile: D:/devel/Git-2.9/mingw64/libexec/ssl/certs/ca-bundle.crt
  CApath: none
```

Copy

이 경우 에러 메시지에 CAfile 경로를 확인후에 없을 경우 설정해 주고 다시 clone 을 실행하면 된다.

```text
$ git config --global http.sslCAInfo d:/devel/my-ca-bundle.crt
```

Copy

### Chain 에 없는 인증서[![Link to Chain &#xC5D0; &#xC5C6;&#xB294; &#xC778;&#xC99D;&#xC11C;](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-Chain%EC%97%90%EC%97%86%EB%8A%94%EC%9D%B8%EC%A6%9D%EC%84%9C) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-Chain&#xC5D0;&#xC5C6;&#xB294;&#xC778;&#xC99D;&#xC11C;"></a>

#### 원인[![Link to &#xC6D0;&#xC778;](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-%EC%9B%90%EC%9D%B8) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-&#xC6D0;&#xC778;"></a>

Verisign, Comodo, Thawte 같이 유명한 CA에서 발급받은 SSL 인증서라면 괜찮지만 self singed certificate 나 모르는 CA 에서 발급한 인증서같이

기본 ca 정보 목록에 없는 인증서를 사용할 경우 에러를 발생시킨다.**셀프 사인 인증서 에러**

fatal: unable to access 'https://myserver/lesstif/util-script.git/': SSL certificate problem: self signed certificate**ca-bundle 에 SSL 발급기관 인증서 정보가 없을 경우**

error: SSL certificate problem, verify that the CA cert is OK. Details:  
error:14090086:SSL routines:SSL3\_GET\_SERVER\_CERTIFICATE:certificate verify failed while accessing https://myhost/username/ExcelANT.git/info/refs git-config 의 해당 항목 보기 Click here to expand...

처리 방법은 다음과 같다.

#### 상용 SSL 인증서 발급[![Link to &#xC0C1;&#xC6A9; SSL &#xC778;&#xC99D;&#xC11C; &#xBC1C;&#xAE09;](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-%EC%83%81%EC%9A%A9SSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EB%B0%9C%EA%B8%89) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-&#xC0C1;&#xC6A9;SSL&#xC778;&#xC99D;&#xC11C;&#xBC1C;&#xAE09;"></a>

1. VeriSign 이나 Comodo, RapidSSL 등 유명한 SSL 인증서 발급 기관에서 돈을 주고 SSL 인증서를 발급받아서 git https 서버에 설치한다.  

**장점**

1. 서버에 적용하므로 git client 마다 설정을 수정할 필요는 없다.

**단점**

1. 돈이 든다. 내부에서만 사용하는 서버라면 굳이 상용 SSL 인증서를 발급받을 필요는 없다고 본다.

#### SSL Verify 옵션 Off[![Link to SSL Verify &#xC635;&#xC158; Off](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-SSLVerify%EC%98%B5%EC%85%98Off) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-SSLVerify&#xC635;&#xC158;Off"></a>

1. git 의 ssl verify 옵션을 끈다. --global 을 주어 전역적으로 설정할 수 있고 

   ```text
   git config --global http.sslVerify false
   ## 또는 다음과 같이 환경 변수로 설정 가능
   export GIT_SSL_NO_VERIFY=0
   ```

   Copy

   특정 repository 에서만 수행하려면 repository 가 있는 폴더에서 다음 명령어를 실행하거나 .git/config 의 \[http\] 섹션에 sslVerify = false를 추가한다.

   ```text
   git config http.sslVerify false
   ```

   Copy

  
   내부적으로는 libcurl 호출시 다음과 같이 SSL 관련 검증을 하지 않게 된다.

   ```text
   static CURL *get_curl_handle(void)
   {
           CURL *result = curl_easy_init();
           if (!curl_ssl_verify) {
                   curl_easy_setopt(result, CURLOPT_SSL_VERIFYPEER, 0);
                   curl_easy_setopt(result, CURLOPT_SSL_VERIFYHOST, 0);
           } else {
                   /* Verify authenticity of the peer's certificate */
                   curl_easy_setopt(result, CURLOPT_SSL_VERIFYPEER, 1);
                   /* The name in the cert must match whom we tried to connect */
                   curl_easy_setopt(result, CURLOPT_SSL_VERIFYHOST, 2);
           }
           ...
   }
   ```

   Copy

**장점**

1. 돈이 안 든다.

**단점**

1. 사용하는 git client 마다 설정을 수정해야 한다.
2. git 을 upgrade 할때마다 설정을 반영해야 할수 있다.

#### curl 의 인증기관 목록에 SSL 인증서 추가[![Link to curl &#xC758; &#xC778;&#xC99D;&#xAE30;&#xAD00; &#xBAA9;&#xB85D;&#xC5D0; SSL &#xC778;&#xC99D;&#xC11C; &#xCD94;&#xAC00;](https://www.lesstif.com/gitbook/_/AC1F142D0171445D13DC476E4B36792B/1603982570002/images/common/link-solid.svg)](https://www.lesstif.com/gitbook/git-https-repository-ssl-14090808.html#git%EC%97%90%EC%84%9Chttpsrepository%EC%97%B0%EA%B2%B0%EC%8B%9CSSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%98%A4%EB%A5%98%ED%95%B4%EA%B2%B0%EB%B2%95-curl%EC%9D%98%EC%9D%B8%EC%A6%9D%EA%B8%B0%EA%B4%80%EB%AA%A9%EB%A1%9D%EC%97%90SSL%EC%9D%B8%EC%A6%9D%EC%84%9C%EC%B6%94%EA%B0%80) <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-curl&#xC758;&#xC778;&#xC99D;&#xAE30;&#xAD00;&#xBAA9;&#xB85D;&#xC5D0;SSL&#xC778;&#xC99D;&#xC11C;&#xCD94;&#xAC00;"></a>

curl이 사용하는 인증기관 인증서 목록에 ca-bundle.crt 에 사용하는 인증서를 추가한다. \(참고 [curl 에 신뢰하는 인증기관 인증서\(CA Cert\) 추가하기](https://www.lesstif.com/gitbook/curl-ca-cert-15892500.html)\)

**장점**

1. 돈이 안 든다.

**단점**

1. 사용하는 git client 마다 설정을 수정해야 한다.
2. git 을 upgrade 할때마다 설정을 반영해야 할수 있다.
3. SSL Verify off 보다 번거롭다.

### See Also <a id="git&#xC5D0;&#xC11C;httpsrepository&#xC5F0;&#xACB0;&#xC2DC;SSL&#xC778;&#xC99D;&#xC11C;&#xC624;&#xB958;&#xD574;&#xACB0;&#xBC95;-SeeAlso"></a>

