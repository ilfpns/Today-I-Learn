# DEQUE

⇒ 양쪽 끝에서 삽입과 삭제를 허용하는 자료구조 

## 특징

- 스택과 큐 자료구조를 혼합한 자료구조
- 스택이나 큐보다 입출력이 자유롭다
- 덱은 double-ended-queue의 줄임말이다
- 전단(front)와 후단(rear)에서 모두 삽입 삭제가 가능하다
- 중간부터 수정은 안됨
- 스크롤 (scroll), 문서 편집기 등의 undo 연산, 방문 기록등에 사용된다

<img width="941" height="272" alt="image" src="https://github.com/user-attachments/assets/9353dcbe-27fc-487c-af34-e38a7d63d1bb" />

그림으로 표현하자면 이런 느낌이다

### 덱의 기능들

- Deque(): 비어 있는 새로운 덱을 생성
- isEmpty(): 덱이 비어있으면 True를 아니면 False 반환
- addFront(x): 항목x를 덱의 맨 앞에 추가
- deleteFront(): 맨 앞의 항목을 꺼내서 반환
- getFront(): 맨 앞의 항목을 꺼내지 않고 반환
- addRear(x): 항목 x를 덱의 맨 뒤에 추가
- deleteRear(): 맨 뒤의 항목을 꺼내서 반환
- getRear(): 맨 뒤의 항목을 꺼내지 않고 반환
- isFull(): 덱이 가득 차 있으면 True를 아니면 False 반환
- size(): 덱의 모든 항목들의 개수 반환
- clear(): 덱을 공백상태로 만듬

## Tips

1. Scroll : 입력 제한 덱 
    
    → 입력이 한쪽에서만 발생하고, 출력은 양쪽에서 일어날 수 있다
    
2. Shelf : 출력 제한 덱
    
    → 입력은 양쪽에서 일어날 수 있고, 출력은 한쪽에서만 일어남
