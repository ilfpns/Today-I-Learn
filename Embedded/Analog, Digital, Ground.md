> analog와 digital의 특징
> 
1. digital신호는 Analog신호의 일종임(대부분 DC로 이뤄짐) ← 있다, 없다 의 Boolean Logic값

> Digital
> 

Digital신호는 high, low 두개의 Logic value만 가질 수 있음 ← 신호가 있다, 없다

좀더 구체적으로 특정 값 이상이면 high 이하면 low와 같은 방식

디지털은 값이 변하며 Bounce를 함 이 요동에 크기에 따라 시스템에 끼치는 영향의 정도를 측정

- 여담
    
    High impedance 상태란, 입력이나 출력이 회로에서 완전히 분리된 것처럼 전류의 흐름에 거의 영향을 주지 않는 상태이다.
    

> GND, Ground
> 

모든 전기, 전자 회로에서 다른 모든 전위에 대하여 기준이 0v을 뜻함

일반적으로 전기의 -극을 의미 

system내부에서 모든 current가 몰려듦.

이는 전류가 ‘돌아가는 경로’는 의미

GND는 마치 땅에 막대를 박은 ㅗ 처럼 연결을 표시함, 이곳에 연결되어 있는 회로상의 모든

point는 절대 0v로 같다는 것을 의미

→ PCV기판 뒷면에 전류가 몰릴 수 있는 환경을 만들어 놓은 후 전위 기준으로 사용

---

PWM = Pulse Width Modulation (펄스 폭 변조)

디지털 신호의 ON/OFF 비율을 조절하여 아날로가 값을 흉내내는 것

아두이노를 예로 들어

```scss
digitalWrite(ledPin, 128);
analogWrite(ledPin, 128);
```

윗 코드를 아래 코드처럼 변형한 것이 PWM이다
