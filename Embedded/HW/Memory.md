> **들어가며**
> 

---

⇒ 저장장치는 휘발성, 비휘발성 두가지 종류로 나뉜다

**ㅤㅤ**

비휘발성 장치는 (NVS) 전기적 저장장치로 → RAM, 캐시, 레지스터가 이에 속한다

휘발성 장치는 (NVM) 기계적 저장장치로 → ROM, HDD, SSD, 자기 디스크, 광학 디스크, 자가 테이프가 이에 속한다

**ㅤ** 

<img width="957" height="684" alt="image" src="https://github.com/user-attachments/assets/baab03b2-e742-4c0d-be33-d19197c42921" />

**ㅤ** 

> **Non-Volatile Storage**
> 

---

⇒ Flash의 일부를 사용함

⇒ key-value 형태로 데이터를 관리한다

**ㅤ** 

- NVS는 펌웨어 용어이다 → NVM을 관리하는 SW계층
- Flash에 직접 쓰지 않고, NVS 라이브러리가 관리함 → 수명과 무결성 확보

**ㅤ** 

1. 사용자 설정값
2. 센서 보정값
3. Wi-Fi (SSID, PASSWORD)
4. 각종 사용자 ID, 장비 이름 등 계속 기억해야할 중요한 내용

**ㅤ** 

> **Non-Volatile Memory**
> 

---

⇒ Flash, EEPROM, FRAM을 포함

⇒ 비휘발성 저장공간 전체를 의미한다

**ㅤ** 

- NVM은 하드웨어 용어 → 비휘발성 물리 메모리

**ㅤ** 

| 종류 | 특징 | 비고 |
| --- | --- | --- |
| Flash | 섹터 단위 Erase, 수명 제한(1만~10만회) | MCU 내부 가장 흔함 |
| EEPROM | 바이트 단위 쓰기 가능, 느림 | 소형 데이터 저장 |
| FRAM | 빠르고 수명 김 | 고가 MCU에서 사용 |
| MRAM | 자기저항 메모리, 고내구성 | 산업용 일부 |

**ㅤ** 

1. 펌웨어 코드
2. 초기화된 전역변수
3. 상수 (const)
4. 부트로더
5. OTA 백업 영역
6. NVS 영역 (일부)
