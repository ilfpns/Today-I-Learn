# RTOS 구성

<img width="533" height="527" alt="image" src="https://github.com/user-attachments/assets/9bd4bfe2-d938-452a-88d8-5b6a4c62f0cc" />

⇒ RTOS는 커널 (Kernal), File system, NetWorking Protocols stack 특정 응용에 필요한 여러 가지 요소 등

⇒ 다양한 모듈(Module)의 조합으로 구성되며, 커널로만 구성되는 경우도 있다

---

## Kernal

⇒ 커널을 하드웨어와 응용 프로그램간의 상호작용을 관리하며, 실시간 응용 프로그램을 스케쥴링하고 제어하는 역할을 한다

## Schedular

⇒ 커널에 포함되며, 언제 어떤 Task를 실행할 지 결정하는 알고리즘을 제공한다

⇒ 대표적인 스케쥴링 알고리즘 예는 `Round-Robin` 스케쥴링과 `preemptive` 스케쥴링이 있다

## Object

⇒ 개발자가 실시간 임베디드 시스템용 응용 프로그램을 만들 때 사용하는 특별한 구조체이다

⇒ 대표적으로 `tack` , `semaphore`, `message-queue` 등이 있다 

## Service

⇒ 커널이 오브젝트를 대상으로 수행하는 동작을 의미한다

⇒ 대표적으로 `Timer` , `Interrupt`, `Memory/Device management` 등이 있다
