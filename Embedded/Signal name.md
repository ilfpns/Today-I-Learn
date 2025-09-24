> **전원 관련**
> 

---

1. VCC ⇒ Voltage at Common Collector
    - 모듈/IC에 전원 공급
    - 동작 전압 공급
    - MCU의 +3.3V/5V 핀에 연결

1. VIN ⇒ Voltage Input 
    - 레귤레이터 앞단 입력
    - 외부 전원을 바로 넣을 때
    - 배터리, 어댑터 출력

1. GND ⇒ Ground
    - 0V 기준 전위
    - 회로 기준점, 전류 귀로
    - 전원 (-), 모든 모듈의 GND 공통 연결

1. VDD ⇒ Voltage Drain-Drain
    - 주로 MOSFET/CMOS IC 전원
    - IC내부 전원 이름
    - VCC와 비슷, MCU/센서 전원편

> **통신**
> 

---

1. TX ⇒ Transmit 
    - UART 송신
    - 데이터 전송
    - MCU의 TX ↔ 다른 기기의 RX

1. RX ⇒ Receive 
    - UART 수신
    - 데이터 수신
    - MCU의 RX ↔ 다른 기기의 TX

1. SCL ⇒ Serial Data Line 
    - I2C 클럭
    - 동기식 데이터 전송
    - MCU I2C SCL ↔ 센서 SCL

1. SDA ⇒ Serial Data Line 
    - I2C 데이터
    - 동기식 데이터 전송
    - MCU I2C SDA ↔ 센서 SDA

1. MOSI ⇒ Master Out Slave Input 
    - SPI : M → S 데이터 전송
    - SPI 쓰기 수신
    - MCU MOSI ↔ 모듈 MOSI

1. MISO ⇒ Master Input Slave Out
    - SPI : S → M
    - SPI 읽기 수신
    - MCU MISO ↔ 모듈 MISO

1. SCK / CLK ⇒ Serial Clock
    - SPI 장치 선택
    - 여러 Slave 구분
    - MCU SCK ↔ 모듈 SCK

1. CS / SS ⇒ Chip Select / Slave Select
    - SPI 장치 선택
    - 여러 Slave 구분
    - MCU GPIO ↔ Slave CS 핀

> **제어/기타**
> 

---

1. RST / RESET ⇒ Reset
    - 칩 리셋
    - 초기화가 필요할 때
    - MCU Reset ↔ 버튼/제어회로

1. INT ⇒ Interrupt
    - 이벤트 알림
    - 빠른 반응 처리
    - MCU GPIO 인터럽트 핀

1. PWM ⇒ Pulse Width Modulation 
    - 신호 제어
    - 아날로그 제어 대체
    - LED, 모터 드라이버 입력

1.
