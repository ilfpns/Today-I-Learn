> **LifeCycle**
> 

---

⇒ 각 위젯이 얼만큼의 시간동안 동작하는지 나타내는 과정으로 위젯의 생명 주기 라고도 한다

> **Stateless**
> 

---

<aside>

- 오른쪽 사진은 Stateless의 LifeCycle을 시각적으로 나타낸 것이다

---

⇒ immutable (불변) 속성을 가지고 있다

1. 처음 실행될 때 Constructor (생성자)가 호출된다
2. Build를 실행하며 앱의 본격적 코드를시작한다
</aside>

<img width="113" height="300" alt="image" src="https://github.com/user-attachments/assets/79a695f1-9e4e-4b5d-8cbc-8f60a0332f42" />

> **Stateful**
> 

---

<img width="870" height="497" alt="image" src="https://github.com/user-attachments/assets/9e3f5197-0bd7-43ed-9280-a4ea4af24f86" />

<img width="681" height="755" alt="image" src="https://github.com/user-attachments/assets/9d5e3859-55e1-424a-84f6-a2b2b6007dc4" />

<aside>

- 위쪽 사진은 Stateful의 LifeCycle을 시각적으로 나타낸 것이다

---

⇒ SetState (rebuilld)를 할 수 있다

1. Constructor - 실행될 때  항상 생성자가 호출된다
2. CreateState - Statefulwidget의 두 번째 클래스의 인스턴스를 만든다
3. initState - state를 초기화 하며, 최초 한 번만 호출된다
4. didChangeDependencies - 위젯이 의존하는 데이터의 객체가 변할 때 호출된다
5. build - 재정의 대상으로, 앱의 본격적 실행이 시작된다
6. dispose - 메서드에서 사용한 것들을 영구적으로 삭제한다

- build는 dirty와 clean사이에 위치한다
- dirty상태에서 실행 준비가 완료되어 build를 할 수 있다
- clean상태에서는 build를 실행할 수 없다
- SetState를 사용하면 Clean → dirty로 돌아가 build를 다시 할 수 있게 한다

- didUpdateWidget은 부모 위젯에서 새로운 데이터가 전단되어 같은 state를 유지한 채 갱신될 때 사용된다
- didUpdateWidget은 자동으로 호출되고 setState를 개발자에 의해 호출된다

</aside>
