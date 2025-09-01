# Void* 타입

⇒ 타입이 정해지지 않은 포인터

⇒ 어떤 자료형도 받을 수 있음

```c
int a = 10;
void *p = &a;   // int* 를 void* 에 넣을 수 있음

```

`P` 를 그냥 사용하면 무슨 자료형인지 알 수 없음

→ 캐스팅이 필요함

# 이벤트 핸들러

```c
void event_handler(void* arg,
                   esp_event_base_t event_base,
                   int32_t event_id,
                   void* event_data)
```

- `event_data`는 그 이벤트에 대한 추가 정보가 담긴 주소.
- 하지만 이벤트마다 들어있는 구조체가 다르기 때문에 공통 인터페이스를 위해 무조건 void 타입으로 전달된다

# 캐스팅의 의미

```c
wifi_event_ap_wps_rg_success_t *evt =
    (wifi_event_ap_wps_rg_success_t *) event_data;
```

- `event_data` : 그냥 주소이며 void로 자료형이 정해지지 않음
- `(wifi_event_ap_wps_rg_success_t *)` : 이 주소에는  `wifi_event_ap_wps_rg_success_t` 구조체가 들어있다고 명시하는 것
- `evt` : 이제 그 구조체 타입을 가리키는 포인터로 쓸 수 있음
