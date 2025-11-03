> **RTOS 예제부터 실행**
> 

---

```bash
cd $IDF_PATH/examples/system/freertos/task
idf.py build flash monitor
```

**ㅤ**

> **Naming rules**
> 

---

- `c`: `char` 타입을 의미한다.
- `s`: `int16_t` 타입 (`short`)을 의미한다.
- `i`: `int32_t`타입 (`int`)을 의미한다.
- `x`: `BaseType_t` 타입을 의미한다. 상당히 자주 사용되는데, **구조체나 인스턴스 핸들** 등 일반적인 타입을 제외하면 대부분 `x`다.
- `u`: `unsigned`를 의미한다.
- `p`: 포인터 변수를 의미한다.

**ㅤ**

> **xTaskCreate**
> 

---

![Uploading image.png…]()

**⇒ 어떤 파리미터를 받는지 표기한다 (return이 없는 v 함수임)**

**ㅤ**

- `pvTaskCode`는 task의 기능이 선언된 함수의 함수포인터를 말한다.
- `pcName`은 디버깅 용도로 사용하는 문자열이며 task의 이름을 말한다.
- `usStackDepth`는 task마다 할당되는 stack 메모리를 말한다. 단위는 `WORD`이며 우리가 사용하는 ARM Cortex-M보드에서는 `1WORD == 4Byte`라는 점을 기억하자.
- `pvParameters`는 task 함수로 전달할 매개변수를 말한다. 없다면 `NULL` 쓰면 된다. 전달할 매개변수를 `(void*)` 타입으로 캐스팅한 뒤 여기다가 넣어주면 task 함수에서 사용할 수 있다.
- `pxCreatedTask`는 task를 제어하기 위한 `TaskHandle_t` 타입 핸들을 말한다. Task의 우선순위를 바꾸거나, task를 멈추거나 등 task에 대한 설정은 모두 이 핸들을 통해서 이뤄진다.

**ㅤ**

**vTaskDelay**

⇒ Task를 멈춤 상태로 만든다, 즉 실행중인 Task를 block 상태로 만들어 정지시킨다

⇒ ms(밀리초) 단위를 tick으로 바꿔서 사용하는 것이 표준화되어 있기에 좋다

**ㅤ**

- pdPASS : 태스크가 성공적으로 생성되었다
- pdFAIL : 메모리 부족으로 인한 태스크 생성 실패가 나타난다

**ㅤ**

**vTaskDelayUntil**

⇒ vTaskDelay와 같은 역할을 하지만, 호출 시점과 관계 없이 목표 절대 시간 주기에 맞춰 정지된다

**ㅤ**

vTaskSuspend, vTaskResume

⇒ Task를 기약없이 block 상태로 만든다.

⇒ task의 핸들러를 파라미터로 받는다

⇒ Task의 우선순위를 바꿀 때 block 상태로 state를 전환해야한다

**ㅤ**

**vTaskPrioritySet**

⇒ 우선순위를 조정 하는 데에 사용한다

**ㅤ**

> **실습**
> 

---

`xTaskCreate((TaskFunction_t)Task1, "Task1", 128, NULL, 10, &xHandle1);`

⇒ vTaskDelay를 생성한다

⇒ null부분에 데이터를 담은 구조체를 담는다 

**ㅤ**

> **SoftWare timer**
> 

---

| 함수명 | 설명 |
| --- | --- |
| xTimerCreate() | 새로운 소프트웨어 타이머 객체를 생성 |
| xTimerStart() | 기본 상태(꺼짐)인 타이머를 시작(만료 후 콜백 실행) |
| xTimerStop() | 실행 중인 타이머를 정지 |
| xTimerDelete() | 타이머를 삭제하고 리소스 회수 |
| xTimerChangePeriod() | 실행 중인 타이머의 주기를 변경 |
| xTimerReset() | 타이머 주기를 리셋하고(다시 카운트다운 시작) |
| xTimerIsTimerActive() | 타이머가 현재 동작 중인지 여부 확인 |
| vTimerSetTimerID() / pvTimerGetTimerID() | 타이머 ID 설정/가져오기 (콜백 내부에서 TimerHandle_t→ID 매핑용) |

**ㅤ**

> **Hook Function**
> 

---

⇒ RTOS가 특정 이벤트를 감지했을 때 사용자가 미리 등록해둔 자동 함수를 자동 호출하는 콜백 메커니즘이다

**ㅤ**

Hook 함수가 필요한 이유

1. 커널 코드 수정 방지
    
    ⇒ 이식성, 안전성이 중요하므로, 커널 코드를 직접 수정하지 않게 Hook을 제공
    
2. 시스템 레벨 이벤트 감지
    
    ⇒ 메모리 부족 등의 내부 이벤트를 사용자 코드가 감지 가능
    
3. 경량 콜백 구조
    
    ⇒ 간단한 상태확인, 로그, 정리 작업을 저비용으로 수행 가능하다
    
4. 실행 시간 예측 가능
    
    ⇒ 언제 실행되는지 알 수 있어서, 타이밍을 예측할 수 있다
    

**ㅤ**

| Hook 이름 | RTOS 내부에서의 의미적 위치 | 시스템 수준 역할 |
| --- | --- | --- |
| **Idle Hook** | “모든 Task가 Blocked일 때” | CPU 유휴 시간 동안의 백그라운드 동작 또는 저전력 전환 |
| **Tick Hook** | “주기적 시간 단위 (Tick ISR)” | 실시간 제어용 짧은 타이밍 이벤트 처리 |
| **Malloc Failed Hook** | “Heap 메모리 부족 감지” | 시스템 리소스 고갈 대응, 안전 종료 |
| **Stack Overflow Hook** | “스택 검사 실패 시점” | 커널 보호 메커니즘, 오작동 방지 |
| **Daemon Task Startup Hook** | “RTOS의 Timer Task 시작 시점” | 커널 의존 초기화 코드 삽입 |
| **Static Memory Hooks** | “정적할당 지원 시점” | RTOS 핵심 Task(Idle, Timer)용 메모리 제공 |

**ㅤ**

> **RTOS 코드에서**
> 

---

```c
QueueHandle_t q;

void SenderTask(void *pvParameters) {
    int count = 0;
    for (;;) {
        xQueueSend(q, &count, portMAX_DELAY);
        count++;
        vTaskDelay(pdMS_TO_TICKS(500));
    }
}

void ReceiverTask(void *pvParameters) {
    int value;
    for (;;) {
        if (xQueueReceive(q, &value, portMAX_DELAY)) {
            printf("Received: %d\n", value);
        }
    }
}

void app_main(void) {
    q = xQueueCreate(5, sizeof(int));
    xTaskCreate(SenderTask, "Send", 2048, NULL, 1, NULL);
    xTaskCreate(ReceiverTask, "Recv", 2048, NULL, 1, NULL);
}
```

**ㅤ**

- 2개 Task 생성 → Queue 통신 ⇒ 간편하게 관리
- LED Task + UART Task ⇒ 하드웨어 맞는 Task를 직접 분리
- Sensor Task + BLE Task ⇒ 동시에 실행할 Tsak를 분리/제어
- 프로토콜 ⇒ 프로토콜 전용 Task 사용 (ap_task ← SoftAP 연결 Task)

**ㅤ**

> **메모리 단편화**
> 

---

⇒ 메모리를 할당하고 해제하는 과정에서  빈 공간이 조각조각 흩어져 연속된 큰 공간이 생기는 현상

**ㅤ**

| 이름 | 역할 | 크기 결정 |
| --- | --- | --- |
| **Stack** | 그 Task 안에서 지역 변수, 함수 호출 스택 | usStackDepth |
| **TCB (Task Control Block)** | Task의 상태 정보 (레지스터 값, 상태, 우선순위 등) | FreeRTOS 내부 구조체 크기 |

⇒ Task = Stack + TCB

**ㅤ**

```scss
처음 힙 상태 (20KB)
[                    free 20KB                    ]

TaskA 생성 (4KB)
[AAAA][                free 16KB                 ]

TaskB 생성 (5KB)
[AAAA][BBBBB][            free 11KB              ]

TaskA 삭제 → 4KB 해제
[ free 4KB ][BBBBB][         free 11KB           ]
```

⇒ 다음과 같이 메모리가 이어지지 않고 구멍이 생김 ⇒ 외부 단편화

**ㅤ**

**생기는 이유**

⇒ FreeRTOS의 heap 관리자는 복잡한 메모리 병합을 거의 안 함

⇒ 시간이 지날수록 단편화된 메모리들이 쌓임
