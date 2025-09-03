# RTOS type

---

## Hart RTOS

⇒ 어떤 작업을 일정한 시간 내에 반드시 수행, 처리해야 하며, 그 시간이 지난 경우 결과 값이 아무리 정확해도 필요 없다

## Soft RTOS

⇒ 주어진 시간 안에 처리하면 좋지만, 그렇지 못한 경우에는 그 시간에서 약간 경과한 후의 값도 인정함

---

### GPOS vs RTOS

|  | General Purpose Computers | Real-Time Embedded Systems |
| --- | --- | --- |
| 목적 | 다양한 분야에 사용되며, 효율성을 중시한다 | 실시간 응용 분야에 사용되며, 효율보다는 시간을 중시 |
| 응답 시간 | 일반적으로 예측 가능한 응답 시간 | 엄격한 응답 시간 요구 (1초 이내) |
| 스케쥴링 | 완전성 우선 순위 또는 다중 큐 스케쥴링 | 우선 순위 기반 또시 시간 분할 스케쥴링  |
| 자원 할당 & 관리 | 동적 자원 할당 & 해제 가능 | 고정된 용량의 자원 할당 및 관리 기능 |
| 우선 순위 | 일반적으로 우선순위 관리가 유연 | 엄격한 우선순위 관리 |
| 커널 크기 & 복잡성 | 큰 크기 및 복잡성을 가질 수 있다 | 작은 크기와 상대적으로 간단한 구조 |
| 이식성 | 여러 플랫폼에서 동작 가능 | 다양한 하드웨어 플랫폼에 이식 가능 |
| 시스템 완전성 | 일반적으로 완전성을 보장하지 않음 | 높은 수준의 시스템 완전성 보장 |
| 응용 분야 | 데스크톱, 모바일, 서버 | 자동차, 의료, 항공 |

---

### 코딩 방식의 차이 (Firmware vs RTOS)

⇒ 코딩 방식의 차이는 주로 H/W 초기화, Task 관리, 스케쥴링 및 동기화 매커니즘 등에서 나타난다

<img width="949" height="507" alt="image" src="https://github.com/user-attachments/assets/c70a170a-bae7-42d6-a65b-2e70c30a3115" />

---

## H/W 초기화

### Firmware

```c
void initializeHardware() {
	configureGPIO();
	configureUART();
	configureTimer();
}
```

### RTOS

⇒ RTOS 는 일반적으로 보다 추상화된 레벨에서 하드웨어 초기화를 처리한다

⇒ 플랫폼마다 차이는 존재하고, RTOS 내부에서 처리되기도 한다

⇒ 그러므로 직접 초기화 코드를 작성하지 않는 경우도 있다

---

## Task, Scheduling

### Firmware

```c
void main() {
	while (1) {
		processMainTask();
	}
}
```

### RTOS

⇒ RTOS를 사용할 경우, 테스크를 정의하고 운영체제에게 스케쥴링을 맡긴다

⇒ 각 태스크는 우선 순위와 실행 주기를 가지며, RTOS는 스케쥴링을 통해 작업을 관리한다

```c
void task1() {
    // 태스크 1의 동작
}

void task2() {
    // 태스크 2의 동작
}

int main() {
    // 태스크 생성
    createTask(task1, priority1, period1);
    createTask(task2, priority2, period2);
    
    // RTOS 시작
    startRTOS();
}
```

---

## Sync & Protocol

### Firmware

```c
void main() {
    // 인터럽트 비활성화
    disableInterrupts();
    
    // 공유 데이터 접근
    accessSharedData();
    
    // 인터럽트 활성화
    enableInterrupts();
}
```

### RTOS

⇒ RTOS는 세마포어, 뮤텍스, 메시지 큐와 같은 동기화 매커니즘을 제공하여 Task간의 안전한 데이터 공유와 통신을 관리한다

```c
SemaphoreHandle_t sem;

void task1() {
    // 세마포어 대기
    xSemaphoreTake(sem, portMAX_DELAY);
    
    // 공유 데이터 접근
    accessSharedData();
    
    // 세마포어 반환
    xSemaphoreGive(sem);
}

void task2() {
    // 세마포어 대기
    xSemaphoreTake(sem, portMAX_DELAY);
    
    // 다른 공유 데이터 접근
    accessOtherSharedData();
    
    // 세마포어 반환
    xSemaphoreGive(sem);
}
```
