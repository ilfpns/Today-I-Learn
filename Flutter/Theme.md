> **Theme**
> 

---

⇒ Flutter에서 테마를 지정한다

### 왜 Theme인가 ?

⇒ `style: TextStyle` 을 지정할 때 너무 반복되는 같은 코드를 방지하기 위해 사용된다

⇒ DRY용으로 한 번의 설정으로 관련 페이지 전체에서 사용할 수 있다

### 코드

```dart
theme: ThemeData(
        fontFamily: 'Sunflower',

        textTheme: TextTheme(
          displayLarge: TextStyle(
            color: Colors.white,
            fontSize: 80,
            fontFamily: 'parisienne',
          ),

          displayMedium: TextStyle(
            color: Colors.white,
            fontFamily: 'Sunflower',
            fontSize: 50,
            fontWeight: FontWeight.w700,
          ),

          bodyLarge: TextStyle(
            color: Colors.white,
            fontFamily: 'Sunflower',
            fontSize: 30,
          ),

          bodyMedium: TextStyle(
            color: Colors.white,
            fontFamily: 'Sunflower',
            fontSize: 20,
          ),
        ),
      ),
```

⇒ 다음은 텍스트 스타일의 Theme을 설정한 코드이다

1. theme: ThemeData로 테마를 생성한다
2. 그 안에 각각의 요소에 TextStyle로 세세한 디자인을 한다
    - 맨 위에 어느 body, display에도 속하지 않은 font가 있는데,
    - 이 설정은 다음에 오는 모든 설정에 font를 설정하지 않으면 자동으로 설정되는 기본 폰트의 개념으로 작동한다
3. TextStyle을 감싸는 body, display는 코드를 짜를 데에 문법적 규칙이 존재하지 않는다, 단순히 팀원과 상의하여 정하면 된다
