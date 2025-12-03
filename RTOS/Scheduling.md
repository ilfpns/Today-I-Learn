> **Preemptive & Cooperative**
> 

---

### Preemptive

- 커널이 강제로 Task를 중단해서 더 높은 우선순위 Task 발생
- Task가 멈춰도 안전하게 작동해야 함
- 인터럽트, 타이머 기반
- 일반적인 RTOS가 해당 방식임**ㅤ**

**ㅤ**

**장점**

- 실시간성이 좋음
- 높은 priority task의 응답시간 최소화

**ㅤ**

**단점**

- 동기화 / Mutex 없으면 race condition 발생이 쉽다

### Cooperative Scheduling

- Task가 스스로 CPU를 양보 해야만 스케줄 체인지
- Task가 while에서 안 빠져나오면 시스템 정지

**ㅤ**

**장점**

- Context switch가 적음
- 상태 추적이 쉬움

**ㅤ**

**단점**

- 실시간성이 낮음
- 하나의 Task가 폭주

**ㅤ**

> **Rate - Monotonic Scheduling**
> 

---

⇒ 고정 우선순위 스케줄링 이론

⇒ 주기가 짧은 Task일수록 우선순위를 높게 부여 ⇒ 더 자주 실행하면 높은 우선순위

**ㅤ**

규칙 : Task주기가 짧을수록 더 빨리 끝나야 하기 때문에 높은 Priority 필요

**ㅤ**

**장점**

- 단순하며 분석이 쉽다
- CPU utilization 69% 이하에서 안정적

**ㅤ**

**단점**

- deadline이 period보다 짧은 시스템엔 부적합
- 우선순위 고정이라 최적화 하기 쉽지 않음

**ㅤ**

> **EDF Scheduling**
> 

---

⇒ 동적 우선순위 스케줄링

⇒ Deadline이 가장 가까운 Task가 먼저 실행

**ㅤ**

**장점**

- CPU utilization을 이론상 100%까지 사용할 수 있다
- 최적 스케줄링 알고리즘이다

**ㅤ**

**단점**

- 동적 priority 계산 → 오버헤드 증가
- MCU같은 제한된 환경에선 잘 안 쓰임 (실시간 OS 거의 미지원)
