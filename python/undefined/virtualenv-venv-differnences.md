# virtualenv, venv differnences



### 1 개요

virtualenv, venv

* "가상 환경\(virtual environment\)"
* 독립된 파이썬 환경을 생성하는 도구
* 의존성과 버전 문제 차이로 인한 어플리케이션간 충돌 문제 해결 가능
* 파이썬과 원하는 모듈만 담아 운용하는 독립된 공간 정도로 생각하면 됨
* venv는 python3에 기본 내장되어 있기 때문에 python3라면 virtualenv대신 venv를 사용하면 됨

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xB3C4;&#xAD6C;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">virtualenv</td>
      <td style="text-align:left">
        <ul>
          <li>2017&#xB144; &#xD604;&#xC7AC;, &#xAC00;&#xC7A5; &#xB110;&#xB9AC; &#xC0AC;&#xC6A9;&#xB418;&#xACE0;
            &#xC788;&#xB294; Python &#xAC00;&#xC0C1;&#xD658;&#xACBD; &#xB3C4;&#xAD6C;</li>
          <li>Python 2.6&#xBD80;&#xD130; &#xD604;&#xC7AC;&#xAE4C;&#xC9C0; &#xACC4;&#xC18D;
            &#xC0AC;&#xC6A9;&#xB418;&#xACE0; &#xC788;&#xC74C;</li>
          <li><a href="https://zetawiki.com/wiki/PyPI">PyPI</a>&#xB85C; &#xC124;&#xCE58;
            &#xAC00;&#xB2A5;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">venv</td>
      <td style="text-align:left">
        <ul>
          <li>Python 3.4&#xBD80;&#xD130; &#xD45C;&#xC900;&#xBC30;&#xD3EC;&#xD310;&#xC5D0;
            &#xD0D1;&#xC7AC;&#xB428;</li>
          <li>&#xB530;&#xB85C; &#xC124;&#xCE58;&#xD560; &#xD544;&#xC694;&#xAC00; &#xC5C6;&#xC74C;</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

### 2 필요한 상황

* django의 1.8 버전과 1.9 버전을 둘 다 동시에 써보고 싶다.
* 그렇지만, 하나의 Python 환경에서는 동일한 라이브러리의 여러 버전을 쓸 수 없다.
* 즉, django 1.8를 사용하려면 django 1.9를 삭제하고 django 1.9를 사용하려면 django 1.8을 삭제해야 한다.
* 이런 경우에 virtualenv를 이용하여 각각 라이브러리에 대해 독립 공간을 만들어 사용할 수 있다.

### 3 같이 보기

* [virtualenv 사용법](https://zetawiki.com/wiki/Virtualenv_%EC%82%AC%EC%9A%A9%EB%B2%95)
* [venv 사용법](https://zetawiki.com/wiki/Venv_%EC%82%AC%EC%9A%A9%EB%B2%95)
* [PyPI 주요 모듈](https://zetawiki.com/wiki/PyPI_%EC%A3%BC%EC%9A%94_%EB%AA%A8%EB%93%88)
* [tox](https://zetawiki.com/wiki/Tox)

### 4 참고

* [http://sourabhbajaj.com/mac-setup/Python/virtualenv.html](http://sourabhbajaj.com/mac-setup/Python/virtualenv.html)
* [https://virtualenv.pypa.io/en/stable/](https://virtualenv.pypa.io/en/stable/)
* [http://docs.python-guide.org/en/latest/dev/virtualenvs/](http://docs.python-guide.org/en/latest/dev/virtualenvs/)
* [http://masnun.com/2016/04/10/python-pyenv-pyvenv-virtualenv-whats-the-difference.html](http://masnun.com/2016/04/10/python-pyenv-pyvenv-virtualenv-whats-the-difference.html)



