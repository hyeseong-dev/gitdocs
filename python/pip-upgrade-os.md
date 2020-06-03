# pip upgrade os별 방법



Python 모듈 설치시 기본적으로 pip 파이썬 패키지를 사용하는데 **이를 필수적으로 업그레이드해야하는 경우가 많습니다**. **pip에 대하여 업그레이드를 수행하지 않으면 필요한 모듈에 문제가 생길 수 있으니** 가급적 python, pip install 후 반드시 pip를 최신으로 업그레이드하세요. 아래는 pip를 최신 버전으로 업그레이드 하는 방법입니다.

​\# Linux에서 pip 최신버전 업데이트 방법

먼저 리눅스 환경에서의 업데이트 방법입니다. 쉘 화면에서 아래의 커맨드를 입력합니다. pip가 pip를 업그레이드한다니 조금 이상해보일 수도 있지만 정상 동작합니다.

| $ pip install --upgrade pip |
| :--- |


​

위 커맨드가 정상동작할 경우 아래와 같이 메시지가 나타납니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>$ pip install --upgrade pip</p>
        <p>&#x200B;</p>
        <p>Installing collected packages: pip</p>
        <p>Found existing installation: pip x.x.x</p>
        <p>Uninstalling pip:</p>
        <p>Successfully uninstalled pip</p>
        <p>Successfully installed pip</p>
        <p>Cleaning up...</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

​

코드를 보면 삭제 후 재인스톨을 수행하는군요. 이제 업데이트가 완료되었는지 버전을 확인합니다. pip -V 또는 pip --version 명령어로 확인할 수 있습니다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">
        <p>$ pip --version</p>
        <p>&#x200B;</p>
        <p>pip 18.1 from /home/webisfree/lib/python3.5/site-package/pip (python 3.5)</p>
      </th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

​

다음은 윈도우 버전의 경우 방법입니다.

​

​



| \# for Windows, pip 최신버전 업그레이드 |
| :--- |


이번에는 윈도우즈에서 pip 업그레이드 방법입니다. 아래 커맨드를 입력하세요.

| python -m pip install --upgrade pip |
| :--- |


​

앞에서 언급했듯이 pip 패키지가 최신이어야 설치 가능한 모듈이 정상적으로 동작합니다.

​

​

**! 위 방법으로 해결되지 않는 경우**

sudo 명령어 추가하여 실행해보세요. 만약 **root 권한이 없는 경우 install되지 않을 수 있으니** sudo를 앞에 추가해서 다시 시도해봅니다.

​

​

**! 이미 최신 패키지 버전인 경우**

| Requirement already up-to-date: ... |
| :--- |


​

위와 같이 출력되는 경우 이미 최신으로 업그레이드 되었다는 부분입니다. 최신 버전이므로 그대로 사용하셔도 되겠습니다. 여기까지 pip 파이썬 패키지 업데이트, 업그레이드 방법이었습니다.



출처: [https://webisfree.com/2017-08-10/python-패키지-pip-업그레이드-upgrade-방법](https://webisfree.com/2017-08-10/python-%ED%8C%A8%ED%82%A4%EC%A7%80-pip-%EC%97%85%EA%B7%B8%EB%A0%88%EC%9D%B4%EB%93%9C-upgrade-%EB%B0%A9%EB%B2%95)

