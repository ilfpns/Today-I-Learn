> Interrupt Architecture
> 

---

- Interrupt Latency
- Interrupt priority
- tail chaining
- interrupt safe api
- hard irq & soft irq (irq, ISR)
- interrupt missed

> Exceptions
> 

---

⇒ 프로세서가 동작하는 도중 예상치 못한 상황이나, 예외적인 상황 또는 외부 인터럽트가 발생하는 경우

### Interrupt

- 예상 치 못한 일이 발생했을 때, 오류가 생긴 수행은 인터럽트가 해결 될 때까지 행동을 중지함
    
    ⇒ ISR을 통해 해결됨
    
- 인터럽트 시 CPU의 동작
    1. 중지된 명령어의 주소를 stack에 적재 Program Counter는 루틴을 실행할 명령어 주소를 가르침
    2. ISR이 종료되면 PC는 마지막에 사용된 명령어의 주소를 stack으로 부터 가지고 와서 다시 실행함
    3. 인터럽트가 발생하고 이를 처리 시작할 때까지 걸리는 시간

### EXTI

⇒ 외부 인터럽트

- 시스템 인터럽트는 제조사에서 설계했음
- 그러므로 외부 인터럽트만 설계하면 됨

| System Exception | External Interrupt |
| --- | --- |
| Reset | Timer |
| NMI | USART |
| Hard Fault  | ADC |
| Systick | EXTI |
| etc | etc |

> **Interrupt priority**
> 

---

⇒ 같은 시간에 인터럽트가 발생하면 어떤 인터럽트를 먼저 해결할지 정함

⇒ 동시에 여러 인터럽트가 발생했을 때, CPU가 어떤 ISR을 먼저 실행할지 정해 놓은 HW 우선순위 규칙

- HW 인터럽트 컨드롤러가 우선순위를 정함
- NVIC가 proprity값 비교
- 더 높은 우선순위 먼저 실행

- ARM Cortex-M → NVIC
- x86 → APIC
- RISC-V → PLIC

**Pending**

⇒ 인터럽트 요청을 들어왔는데, 아직 CPU가 처리를 못 하여 대기 중인 상태

> **tail chaining**
> 

---

⇒ Tail (꼬리) + Chaining (연결고리) ⇒ 꼬리를 머리에 연결한다

⇒ ISR에서 다음 pending ISR로 갈 때, 복원/저장 없이 바로 이어서 실행하는 NVIC 최적화 기법

- 중간에 태스크 안 낀다
- context restore/save

위 두 과정을 거치지 않고

```css
ISR(1) → ISR(2) → ISR(3) 
```

으로 바로 ISR끼리 이어지며 해결함

> **Interrupt-safe API**
> 

---

⇒ ISR안에서 호출해도 깨지지 않도록 설계된 RTOS 전용 API

⇒ 인터럽트 컨텍스트에서도 안전하게 사용되는 RTOS 함수

**인터럽트 컨텍스크**

⇒ ISR 이 실행 중인 상태

<aside>

### Queue

- **xQueueSendFromISR** – ISR에서 큐에 데이터 전송
- **xQueueReceiveFromISR** – ISR에서 큐 데이터 수신

---

### Semaphore / Mutex

- **xSemaphoreGiveFromISR** – ISR에서 세마포어 release
    
    *(mutex는 ISR에서 take 불가)*
    

---

### Task 제어

- **xTaskNotifyFromISR** – ISR에서 특정 태스크에 notification 전송
- **xTaskNotifyGiveFromISR** – ISR에서 태스크에 카운트형 notify
- **xTaskResumeFromISR** – ISR에서 suspend된 태스크 재개

---

### Event Group

- **xEventGroupSetBitsFromISR** – ISR에서 이벤트 비트 설정

---

### Context Switch 요청

- **portYIELD_FROM_ISR** – ISR 종료 시 컨텍스트 스위치 필요함을 RTOS에 알림

---

### 공통 보조 타입

- **BaseType_t xHigherPriorityTaskWoken** –
    
    ISR 때문에 더 높은 우선순위 태스크가 깨어났는지 표시하는 플래그
    
</aside>

> **hard irq & soft irq (irq, ISR)**
> 

---

IRQ : 하드웨어가 CPU에 인터럽트 처리 요청을 보냄

ISR : IRQ발생 시 CPU가 즉시 실행하는 함수to

### Hard IRQ

⇒ 하드웨어 인터럽트가 발생하자마자 실행되는 ISR 본체

**특징**

- 인터럽트 컨텍스트
- 스케줄링 불가
- 락 제약이 있음
- 아주 짧음

**하는 일**

- 인터럽트 원인 확인
- 신호 처리
- 바로 작업 해야할 일 처리

### Soft IRQ

⇒ Hard IRQ에머 미룬 후속 처리를 커널이 소프트웨어적으로 실행

**특징**

- softirq컨텍스트
- 스케줄링 불가
- Hardirq보다 우선순위 낮음
- 여러 CPU에서 병렬 실행 가능능

> **interrupt missed**
> 

---

⇒ 인터럽트가 발생했지만 CPU/ISR에서 처리되지 않고 소실된 상태

### 원인

- IRQ 비활성화 구간이 김
- 우선순위 문제
- ISR 지연 & 과부화
- 잘못된 설정

### 증상

- 이벤트 카운터 불일치
- 타이밍 드리프트
- 간혈적 동작 실패
