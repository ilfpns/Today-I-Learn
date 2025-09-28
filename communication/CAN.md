> Controller Area Network
> 

---

⇒ 차량 내에서 호스트 컴퓨터 없이 MCU들이 서로 통신하기 위해 설계된 표준 통신 규격이다

⇒ 차량 내에 수만은 ECU들이 CAN 프로토콜을 사용해 통신한다

<img width="952" height="250" alt="image" src="https://github.com/user-attachments/assets/c9cc1b69-4d93-4095-bd42-a802c5a877cd" />

### 특징

1. 메시지 지향성 프로토콜
    - 메시지 우선순위에 따라 ID를 부여하고, ID를 이용해 메시지를 구분한다
    - 메시지가 자신에게 필요한지를 ID를 기반으로 판단한다
2. 보완적인 에러 감지 메커니즘 
    - 메시지 전송 시, 에러가 감지되면 자동적으로 해당 메시지를 즉시 재전송한다
3. 멀티 마스터 능력
    - 버스가 비어 있을 때 라면 언제든지 전송이 가능하다
    - 모든 노드가 버스 마스터가 되는 것이며
    - 우선 순위 높은 메시지를 먼저 전송한다
    - 우선 순위는 ID값이 낮은 메시지가 더 높은 우선순위를 가진다
4. 결점 노트 감지 및 비활성화
    - 실시간 결함 노드를 감지하고 해당 노드를 비활성화한다
5. 전기적 노이즈에 강함

### CAN BUS 네트워크 동작 원리

CAN은 다중통신망이며, CSMA/CD+AMP 방식을 이용한다

1. CAN노드는 메시지를 보내기 전에 버스가 사용중인지 파악한다 (메시지 간 충돌 검출을 수행한다)
2. 메시지에는 송수신측 주소를 포함하지 않고, 고유 ID가 있다 (11bits or 29bits)
3. 각 ECU마다 고유 ID값이 존재하고, 메시지를 보낼 때 해당하는 ECU ID값을 메시지 헤더에 붙어서 메시지 CAN 버스에 올려보내면 ID에 해당하는 ECU 쪽에서 메시지를 읽는다

- CAN 메시지 ID는 11bits(CAN 2.0A) 또는 29bits(CAN 2.0B)를 가지며, 역할/우선순위를 가진다

<img width="950" height="140" alt="image" src="https://github.com/user-attachments/assets/541282fb-21b2-4ebe-8b97-f45ec50feb9b" />

### CAN 프로토콜 규격

⇒ CAN메시지 ID의 길이에 따라 2가지 버전으로 구분한다

**ㅤ**

**표준 (Standard) CAN (2.0A) :** 11 bits, ISO 11898 (1Mbps 이상 고속 통신)

**확장 (Extended) CAN (2.0B) :** 29 bits, ISO 11519 (125Kbps 까지 통신)

**ㅤ**

표준 CAN 컨트롤러는 오직 표준 CAN포맷 메시지만 송수신할 수 있다 

확장 CAN 컨트롤러는, 표준/확장 CAN 포맷 메시지모두 송수신할 수 있다

### CAN 메시지 구조

1. 데이터 프레임 → 데이터 전송에 사용
2. 리모트 프레임 → 수신노드에서 송신노드에게 원하는 메시지 전송 요청을 위해 사용
3. 에러 프레임 → 메시지 에러 감지시 시스템에게 알리기 위해 사용
4. 오버로드 프레임 → 메시지 동기화에 사용

### 메시지 프레임

<img width="941" height="518" alt="image" src="https://github.com/user-attachments/assets/c6bc6d6e-d65c-45dd-8810-8513df8f50d8" />

SOF : Start Of Frame

⇒ 메시지 처음을 지시, 모든 노드 동기화를 위해 사용

**ㅤ**

Arbitation Field 

⇒ 중재 필드, ID와 RTR (1bit)로 구성, 메시지간 충돌을 조정하는데 사용한다. RTR비트의 값은 데이터 프레임(d) 인지 리모트 프레임(r) 인지 결정한다

**ㅤ**

Control Field 

⇒ 제어 필드, IDE(2bits), DLC(4bits) 로 구성, R0는 Reserved 비트 (Extended CAN 2.0B R0, R1)이다

**ㅤ**

Data Field 

⇒ 데이터 필드 8bytes 까지 사용 가능, 전송 데이터를 저장

**ㅤ**

CRC Field

⇒ SOF에서 데이터 필드까지 비트열을 이용해 생성한 CRC 시퀀스 (15bits)와 하나의 ‘r’bits의 CRC  DEL로 구성, 메시지 상의 에러 유무검사에 사용한다

**ㅤ**

ACK Field

⇒ ACK 슬롯 (1bits) 와 ACK DEL (1bit, ‘d’)로 구성, 임의의 노드에서 올바른 메시지 수신시 ACK Field를 받는 순간 ACK 슬롯을 ‘d’로 설정해 버스 상에서 계속 전송한다

**ㅤ**

EOF Field

⇒ 프레임 종료, 7개의 ‘r’bit로 구성되어 메시지 끝을 알린다

### CAN Controller

- 내부 버퍼를 가지며, Transceiver 에서 전달되는 수신 메세지에 대해 ID를 기반으로 유효한 데이터인지 판단하며, 유효한 데이터일 떼 MCU로 전달한다
- CAN Bus 혹은 MCU 에서 전달되는 송수신 데이터를 전기적 신호로 변환한다
