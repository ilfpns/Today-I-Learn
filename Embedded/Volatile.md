> **Volatile**
> 

---

⇒ Volatile : 휘발성 물질, 불안정한

⇒ 특정 변수의 값이 프로그램 흐름에 의해 예측할 수 없어, 항상 메모리에서 직접 읽도록 지시하는 키워드이다

**예제**

```c
int flag = 0;

while(flag == 0) {

}
```

다음과 같은 코드가 있을 때 

while문 안에 flag의 값을 변화하는 코드가 없을 떄 컴파일러는 다음과 같이 최적화를 진행한다

**ㅤ**

컴파일러 : flag가 바뀌지 않으니 더이상 검사하지 않고 계속 반복해야겠다 !

⇒ 외부 센서 값이나, 인터럽트가 발생해도 알아챌 수 없음

**ㅤㅤ**

그렇기에 메모리에서 계속 읽어주는 키워드인 Volatile을 사용한다

**ㅤㅤ**

```c
volatile bool button_pressed = false;

void ISR(void) {
    button_pressed = true;   // ISR은 신호만 남김 (빠르게 끝남)
}

int main(void) {
    while (1) {
        if (button_pressed) {
            button_pressed = false;
            toggle_LED();      // 메인 루프에서 안전하게 처리
            send_UART("Pressed");
        }
    }
}
```

⇒ 다음 코드에서 button_pressed는 Volatile로 외부 이벤트를 받아 값만 딱 바꿔주고 끝남 

**ㅤ**

**장점**

- 외부 변화 감지 보장
- 인터럽트 신호 정확이 보장
- 최적화로 인한 버그 방지
- 코드 의도 명확화
- 컴파일러의 캐싱을 막아 바뀌는 값을 바로 인지함
