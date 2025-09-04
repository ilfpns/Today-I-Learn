# RTOS Release time & Deadline 용어

### Release Time (Task 실행 시간)

: Task나 작업이 시스템에 도착하여 실행 가능한 상태가 되는 시간 즉 Real-Time 작업이 시스템에 들어와 작업이 시작될 수 있는 시간

### Deadline

: Task나 작업이 완료되어야 하는 시간 제한, Deadline을 지키지 못 하면 요구 사항을 만족시키지 못할 수 있다, job의 실행이 밀릴 수 있지마느 “어디까지 밀려도 되는가” 와 관련있는 것이 Deadline이다

---

### Release Time의 종류

<img width="879" height="175" alt="image" src="https://github.com/user-attachments/assets/795ad00c-6f1e-41c4-ac2a-1b9a4d73cb5d" />

⇒ Periodic Task

⇒ 주기적으로 Release 되는 Task

<img width="879" height="223" alt="image" src="https://github.com/user-attachments/assets/9c56f6c0-e570-4aca-b9ff-7d7e40f7eb7e" />

⇒ Sporadic Task

⇒ Release와 그 다음 Release 까지의 minimum gap

<img width="876" height="256" alt="image" src="https://github.com/user-attachments/assets/0d127adc-37ef-467f-9f05-01c82cd385b1" />

⇒ Aperiodic Task

⇒ 규칙이 없는 Task

---

### Deadline의 종류

<img width="858" height="315" alt="image" src="https://github.com/user-attachments/assets/6b1b5073-a056-4801-a451-a9a02657f375" />

⇒ Absolute Deadline

⇒ Deadline이 절대적인 단위로 표현한다

<img width="865" height="197" alt="image" src="https://github.com/user-attachments/assets/d2e7da8d-6b89-49d8-a3c3-a0ae29ff459e" />

⇒ Relative Deadline 

⇒ Deadline을 Release Time과 상대적으로 비교

<img width="875" height="138" alt="image" src="https://github.com/user-attachments/assets/bae36979-f6d5-441a-9bbe-8c150d43e8f5" />

⇒ Implicit Deadline

⇒ Deadline에 대한 별도 언급이 없다면, Deadline은 다음 job의 Release Time이 된다

<img width="880" height="176" alt="image" src="https://github.com/user-attachments/assets/43f441f2-2d52-4fe8-b60a-a3889a0ae3cb" />

⇒ Contrained Deadline

⇒ Deadline이 Period보다 작은 경우

<img width="882" height="158" alt="image" src="https://github.com/user-attachments/assets/e77d1c8f-5a2d-48c9-889e-47296a677102" />

⇒ Execution Time

⇒ Task나 작업의 실행 시간을 의미한다, 이는 Task나 Job이 CPU에 얼마나 오랜 시간동안 실행되는지를 나타낸다

⇒ 이 정보를 통해 스케쥴링 알고리즘이 Task를 어떻게 할당할지 결정한다

⇒ Job을 실행시킬 때마다 cache의 상태, 분기문의 실행이 달라지므로 같은 Task의 서로 다른 Job의 실행 시간이 달라질 수 있고, 그렇기에 Task의 execution time을 정의할 방법이 필요하다

---

### BCET

⇒ Best Case Execution Time

⇒ Task나 Job이 가장 이상적인 조건에서 실행될 때 걸리는 최소 실행 시간

### WCET

⇒ Worst Case Execution Time

⇒ Task나 Job이 가장 악화된 조건에서 실행될 때 걸리는 최대 실행 시간

⇒ RTOS에서 중요한 개념중 하나로, 시스템의 실시간 요구 사항을 충족시키기 위해 반드시 고려되어야 하며, 이를 분석하는 SW도 있다
