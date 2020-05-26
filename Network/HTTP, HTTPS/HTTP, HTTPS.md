# HTTP, HTTPS

---

# HTTP란?

HTTP는 HyperText Transfer Protocol의 약자이며, 인터넷(WWW) 상에서 웹 클라이언트와 웹 서버 간 데이터 전송을 위한 규약(Protocol)이다. 애플리케이션 레벨의 프로토콜로 TCP/IP 위에서 작동한다. HTTP 통신을 이용해 HTML 문서, 이미지, 동영상, 오디오, 텍스트 문서 등 대부분의 데이터 형식을 지원한다.

## 작동 방식

[https://docs.google.com/drawings/d/1O6w7drXt5aw6vogI8-PRR7xA5g3ay0UmEy67fenyQ54/pub?w=415&h=162](https://docs.google.com/drawings/d/1O6w7drXt5aw6vogI8-PRR7xA5g3ay0UmEy67fenyQ54/pub?w=415&h=162)

클라이언트는 웹 브라우저 애플리케이션(IE, Firefox, Chrome, Opera 등)로 URI를 이용해 서버에 특정 데이터를 요청할 수 있다.
서버는 클라이언트 요청을 해석하고 클라이언트가 요청한 데이터를 응답 데이터에 실어 보낸다.

## HTTP의 특징

HTTP는 두 가지의 큰 특징이 있다.

- Connectless(비연결성): 단일 요청에 대해서 단일 응답을 돌려주며, 단일 요청을 보내고 단일 응답을 받는 동안에만 연결을 유지한다.
- Stateless(무상태성): HTTP는 비연결성의 특징을 갖기 때문에 서버는 이전 연결에서의 클라이언트 상태를 알 수 없다.

이 특징에는 다음과 같은 장/단점이 있다.

- 장점: **불특정 다수를 대상으로 하는 서비스에 적합하다.** 연결은 서버의 유한한 자원이다. 연결을 항상 유지한다면 누군가 연결을 끊지 않는 이상 서버는 연결이 되지 않은 클라이언트의 요청을 처리할 수 없다. 하지만 HTTP는 항상 연결을 유지하는 것이 아니라 필요할 때만 연결하고 끊기 때문에 최소한의 연결로 다수의 요청을 처리할 수 있어 효율적인 요청 처리가 가능하다는 장점이 있다.
- 단점: 대부분의 웹 서비스는 클라이언트의 이전 상태를 이용하는 서비스가 필요하다. 로그인을 예로 들자면, 사용자가 로그인을 했다는 정보를 참고하여 마이페이지를 조회할 수 있어야 하는데, HTTP의 Stateless 특징 때문에 서버는 클라이언트의 로그인 여부를 알 수 없다. 이를 해결하기 위해 클라이언트 상태 정보를 저장할 수 있는 기술이 있으며, 클라이언트에 저장되는 Cookie와 서버에 저장되는 Session이 있다.

## 요청(Request)과 응답(Response)의 데이터 구조

서버와 클라이언트가 요청과 응답으로 주고받는 데이터를 HTTP 메세지(Message)라고 하며, HTTP Message는 다음과 같은 데이터 구조로 이루어져 있다.

![https://mdn.mozillademos.org/files/13827/HTTPMsgStructure2.png](https://mdn.mozillademos.org/files/13827/HTTPMsgStructure2.png)

- 시작 줄(start-line): 실행되어야 할 요청, 또는 요청 수행에 대한 성공/실패에 대한 정보를 포함한다. 이 줄은 항상 한 줄이다.
- 헤더(Header): 요청에 대한 설명, 혹은 메시지 본문에 대한 메타데이터를 포함한다.
- 빈 줄(blank line): 요청에 대한 모든 메타 정보가 전송되었음을 알리는 역할이다.
- 본문(body): 요청과 관련된 내용(HTML 폼 콘텐츠 등)이 옵션으로 들어가거나, 응답과 관련된 문서(document)를 포함한다. 본문의 존재 유무 및 크기는 첫 줄과 HTTP 헤더에 명시된다.
HTTP 메시지의 시작 줄과 HTTP 헤더를 묶어서 요청 헤드(head)라고 부르며, 이와 반대로 HTTP 메시지의 페이로드는 본문(body)이라고 한다.

### Request Message

- 시작 줄: [HTTP Method] [URL] [HTTP 버전]
ex) `POST localhost/ HTTP 1.1`

    주로 사용되는 HTTP Method의 종류는 다음과 같다.

    - GET : 정보를 요청하기 위해서 사용한다. (SELECT)
    - POST : 정보를 밀어넣기 위해서 사용한다. (INSERT)
    - PUT : 정보를 업데이트하기 위해서 사용한다. (UPDATE)
    - DELETE : 정보를 삭제하기 위해서 사용한다. (DELETE)
    - HEAD : (HTTP)헤더 정보만 요청한다. 해당 자원이 존재하는지 혹은 서버에 문제가 없는지를 확인하기 위해서 사용한다.
    - OPTIONS : 웹서버가 지원하는 메서드의 종류를 요청한다.
    - TRACE : 클라이언트의 요청을 그대로 반환한다. 예컨데 echo 서비스로 서버 상태를 확인하기 위한 목적으로 주로 사용한다.
- 헤더: 다음과 같은 정보를 포함한다.

    ![https://mdn.mozillademos.org/files/13821/HTTP_Request_Headers2.png](https://mdn.mozillademos.org/files/13821/HTTP_Request_Headers2.png)

- 본문: HTTP Method에 따라 옵션으로 포함된다. 요청과 관련된 데이터를 포함한다.

### Response Message

- 시작 줄(상태 줄, Status Line): [프로토콜 버전] [상태 코드] [상태 텍스트]
ex) `HTTP/1.1 404 Not Found.`

    상태 코드의 종류는 크게 다음과 같이 분류된다.

    - 1xx: Informational - 요청 정보 처리 중
    - 2xx: Success - 요청을 정상적으로 처리함
    - 3xx: Redirection - 요청을 완료하기 위해 추가 동작 필요
    - 4xx: Client Error - 서버가 요청을 이해하지 못함
    - 5xx: Server Error - 서버가 요청 처리 실패함
- 헤더: 다음과 같은 정보를 포함한다.

    ![https://mdn.mozillademos.org/files/13823/HTTP_Response_Headers2.png](https://mdn.mozillademos.org/files/13823/HTTP_Response_Headers2.png)

- 본문: 상태 코드에 따라 옵션으로 포함된다. Request Message 에서 요청한 데이터를 포함한다.

# HTTPS의 등장

## HTTP의 문제점

1. HTTP는 평문 통신이기 때문에 도청이 가능하다.
2. 통신 상대를 확인하지 않기 때문에 위장이 가능하다.
3. 완전성을 증명할 수 없기 때문에 변조가 가능하다.

*위 세 가지의 문제점은 암호화하지 않은 다른 프로토콜에서도 공통되는 문제점이다.*

## SSL(Secure Socket Layer)

위와 같은 HTTP의 문제점을 보완하기 위해 `SSL`과 HTTP를 조합하여 사용하는데, 이를 `HTTPS(HTTP Secure)` or `HTTP over SSL`라고 한다.

SSL에는 다음과 같은 보안화 기능을 제공한다.

1. 암호화(Encryption)
2. 디지털 증명서(Digital Certificates)
3. 메세지 다이제스트(Message Digest)

이러한 SSL의 기능들이 HTTP의 문제점을 어떻게 보완하는지 알아보자.

### 1. TCP/IP는 도청 가능한 네트워크이다. → 암호화로 보완

TCP/IP 구조의 통신은 전부 통신 경로 상에서 엿볼 수 있다. 패킷을 수집하는 것만으로 도청할 수 있다. 평문으로 통신을 할 경우 메세지의 의미를 파악할 수 있기 때문에 **암호화하여 통신**해야 한다.

- 보완 방법: 암호화
    1. 통신 자체를 암호화
    `SSL(Secure Socket Layer)` or `TLS(Transport Layer Security)`라는 다른 프로토콜을 조합함으로써 HTTP의 통신 내용을 암호화할 수 있다. 즉, HTTPS를 사용함으로써 도청 문제를 보완할 수 있다.
    2. 콘텐츠를 암호화
    말 그대로 HTTP를 사용해서 운반하는 내용인, HTTP 메세지에 포함되는 콘텐츠만 암호화하는 것이다. 암호화해서 전송하면 받은 측에서는 그 암호를 해독하여 출력하는 처리가 필요하다.

![HTTP%20HTTPS%20b784fe5dbbd94cf18dd9e856d32e1cfb/Untitled.png](HTTP%20HTTPS%20b784fe5dbbd94cf18dd9e856d32e1cfb/Untitled.png)

### 2. 통신 상대를 확인하지 않기 때문에 위장이 가능하다. → 디지털 증명서로 보완

HTTP에 의한 통신에는 상대가 누구인지 확인하는 처리는 없기 때문에 누구든지 요청을 보낼 수 있다. IP 주소나 포트 등에서 그 웹 서버에 액세스 제한이 없는 경우 요청이 오면 상대가 누구든지 임의의 응답을 반환한다. 이러한 특징은 여러 문제점을 유발한다.

1. 클라이언트에서는 요청을 보낸 곳의 웹 서버가 원래 의도한 응답을 보내야 하는 웹 서버인지를 확인할 수 없다.
2. 서버에서는 응답을 반환한 곳의 클라이언트가 원래 의도한 요청을 보낸 클라이언트인지를 확인할 수 없다. 
3. 통신하고 있는 상대가 접근이 허가된 상대인지를 확인할 수 없다.
4. 어디에서 누가 요청을했는지 확인할 수 없다.
5. 의미 없는 요청도 수신한다 → DoS 공격을 방지할 수 없다.

요악하면 *두 호스트가 서로를 신뢰할 방법이 없으며, 그렇기 때문에 의미 없는 데이터 송수신이 이루어질 수도 있고 이를 악용할 여지가 있다*는 것이다.

- 보완 방법: 디지털 증명서
위 암호화 방법으로 언급된 `SSL`로 상대를 확인할 수 있다. `SSL`은 상대를 확인하는 수단으로 **디지털 증명서**를 제공하고 있다. 증명서는 신뢰할 수 잇는 **제3자 기관에 의해** 발행되는 것이기 때문에 서버나 클라이언트가 실재하는 사실을 증명한다. 이 증명서를 이용함으로써 통신 상대가 내가 통신하고자 하는 서버임을 나타내고 이용자는 개인 정보 누설 등의 위험성이 줄어들게 된다. 추가로 클라이언트는 이 증명서로 본인 확인을 하고 웹 사이트 인증에서도 이용할 수 있다는 이점이 있다.

![HTTP%20HTTPS%20b784fe5dbbd94cf18dd9e856d32e1cfb/Untitled%201.png](HTTP%20HTTPS%20b784fe5dbbd94cf18dd9e856d32e1cfb/Untitled%201.png)

### 3. 완전성을 증명할 수 없기 때문에 변조가 가능하다. → 메세지 다이제스트로 보완

여기서 완전성이란 **정보의 정확성**을 의미한다. 서버 또는 클라이언트에서 수신한 내용이 송신 측에서 보낸 내용과 일치한다는 것을 보장할 수 없다. 요청이나 응답이 발신된 후에 상대가 수신하는 사이에 누군가에 의해 변조되더라도 이 사실을 알 수 없다. 이와 같이 공격자가 도중에 요청이나 응답을 빼앗아 변조하는 공격을 중간자 공격(Man-in-the-Middle)이라고 부른다.

- 보완 방법: 메세지 다이제스트(Message Digest)
메세지 다이제스트는 평문을 일정한 길이로 압축하는 기술이다. 압축된 데이터는 `Hash`라고 부른다.
메세지 다이제스트 함수는 다음과 같은 특징을 가진다.
    1. 출력값을 생성하기 위한 키가 없다. 즉, 키 없이 출력값을 생성한다.
    2. 평문의 길이에 상관 없이 항상 동일한 길이의 출력값을 생성한다.
    3. 단방향 암호화이다. 평문에서 해시로 압축은 가능하지만, 해시에서 평문으로 복원은 불가능하다.

    메세지 다이제스트 함수에는 대표적으로 `MD5`, `SHA-1` 등이 있다.

![HTTP%20HTTPS%20b784fe5dbbd94cf18dd9e856d32e1cfb/Untitled%202.png](HTTP%20HTTPS%20b784fe5dbbd94cf18dd9e856d32e1cfb/Untitled%202.png)

### 참조

[SSL 과 HTTPS - 인터넷 보안을 위한 과정](https://real-dongsoo7.tistory.com/110)

[SSL 서버의 역할](https://post.naver.com/viewer/postView.nhn?volumeNo=7851686&memberNo=15488377)

[메시지 다이제스트, MD (1) - 메시지 다이제스트 함수란?](http://blog.naver.com/PostView.nhn?blogId=nttkak&logNo=20130240183&categoryNo=19&viewDate=&currentPage=1&listtype=0](http://blog.naver.com/PostView.nhn?blogId=nttkak&logNo=20130240183&categoryNo=19&viewDate=&currentPage=1&listtype=0))