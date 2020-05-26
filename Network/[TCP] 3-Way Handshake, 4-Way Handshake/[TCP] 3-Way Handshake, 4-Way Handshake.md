# [TCP] 3-Way Handshake, 4-Way Handshake

---

# 연결 성립

[https://t1.daumcdn.net/cfile/tistory/2352F94A58D7287932](https://t1.daumcdn.net/cfile/tistory/2352F94A58D7287932)

1. 클라이언트는 서버에 접속을 요청하는 SYN(M) 패킷을 보낸다.
2. 서버는 클라이언트의 요청인 SYN(M) 요청을 받고 클라이언트에게 요청을 수락한다는 ACK(M+1)와 SYN(N)이 설정된 패킷을 발송한다.
3. 클라이언트는 서버의 수락 응답인 ACK(M+1)과 SYN(N) 패킷을 받고 ACK(N+1) 패킷을 서버로 보내면 연결이 성립된다.

# 연결 해제(Connection Termination)

[https://t1.daumcdn.net/cfile/tistory/2336285058D7288E33](https://t1.daumcdn.net/cfile/tistory/2336285058D7288E33)

1. 클라이언트가 연결을 종료하겠다는 FIN 플래그를 전송한다.
2. 서버는 클라이언트의 FIN 요청을 받고 알겠다는 확인 메세지로 ACK를 보낸다.
    1. 그리고 나서는 데이터를 모두 보낼 때까지 잠깐 기다린다.(TIME_OUT)
3. 서버는 데이터를 모두 보내고 통신이 끝났으면 연결이 종료되었다고 클라이언트에게 FIN 플래그를 전송한다.
4. 클라이언트는 FIN 메세지를 받고 응답(ACK)를 보낸다.
5. 클라이언트의 ACK 메세지를 받은 서버는 소켓 연결을 해제한다.(Socket close)
6. 클라이언트는 아직 서버로부터 받지 못한 데이터가 있을 것을 대비해 일정 시간 동안 세션을 남겨놓고 잉여 패킷을 기다리는 과정을 거친다.(TIME_WAIT)

# TCP Control Flag

![TCP%203%20Way%20Handshake%204%20Way%20Handshake%200151dbef6a684a6ba61d1b6b91b0f1d8/_2020-04-08__5.21.41.png](TCP%203%20Way%20Handshake%204%20Way%20Handshake%200151dbef6a684a6ba61d1b6b91b0f1d8/_2020-04-08__5.21.41.png)

TCP Header의 구조

TCP Header에는 6 bit의 Code Bit라고 하는 TCP 제어 비트(Control Flag)가 있다. Code Bit는 다음과 같은 정보를 나타낸다.

1. URG (Urgent)
    - 긴급 데이터의 유무를 확인하는 플래그(default 0)
    - 거의 사용하지 않는다.
2. ACK (Acknowledgement)
    - 유효한 ACK 번호의 유무를 확인하는 플래그
    - TCP 3-Way Handshake시 최초를 제외한 다른 모든 TCP 패킷은 ACK 플래그가 on으로 설정되어 있다.
3. PSH (Push)
    - 받은 데이터를 즉시 응용 프로그램에 전달할 것을 요구하는 플래그
    - 버퍼링을 사용하면 응답성에 손상 가능성이 있으므로 Telnet에서는 PSH 플래그가 on으로 설정되어 있다.
4. RST (Reset)
    - TCP 연결을 중단, 거부하고 싶은 경우에 설정되는 플래그
    - RST 플래그를 on으로 한 TCP 패킷을 전송함으로써 현재의 TCP 접속을 강제 종료할 수 있다.
5. SYN (Syncronize)
    - 연결을 위해 메세지 수신 측에 연결을 요청하기 위해 사용하는 플래그
    - TCP 3-Way Handshake 시 SYN 플래그가 on으로 설정하여 ACK 번호를 동기화한다.
6. FIN (Finish)
    - TCP 연결을 종료하기 위해 설정되는 플래그
    - 양쪽에서 FIN이 전송되면 TCP 연결은 종료된다.

## ISN (Initial Sequence Number)

초기 Sequence Number를 ISN이라고 하며, 처음 클라이언트에서 SYN 패킷을 보낼 때 Squencce Number에는 난수가 저장된다. 그 이유는 과거와 현재의 연결에서 주고받은 각각의 패킷을 구분하기 위해서다.

Connection을 맺을 때 사용하는 포트는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용된다. 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용하는 가능성이 존재한다. 서버 측에서는 패킷의 SYN을 보고 패킷을 구분하게 되는데, **난수가 아닌 순차적인 값이 전송된다면 이전의 connection으로부터 오는 패킷으로 인식할 수도 있다.** 이런 문제가 발생할 가능성을 줄이기 위해 ISN을 난수로 설정한다.

### 참조 및 출처

[[TCP] 3-way-handshake & 4-way-handshake](https://asfirstalways.tistory.com/356)

[TCP 헤더](https://m.blog.naver.com/PostView.nhn?blogId=koromoon&logNo=120162515063&proxyReferer=https%3A%2F%2Fwww.google.com%2F)