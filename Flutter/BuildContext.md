> **BuildContext**
> 

---

⇒ 위젯 트리 내에서 자기 위치를 설명하는 객체

⇒ 플러터의 모든 UI를 위젯 트리로 관리하는데, BuildContext는 특정 위젯이 트리에서 어디에 붙어 있는지 알 수 있는 좌표 같은 역할을 한다

### 왜 사용하는가

1. 위젯 트리 탐색
    
    ⇒ 부모/자식 위젯에 접근하거나, 상위 위젯이 제공하는 데이터를 가져올  수 있음
    
2. 위젯 빌드 과정
    
    ⇒ 모든 `build()` 함수는 반드시 `buildContext를`  를 인자로 받음
    
    ⇒ 본인이 트리에 어디에 붙어있는지 알아야 UI를 그릴 수 있기 때문
    

### Context vs BuildContext

- `BuildContext` → 타입 (클래스)
- `Context` → 변수 이름
    
    ⇒ 보통 `build(BuildContext context)`이렇게 쓰는데 여기서 context는 그 타입의 인스턴스이다
    

### **BuildContext 동작 원리**

- 내부적으로는 트리에서 **Element**를 가리키는 핸들.
- Flutter는 `Widget Tree → Element Tree → RenderObject Tree` 구조인데,
    
    `BuildContext`는 **Element Tree의 노드에 접근할 수 있는 키**라고 이해하면 됨.
    

### 한 마디로

- BuildContext ⇒ 타입 (클래스) 자체, 특정 위젯의 위치를 설명함
- Context ⇒ BuildContext의 인스턴스, 보편적으로 context라고 부르는 것 뿐이다
