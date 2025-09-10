# Serial Peripheral Interface

→ I2C, UART와 같은 시리얼 통신(직렬 통신) 방식 중 한 가지로 MCU, 시프트 레지스터, SD 카드 등의 소형 주변 장치 사이에 데이터 전송을 관리

→ SPI 통신은 칩(IC)과 친 간에 데이터를 주고받기 위한 방법중 하나이다

→ 하나의 트랜시버이다

- 1 : N 통신을 지원하는 동기식 통신 방식이다
- 다수의 통신을 원한다면 다수만큼의 선이 필요하다
- 동시 송수신이 가능하며 I2C보다 빠르다

![image](https://github.com/user-attachments/assets/5ba194c9-b9bd-48c1-9611-03e21c2089bb)

## SPI의 4가지 신호

### SLCK(SCK)

→ 동기화 신호이며 클럭 전송을 위한 단자로, 마스터에서 슬레이브로 클럭을 전송

→ 통신 번호가 맞지 않아도 알아서 맞춤 (baud 9600, 115.200)

### MOSI

→ master output slave input의 준 말로 말 그대로 마스터 출력 슬레이브 입력이다

### MISO

→ 슬레이브 출력 마스터 입력으로, 보통 MISO를 통해 슬레이브 명령 데이터가 들어오면 MISO를 통해 슬레이브에서 마스터로 응답 데이터가 출력된다

### CS(SS)

→ chip select, 보통 SS핀 즉 Slave Select로 슬레이브를 선택할 때 사용된다. 다시 말해 마스터 장치에서 슬레이브 장치를 선택하기 위한 단자이다

→ 1:N으로 연결할 때 어떤 slave를 선택할지 고르는 선 (주소로 선택함)

| 신호 | 풀네임 | 방향 | 설명 |
| --- | --- | --- | --- |
| **MOSI** | **Master Out, Slave In** | 🔽 마스터 → 슬레이브 | 마스터가 데이터를 보낼 때 사용하는 선 |
| **MISO** | **Master In, Slave Out** | 🔼 슬레이브 → 마스터 | 슬레이브가 응답 데이터를 보낼 때 사용하는 선 |

즉 MOSI로 묻고 MISO로 질문에 답을 받는다고 생각하면 편하다

---

![image](https://github.com/user-attachments/assets/560a8b20-4479-4c24-a8bf-2a36e434cf65)

SPI 장치들은 Shift Register를 가지고 있다

| 용어 | 의미 |
| --- | --- |
| **MSB** | Most Significant Bit → 가장 중요한(큰 자리) 비트 (보통 맨 왼쪽) |
| **LSB** | Least Significant Bit → 가장 덜 중요한(작은 자리) 비트 (보통 맨 오른쪽) |

`0b11010010` 이라는 8비트 숫자가 있다면 

MSB는 1 (맨 왼쪽)

LSB는 0 (맨 오른쪽)

MSB부터 전송된다 → 왼쪽 부터 한 비트씩 천천히 보낸다

구형이거나 특수 목적용(LSB)는 오른쪽 부터 보내는데 이는 양쪽의 설정이 동일해야함

기본적으로 MSB 부터 전송된다. 위 그림처럼 SHIFT REGISTER에 의해 데이터가 이동한다

(특정 컨트롤러는 LSB부터 전송된다)

---

Master → Slave 값을 보낼 때 1Clock 신호마다 1bit의 data가 이동된다

![image](https://github.com/user-attachments/assets/c0e2353b-2be9-474b-b39f-f6fa3c869267)

이처럼 data는 밀어내기 식으로 들어간다

---

# SPI 장단점

**장점**

- 전이중 즉 양뱡향 통신이다
- 최대 16비트까지 맘대로 길이를 조절할 수 있다
- 전송기가 필요없다 (=트랜시버가 필요 없다)
- 단순 센서나 메모리에서 많이 사용된다
- IC 패키지에 4개의 핀만 사용
- 최대 클럭이 제한되지 않아 속도 제한이 없다
- Push-pull 출력을 사용하여 상호 간에 같은 전압을 사용하여 시그널 정합성과 고속을 지원한다
- I2C 보다 낮은 소비 전력
- 정확성이 떨어져도 상관 없다

**단점**

- 하드웨어 슬레이브 인식이 없음
- 슬레이브에 의한 하드웨어 흐름 제어가 없음
- 오류 검사 프로토콜이 정의되어 있지 않음
- 노이즈 스파이크에 영향을 받음
- RS-232, CAN 버스보다 비교적 더 짧은 거리에서 동작한다
- 하나의 마스터 장치만 사용한다
- Hot 플러그를 지원하지 않는다
---

### 연결 방식

<img width="688" height="316" alt="image" src="https://github.com/user-attachments/assets/0a90f3a9-c267-4a6f-88db-2f3daec82e6f" />

- Daisy chain은 보통 사용하지 않는다
