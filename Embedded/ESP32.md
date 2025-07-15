# ESP32

## uart_param_config()

→ 프토의 기본 통신 설정을 구성해주는 함수이다

```c
uart_param_config(UART_NUM_0, &uart_config); 
```

에서 통신 설정 함수를 호출 후 (사용할 포트 번호, 설정된 내용이 담긴 구조체 주소)를 넘겨 기본 설정

- **uart_num** -- UART 포트 번호, 최대 포트 번호는 (UART_NUM_MAX -1)입니다.
- **uart_config** -- UART 매개변수 설정

### UART_NUM

→ 포트 번호 

ESP32는 기본적으로 3개의 포트를 가진다

1. UART_NUM_0 → 기본 UART, 보통 로그 출력용
2. UART_NUM_1 → UART1
3. UART_NUM_2 → UART2

### uart_config_t

→ UART통신을 설정할 때 사용하는 구조체, SDK에 미리 정의되어 있는 구조체이다

## uart_driver_install

→ UART 드라이버를 설치함

```c

#define BUF_SIZE 1024
uart_driver_install(UART_NUM_0, BUF_SIZE * 2, 0, 0, NULL, 0);
```

- **uart_num** -- UART 포트 번호, 최대 포트 번호는 (UART_NUM_MAX -1)입니다.
- **rx_buffer_size** -- UART RX 링 버퍼 크기.
- **tx_buffer_size** -- UART TX 링 버퍼 크기입니다. 0으로 설정하면 드라이버가 TX 버퍼를 사용하지 않고, TX 함수는 모든 데이터가 전송될 때까지 작업을 차단합니다.
- **queue_size** -- UART 이벤트 큐 크기/깊이.
- **uart_queue** -- UART 이벤트 큐 핸들(출력 매개변수). 성공 시 UART 이벤트에 액세스할 수 있도록 새 큐 핸들이 여기에 작성됩니다. NULL로 설정하면 드라이버가 이벤트 큐를 사용하지 않습니다.
- **intr_alloc_flags** -- 인터럽트 할당에 사용되는 플래그입니다. 하나 또는 여러 개의 (OR 연산으로) ESP_INTR_FLAG_* 값을 사용할 수 있습니다. 자세한 내용은 esp_intr_alloc.h를 참조하십시오. 드라이버의 ISR 핸들러가 IRAM에 위치하지 않으므로 ESP_INTR_FLAG_IRAM을 여기에 설정하지 마십시오.

> **어째서 RX의 size는 2배나 할당될까?**
> 
> 
> ESP-IDF의 문서에 따르면:
> 
> "Hardware FIFO와 별도로, 드라이버는 소프트웨어 버퍼를 하나 더 가지고 데이터를 쌓아 놓습니다. 이 소프트웨어 버퍼의 크기를 지정하는 것이 이 인자입니다."
> 
> 즉
> 
> - `uart_read_bytes()` 같은 함수가 UART 데이터를 읽기 전에,
> - **UART 드라이버가 내부적으로 소프트웨어 수신 버퍼**를 만들어서 데이터를 계속 쌓고 있어야 돼.
> - 이 버퍼가 **FIFO(HW) + SW 버퍼 합쳐서 안정적으로 작동**해야 하므로, 여유를 줘야 해.
> 
> 그래서 보통 공식 예제나 실제 사용 코드에서는:
> 

### rx_buffer_size:  BUF_SIZE * 2

→ 데이터를 안정적으로 수신하기 위해 메모리를 잡아두는 버퍼 공간의 크기를 지정 2048

**Ring Buffer (링 버퍼)란?**

> 원형 순환 구조의 버퍼로 데이터가 차면 다시 처음으로 돌아가는 구조
> 
- MCU가 빠른 데이터의 흐름을 다 읽지 못하기에 잠시 저장할 버퍼가 필요함
- 버퍼가 작다면 오버플로가 발생함
- tx_buffer_size는 수신 → 송신 (데이터를 보냄)

### queue_size: 0

→ 최대 몇 개의 UART 이벤트를 동시에 저장할 수 있는지를 의미한다

- UART 이벤트 큐 = 이벤트를 전달하는 RTOS 큐
    - 어떤 이벤트가 발생했을 때 uart_event_t로 만들어 RTOS에 task에 전달함 ⇒ 이 큐의 길이가 queue_size이다
    - queue_size가 다 쌓이기 전에 처리해야함 (그러지 않다면 오버플로 or 값이 덮여씌여짐)
    - queue_size: 0 → 이벤트가 쌓이자 마자 없앰

### uart_queue

→ UART 통신 중 발생하는 사건(Event) 들을 코드로 전달해주는 통로 (큐) 핸들이다

**핸들 (Handle)** ⇒ 큐, 태스크, 세마포어 등 리소스를 가리키는 포인터

<aside>

한 마디로?

---

UART에서 발생한 일들을 알려주는게 uart_queue이며

개발자는 이를 정기적으로 확인하고 상황을 판단하고 처리한다

</aside>

uart_queue: NULL → 이벤트 큐가 필요하지 않다

### intr_alloc_flags: 0

→ 인터럽트 할당 시 사용되는 플래그를 지정하는 매개변수

intr_alloc_flags: 0 → 특별한 설정 없이 인터럽트를 등록할 때 어떤 특성으로 인터럽트를 할당할지 옵션을 설정한다

## uart_read_bytes

→ 수신 버퍼에 저장된 데이터를 읽어오는 함수

```c
int len = uart_read_bytes(UART_NUM_0, data, BUF_SIZE, 100 / portTICK_PERIOD_MS);
```

- **uart_num** -- UART 포트 번호, 최대 포트 번호는 (UART_NUM_MAX -1)입니다.
- **buf** -- 버퍼를 가리키는 포인터.
- **길이** -- 데이터 길이
- **ticks_to_wait** -- sTimeout, RTOS tick 수

### buf: data

→ 버퍼에 있는 배열 data를 가져옴

### length: BUF_SIZE

→ 내가 읽을 데이터의 최대 바이트 수

### tricks_to_wait: 100 / portTICK_PERIOD_MS

→ 데이터를 받을 때 최대 얼마나 기다릴 것인가?

100 / portTICK_PERIOD_MS → 100밀리초를 FreeRTOS의 틱 단위로 변환한 것

만약 값이 0일 경우 기다리지 않기에 입력이 없으면 바로 0이 리턴됨
