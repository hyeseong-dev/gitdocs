# Flask-sqlAlchemy

SQLAlchemy 객체 관계형 매퍼는 데이터베이스 테이블을 이용해 사용자가 정의한 파이썬 클래스의 메소드와 각각의 행을 나타내는 인스턴스로 표현된다. 객체와 각 연관된 행들의 모든 변경점들이 자동으로 동기되어 인스턴스에 반영되며, 그와 동시에 사용자가 정의한 클래스와 각 클래스 사이에 정의된 관계에 대해 쿼리할 수 있는 \(Unit of work이라 하는\)시스템을 포함하고 있다.

이 ORM에서 사용하는 SQLAlchemy 표현 언어는 ORM의 구성 방식과도 같다. SQL언어 튜토리얼에서는 직접적인 의견을 배제한 채 데이터베이스들의 초기에 어떻게 구성해 나가야 하는지에 대해 설명하는 반면 ORM은 고수준의, 추상적인 패턴의 사용 방식과 그에 따른 표현 언어를 사용하는 방법을 예로 보여준다.

사용 패턴과 각 표현 언어가 겹쳐지는 동안, 초기와 달리 공통적으로 나타나는 사항에 대해 표면적으로 접근한다. 먼저 사용자가 정의한 도메인 모델서부터 기본적인 저장 모델을 새로 갱신하는 것까지의 모든 과정을 일련의 구조와 데이터로 접근하게 해야한다. 또 다른 접근 방식으로는 문자로 된 스키마와 SQL 표현식이 나타내는 투시도로부터 명쾌하게 구성해, 각 개별적인 데이터베이스를 메시지로 사용할 수 있게 해야 한다.

가장 성공적인 어플리케이션은 각각 독자적인 객체 관계형 매퍼로 구성되야 한다. 특별한 상황에서는, 어플리케이션은 더 특정한 데이터베이스의 상호작용을 필요로 하고 따라서 더 직접적인 표현 언어를 사용할 수 있어야 한다.

\(제 실력이 미천해 깔끔하게 번역이 안되네요. 공통된 부분에만 집중하고 각 데이터베이스의 특징을 몰개성화 하며 단순히 저장공간으로 치부하는 다른 ORM과 달리 SQLAlchemy는 각 데이터베이스의 특징도 잘 살려내 만든 ORM이다

