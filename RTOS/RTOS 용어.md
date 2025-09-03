# RTOS 용어 정리

> RTOS Scheduling
> 
- RTOS에서 Task들을 어떻게 실행할 지 결정하는 프로세스를 의미한다
- RTOS는 다양한 스케쥴링 알고리즘을 제공하여 Task들의 우선순위, 실행 주기, 처리 시간 등을 관리한다

> Sequence
> 
- Workload : Task를 의미
- RTOS schedular : CPU를 활용하여 N개의 Task들의 우선순위를 지정한다
- RTOS schedular의 목적 : 모든 Task의 Timing requirement를 만족시키는 것

- 이후 프로세서가 recource되어 Workload (Task) 들을 순차적으로 해결
- Timing requiremen : 타이밍 요구 사항으로, 어떤 동작을 하는 데에 시간 조건을 말한다

<img width="849" height="411" alt="image" src="https://github.com/user-attachments/assets/9f5d0ed7-dfab-4f0a-afeb-31122a53d333" />

---

### 프로그래머 관점에서의 Workload

<img width="873" height="593" alt="image" src="https://github.com/user-attachments/assets/a6a53030-228b-4f4b-a336-c6553fa833c5" />

- 프로그래머 관점에서의 Workload는 Task와 ISR과 같은 것이다
- RTOS에서 프로그래밍을 할 때는 Firmware programming과 달리 main function을 건드리지 않고 (OS가 가지고 있음)
    
    Task, ISR을 function 형태로 작성하여 OS에게 제공하게 되고 OS는 이 function을 활용하여 scheduling 한다
    
    - Task
        
        → 정해진 주기마다 OS가 trigger 시켜준다, OS에게 주기를 알려주면, OS가 정해진 시간에 해당 함수를 호출한다
        
    
    - ISR
        
        → OS가 아닌, H/W interrupt 발생시 호출된다
        

---

<img width="864" height="419" alt="image" src="https://github.com/user-attachments/assets/5cc6ea64-21b9-482c-9ebb-a54d7aee80f4" />

### 1. Task

: 실행 가능한 독립적인 작업 단위

→ 이 작업 단위는 프로세스나 함수와 같은 의미를 가진다

→ RTOS는 이러한 Task들을 스케쥴링 하여 실행된다

→ (RTOS는 프로세스들의 우선순위를 등록한다)

### 2. Jobs

: Task의 실행 단위로서 태스크 내부에 정의된 동작을 의미한다

→ Job들의 묶음이 Task

→ Task A가 10ms마다 한 번씩 실행된다면, 각 주기마다 실행되는 instance를 Job이라 부른다

---

<img width="874" height="309" alt="image" src="https://github.com/user-attachments/assets/642def70-b364-4463-8e9d-2c449d69fe9e" />

### 1. Task Offset

: 위 그림처럼 일정 시간의 Delay를 두고 실행시키는 것

→ Task의 실행이 시작되는 시점을 나타내는 값을 의미

→ Task offset은 주로 주기적으로 반복되는 실시간 작업에 사용된다

→ Task의 시작 시간을 정의하는데 사용한다

→ Time을 처음 초기화할 때 Task를 동시에 Release할 수 있다 하지만 각각 Shifiting시켜서 release할 수도 있다
