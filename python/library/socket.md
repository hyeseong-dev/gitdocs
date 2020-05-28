---
description: 파이썬 라이브러리
---

# Socket 모듈

네트워크 프로그래밍 분야에서 소켓은 연결된 네트워크의 양 끝단을 추상화 시킨 개념이며, 컴퓨터의 관점에서는 네트워크로 통하는 컴퓨터의 외부와 컴퓨터 내부의 프로그램을 이어주는 인터페이스에요.

 소켓의 개념에 대해서 이 글에서 모두 소상히 설명할 수는 없고, 네트워크를 통해서 바이트스트림을 주고 받을 수 있는 창구라 보면 되요. 다만 단순히 프로그램의 내부와 외부를 잇는 표준 입출력과는 달리 소켓은 네트워크의 반대편이 어디인지에 대한 정보를 가지고 있어요. 

즉 우리가 택배를 보낼 때 박스에 물건을 넣고 받는 사람 주소를 쓰는 것과 비슷하게 소켓은 어디로 보내지는 창구라는 것이 명시된 택배 상자 같은 것이에요.

 파이썬의 `socket` 모듈은 소켓 프로그래밍에 필요한 시스템 콜을 래핑하는 API를 제공하는 모듈이다.  소켓 통신을 위해서 물론 소켓을 생성해서 사용하는데, 서버와 클라이언트일 때가 조금 다르다.

## 소켓을 생성하기 

 `socket.socket()` 함수를 이용해서 소켓 객체를 생성할 수 있다. 서버든 클라이언트등 동일하게 소켓을 이용한 네트워킹을 하기 위해서는 소켓을 먼저 생성할 필요가 있다. 이 함수는 두 가지 인자를 받는데, 하나는 **패밀리**이고 다른 하나는 **타입**이다.

1. **패밀리** : 첫번째 인자는 패밀리에요 소켓의 패밀리란, '**택배 상자에 쓰는 주소 체계가 어떻게 되어 있는냐**'에 관한 것으로 흔히 AF\_INET이나 AF\_INET6를 많이 쓴다. 전자는 IP4v에 후자는 IP6v에 사용된다고해요. 
2. 타입 : 소켓 타입이에요. raw소켓, 스트림 소켓, 데이터그램 소켓등이 있는데 , 보통 많이 쓰는것은 socket.SOCK\_STREAM 혹은 socket.SOCK\_DGRAM이에요. 

 가장 흔히 쓰이는 socket.AF\_INET, socket.SOCK\_STREAM 조합은 사실 socket.socket\(\)의 인자 중에서 family=, type= 에 대한 기본 인자 값이에요.   
 따라서 이 타입의 소켓을 생성하고자 하는 경우에는 많은 파이썬 소켓 관련 튜토리얼과 달리, 인자를 생략하고 `socket.socket()`만 써도 무방해요. 

이렇게 생성한 소켓을 통해 데이터를 주고 받기 위해서는 소켓을 포트에 맵핑하고 상대측 포트에 연결하는 과정이 필요해요. 이 과정은 서버 측과 클라이언트 측의 구성 방식이 약간 달라요. 먼저 서버쪽의 구성방법을 살펴볼게요. 

### 바인드와 리스닝 

 소켓통신에서 **서버**는 **보통 최초의 수신자**가 되는 **노드**를 의미해요. 따라서 서버는 소켓을 만들고 포트에 맵핑한 다음, 클라이언트가 접속하기를 기다리게 되요. **서버가 소켓을 포트에 맵핑하는 행위를 바인딩**이라 하며, 이는 생성된 소켓 객체에 대해서 `sock.bind()` 메소드를 호출해요. `bind()` 호출 시에는 호스트이름과 포트번호를 튜플로 감싸서 전달해요.

바인드는 프로그램 인터페이스인 소켓과 네트워크 자원인 포트를 연결하는 행위에요. 따라서 프로그래머는 자신이 사용하는 포트가 명시적으로 몇 번인지, 자신의 IP가 무엇인지 알고 있어야해요. \(알고 있다는 말은 즉 자신이 능동적으로 할당 해준다는 말이에요.\)

```text
sock = socket.socket()
host = 'localhost'
port = 7777 
sock.bind((host, port))
```

바인드 완료된 후 수행해야 하는 동작은 **리스닝**이에요.  이는  소켓에  대해 listen\(\)메소드를 호출하여 수행되요. 이 메소드는 클라이언트가 바인드된 포트로 연결을 할 때까지 기다리는 블럭킹 함수에요.  클라이언트로부터 연결 요청이 들어오면 리턴하게 되는데, 따라서 이  코드의 다음 행에는 해당 연결을 받아들이기 위한 accept\(\) 메소드를 호출하는 부분이 주로 오게되요. 

 accept\(\)는 \(소켓, 주소정보\)로 구성되는 튜플을 리턴한다. 이때의 소켓은 처음에 생성한 소켓과는 별개의 객체로 클라이언트와 연결이 구성되어 실제로 데이터를 주고 받을 수 있는 창구가 된다. 이 소켓은 연결이 들어와서 listen\(\), accept\(\) 가 호출될 때마다 생성될 수 있기 때문에 만약, 연결이 구성된 소켓을 멀티스레드로 처리한다면 1:N의 연결도 처리할 수 있다.

#### 정보 주고 받기

소켓으로부터 데이터를 읽을 때는 `sock.recv()`를, 정보를 보낼 때는 `sock.sendall()`을 사용한다. 데이터를 읽어들일 때에는 버퍼의 크기를 전달해야 한다. `sock.recv(bufsize)`는 최대 bufsize 바이트만큼의 데이터를 읽어온다. 만약 읽어들일 데이터가 아예 없다면 상대방이 데이터를 보내줄때까지 대기한다.

읽어들인 데이터는 bytes 타입의 바이트 시퀀스이며, 데이터를 보낼때에도 바이트시퀀스를 보내야 한다. 만약 문자열을 주고 받고 싶다면 해당 문자열을 인코딩/디코딩해서 전달해야 한다.

 `sendall()`이 아닌 `send()` 메소드도 있다. 이 메소드는 `sendall()`과는 달리 리턴값이 있는데, 바로 실제 전송된 바이트 수를 리턴한다. 따라서 보내려는 데이터와 실제 보내진 데이터가 다를 수 있다는 의미이며, 보내지 못한 데이터를 보낼 책임은 프로그래머에게 있다. \([https://docs.python.org/3/library/socket.html\#socket.socket.send](https://docs.python.org/3/library/socket.html#socket.socket.send)\)

#### 닫기

소켓 역시 외부 리소스를 열어서 사용하는 것이므로 닫는 것이 매우 중요하다. 연결을 종료할 때에는 서버와 클라이언트 모두 소켓을 닫아야 하며, 이미 닫혀있는 소켓에서 데이터를 받으려하거나 데이터를 보내려하는 동작은 모두 에러가 된다. 소켓을 닫을 때에는 `sock.close()` 메소드를 사용한다. 참고로 소켓 객체는 컨텍스트 매니저 프로토콜을 지원하므로 with 구문과 함께 사용하면 안전하게 닫히는 것을 보장할 수 있다.

#### 클라이언트가 서버에 연결하기 – connect

클라이언트가 서버와 통신하는 방법도 거의 비슷하다, 다만 한가지 차이점이 있다면 클라이언트는 바인드나 리스닝의 과정이 필요없다는 것이다. 클라이언트는 능동적으로 서버에 연결하며, 연결된 소켓으로 항상 1:1로 서버와 통신하기 때문이다. \(물론 이것은 클라이언트의 입장이다. 결국 서버가 바인딩이 필요한 이유는 같은 포트로 여러 클라이언트와 동시에 접속될 수 있기 때문이다.\)

 연결은 `sock.connect()`를 사용하며 이 때 사용하는 인자는 `bind()`와 동일하다. 이 메소드는 연결이 수립되면 리턴하며, 이때 리턴값은 존재하지 않는다. 따라서 클라이언트는 최초 생성한 소켓을 통신에 사용하면 된다.

#### 예제 – 간단한 에코서버

간단하게 전달받은 메시지를 출력하고 다시 그대로 클라이언트에게 돌려보내는 에코서버를 구현해보자.



```text
'''echo_server1.py'''

import socket

def run_server(host="127.0.0.1", port=4000):
  with socket.socket() as s:
    s.bind((host, port))
    s.listen(1)
    conn, addr = s.accept()
    msg = conn.recv(1024)
    print(f'{msg.decode()}')
    conn.sendall(msg)
    conn.close()

if __name__ == '__main__':
  run_server()
```

이어서 클라이언트 코드. 클라이언트는 connect 하나면 되기 때문에 간단하다.

```text
'''echo_client1.py'''
import socket

def run(host='127.0.0.1', port=4000):
  with socket.socket() as s:
    s.connect((host, port))
    line = input('>')
    s.sendall(line.encode())
    res = s.recv(1024)
    print(f'={resp.decode()}')

if __name__ == '__main__':
  run()
```

서버를 실행해놓고 다른 터미널창에서 클라이언트를 실행한 후, 클라이언트 쪽에서 키보드로 문자열을 입력하면 다시 출력되고 양쪽 프로그램이 종료된다.

이 때, 중요한 것은 클라이언트가 먼저 실행이 되면 안된다는 것이다. `connect()` 메소드는 리스닝 중인 포트에 연결되어야 하며, 해당 포트가 연결될 준비가 되지 않았다면 예외를 일으킨다.

#### 예제 – 반복적으로 통신하는 에코서버/클라이언트

처음의 코드를 간단히 변형하여 반복적으로 메시지를 주고 받는 에코서버/클라이언트를 만들어보자. 연결이 생성된 후에 while 루프를 돌면서 종료 메시지를 받을 때까지 수신과 송신을 반복하면 된다.

```text
'''simple echo server'''
import socket

def run_server(host='127.0.0.1', port=7788):
    BUF_SIZE = 1024
    with socket.socket() as sock:
        sock.bind((host, port))
        sock.listen()
        conn, addr = sock.accept()
        while True:
            data = conn.recv(BUF_SIZE)
            msg = data.decode()
            print(data.decode())
            conn.sendall(data)
            if msg == 'bye':
                conn.close()
                break

if __name__ == '__main__':
    run_server()
```

클라이언트도 마찬가지로 연결을 만든 다음 while 루프를 돈다. 입력된 내용이 종료메시지라면 메시지를 보내고\(서버가 종료시점을 알아야하므로\) 연결을 닫고 루프를 끝낸다.

```text
import socket

def run_client(host='127.0.0.1', port=7788):
    with socket.socket() as sock:
        sock.connect((host, port))
        for _ in range(10):
            data = input(">>")
            sock.sendall(data.encode())
            if data == 'bye':
                sock.close()
                break
            res = sock.recv(1024)
            print(res.decode())

if __name__ == '__main__':
    run_client()
```

#### 예제 – 다중 접속 에코 서버

앞서 서버에서는 생성한 소켓을 바인드하고, 이후 접속을 받아들이는 시점에 새로운 소켓 객체가 생성된다고 했다. 이전까지의 예제에서는 연결이 만들어진 이후의 통신을 루프를 돌면서 처리했는데, 이 때 통신을 처리하는 코드를 별도의 스레드에서 실행하도록 할 수 있다면, 메인 스레드는 다시 새로운 연결을 받아들일 준비를 하게 된다.

다음 소스는 여러 클라이언트를 받아들여서 동시에 처리할 수 있는 에코서버의 구현이다. 스레드처리에는 threading.Thread를 사용했다.

```text
'''server3.py : multi echo server'''

import socket
from threading import Thread

def echo_handler(conn, addr, terminator="bye"):
    '''개별 연결에 대해 에코잉을 처리하는 핸들러'''
    BUF_SIZE = 1024
    while True:
        data = conn.recv(BUF_SIZE)
        msg = data.decode()
        print('RECEIVED: {} << {}'.format(msg, addr))
        conn.sendall(data)
        if msg == terminator:
            conn.close()
            break

def run_server(host='127.0.0.1', port=7788):
    with socket.socket() as sock:
        sock.bind((host, port))
        while True:
            sock.listen(3)
            conn, addr = sock.accept()
            # 새 연결이 생성되면 새 스레드에서 에코잉을 처리하게 한다.
            t = Thread(target=echo_handler, args=(conn, addr))
            t.start()
        sock.close()

    if __name__ == '__main__':
        run_server()
```

물론 이 코드는 그저 컨셉을 구현한 수준이며, 접속이 많아지는대로 스레드를 늘릴 수는 없으니 별도의 관리가 필요할 것이다. 대략 기본적인 소켓 사용은 이렇게 하는 것이라하는 정도만 알면 되겠다.

