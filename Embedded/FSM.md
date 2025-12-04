> **State Machine**
> 

---

⇒ 장치나 프로그램의 동작을 상태로 나누고 조건에 따라 상태가 바뀌도록 만들어진 구조

⇒ 오로지 한 개의 상태를 가짐, 이러한 상태는 어떠한 사건에 의해 다른 상태로 변한다 이를 천이라 한다

**ㅤ**

장점

- 안전성
    
    ⇒ 통제 가능한 변인을 제어하여 원하는 아웃풋을 내기 때문이다, if-else나 switch-case 문은 변수 오염이라던가, 잘못된 플로우를 타게 할 경우 코드가 꼬인다
    
- 플로우가 계획된 대로 흐른다
- 정해진 이벤트를 통해 상태가 천이된다

**ㅤ**

**상태**

- IDLE
- RUNNING
- ERROR
- WAIT_SENSOR

와 같은 식으로 현재 시스템의 모드를 하나만 갖고 있음

**ㅤ**

**구현**

```bash
switch(state) {
    case IDLE:
    case RUN:
    case ERROR:
}
```

다음과 같이 switch로 쉽게 구현할 수 있음

switch를 안 쓰는 것이 아니라, FSM모델 기반 설계를 하는 것

**ㅤ**

> **EFSM**
> 

---

⇒ FSM + 내부 변수 + 가드 조건식을 포함하는 모델

**ㅤ**

**구조 구성 요소**

- state : 현재 상태
- Event : 상태 전이를 일으키는 입력
- Action : 전이 시 수행하는 동작
- Variable : 카운터, 플래그, 센서값 등 내부 데이터
- Guard Condition : 변수 기반 조건식 (전이 여부 결정)

**ㅤ**

FSM : 상태 + 이벤트로 전이

EFSM : 상태 + 이벤트 + 조건 + 변수 조합으로 전이

**ㅤ**

> **계층형 상태 머신**
> 

---

⇒ 상태 폭발을 줄이기 위해 상태를 계층 구조로 표현함

**ㅤ**

**개념**

- 상위 상태(Superstate) 안에 여러 하위 상태(Substate)가 존재
- 공통 행동을 상위 상태에서 처리
- 하위 상태는 개별 행동만 처리

**ㅤ**

**예제**

```bash
SUPER_STATE: RUNNING
 ├─ SUB_STATE: WAIT_DMA
 ├─ SUB_STATE: PROCESS_SENSOR
 └─ SUB_STATE: SEND_PACKET
```
