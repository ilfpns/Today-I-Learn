# Web Socket

**→ 두 프로그램 간의 메시지 교환을 위한 방식중 하나이다**

- 현재 인터넷 환경에서 많이 사용된다
- 웹 소켓을 지원하는 브라우저의 경우 웹 소켓 프로토콜을 지원
- W3C와 IETF에 의해 자리잡은 표준 프로토콜이다

# 웹 소켓 특징

**→ 양방향 통신**

- 클라이언트와 서버가 원할 때 데이터를 주고받을 수 있다
- 통상적인 HTTP 방식의 경우 클라이언트가 요청을 보낼 경우에만 서버가 응답을 단방향 통신

→ 실시간 통신

- 웹 환경에서 연속된 데이터를 빠르게 노출
- 채팅, 주식, 비디오

# 웹 소켓 이전의 비슷한 프로토콜

**→ 실시간 네트워킹을 하며 양방향 통신을 지원하는 프로토콜** 

### 폴링 (Polling)

→ 서버로 일정 주기로 요청 송신

# 웹 소켓 동작 방식

→ 웹 소켓 역시 핸드 쉐이킹이 필요하며, Socket 프로토콜이 아닌 HTTP, HTTPS 프로토콜을 통해 이뤄진다

<img width="1162" height="840" alt="image" src="https://github.com/user-attachments/assets/8c7e3b9b-4117-43d5-aff6-101032227011" />

Opening handshake → 프로토콜 전환

<aside>

- Upgrade
    
    → 프로토콜을 전환하기 위해 사용되는 헤더
    
- Connection
    
    → 전송이 완료된 후 접속을 유지할 것인가에 대한 정보
    
- Sec-Websocket-key
    
    → 유효한 요청인지 확인하는 키 값
    
- Sec-Websocket-protocol
    
    → 사용하고자 하는 하나 이상의 웹 소켓 프로토콜을 지정
    
- Origin
    
    → CORS 정책으로 만들어진 헤더
    
</aside>

Data transfer → 데이터 전송

<aside>

데이터의 단위는 ‘메시지’이다

</aside>

Closing handshake → 연결 종료
