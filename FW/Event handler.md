# Even_Handler

**→ 프로그램에서 이벤트 발생시 호출되는 콜백 함수**

- 정해진 형식을 따라야 한다
- 시스템이 내부적으로 값을 넘겨준다

`(void *handler_arg, esp_event_base_t base, int32_t event_id, void *event_data)`

대게 위와 같은 형식을 지원한다

| *handler_arg | 등록할 때 사용한 사용자 데이터 |
| --- | --- |
| base | 이벤트 그룹 |
| event_id | 해당 그룹 내 세부 이벤트 |
| *event_data | 이벤트 관련 데이터 포인터 (이벤트 종류마다 다른 구조체를 가르킴) |
- *handler_arg
    
    → NULL 또는 구조체 포인터의 정보들을 받아온다
    
- base
    
    → WIFI EVENT, IP EVENT, WEBSOCKET EVENT 등을 받아옴
    
- event_id
    
    → 이벤트 상태 변화를 저장함 (ex : WEBSOCKET_EVENT_CONNECTED, WEBSOCKET_EVENT_DISCONNECTED 등의 상태)
    
- *event_data
    
    → Websocket의 경우 `esp_websocket_event_data_t` 를 가르킴
    

# Loop의 흐름

1. 이벤트 핸들러 정의
2. 이벤트 루프 생성
3. 핸들러 등록 ( 이때 어떤 EVENT를 감지할지 정함 Ex : WEBSOCKET_ANY_EVENT)
4. 이벤트 발생 or 호출
5. 이벤트 큐에 저장 → 핸들러 실행 → 로직 처리
6. 핸들러 해제 or 루프 삭제

# EVENT_BASE? EVENT ID?

### EVENT_BASE

→ 라이브러리가 그룹화한 상수 플래그

→ WIFI_EVENT, IP_EVENT 등 사용자가 직접 정의한 이벤트

### EVENT_ID

→ 특정 베이스 그룹에서의 항목

→ WIFI_EVENT_STA_START, IP_EVENT_STA_GOT_IP 등

- 두 인자 모두 문자열 매크로처럼 선언된 상수이다

# TIP

- `handler_arg` 는 복사되지 않음, 등록 후에도 유효해야 함
    
    → 메모리 관리에 주의를 요망한다
    
- `esp_websocket_event_data_t *data = (esp_websocket_event_data_t *)event_data;` 위와 같은 식으로
    
    자료형이 없는 포인터는 사용할 수 없기에 *data에 구조체 값을 옮김 
    
    void는 필드에 접근할 수 없기에 명시적 형변환을 해준다
    
    void는 어떤 자료형인지 알 수 없음 
    

**필드**란? 구조체 내부에 정의된 포인터 변수
