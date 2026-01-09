> **Concurrency Model의 근본**
> 

---

⇒ 동시에 여러 작업을 처리할 때 생기는 문제와 설계를 다루는 추상 구조이다

⇒ 여러 흐름이 겹치면서 작동할 때 어떻게 정리하고 제어할 것인가를 규정함

## Parellelism

- 실제로 동시에 실행되는 것에 초점이 있다
- 하드웨어 특성이다

## Concurrency Model

- 여러 흐름간 관계와 상호작용을 정의하는 모델
- 그것이 실제로 물리적으로 동시에 실행되든 안 되든, 모델은 독립적이다
- 겹친 흐름을 해결하는 코드를 짜는 데에 사용되는 아키텍쳐이다
- 여러가지 종류를 가진다

---

### Thread & Lock

- Lock & Mutex로 공유 자원 보호
- 가장 기본적인 모델

```cpp
#include <pthread.h>
#include <stdio.h>

int shared = 0;
pthread_mutex_t lock;

void* inc(void* arg) {
    for(int i=0;i<100000;i++){
        pthread_mutex_lock(&lock);
        shared++;
        pthread_mutex_unlock(&lock);
    }
    return NULL;
}

int main(){
    pthread_t t1, t2;
    pthread_mutex_init(&lock, NULL);
    pthread_create(&t1, NULL, inc, NULL);
    pthread_create(&t2, NULL, inc, NULL);
    pthread_join(t1, NULL);
    pthread_join(t2, NULL);
    printf("%d\n", shared);
}
```

### Functional

- 상태 변화를 피하는 함수형 접근
- 상태 공유 문제 자체를 제거한다

```cpp
#include <stdlib.h>

int* map_inc(int* arr, int n){
    int* out = malloc(sizeof(int)*n);
    for(int i=0;i<n;i++){
        out[i] = arr[i] + 1;
    }
    return out;
}
// 새로운 메모리에 배열을 받아 사용함 (메모리가 겹치지 않음)
// arr는 readonly로 사용되어, 값이 변하지 않는다
```

### Message Passing

- 공유 메모리를 없앤다
- 스레드 또는 메시지로만 통신
- 각자 자기 메모리만 수정한다

```cpp
#include <pthread.h>
#include <stdio.h>

int queue[10];
int q_head = 0;

pthread_mutex_t qlock;

void send(int msg) {
    pthread_mutex_lock(&qlock);
    queue[q_head++] = msg;
    pthread_mutex_unlock(&qlock);
}

void* receiver(void* arg) {
    pthread_mutex_lock(&qlock);
    int msg = queue[--q_head];
    pthread_mutex_unlock(&qlock);

    printf("received %d\n", msg);
    return NULL;
}
```

### Event Loop

- 단일 스레드
- 이벤트 큐에 작업을 등록한다
- 준비되면 순서대로 처리한다

```cpp
#include <stdio.h>
#include <unistd.h>

void task1() {
    printf("task1\n");
}

void task2() {
    printf("task2\n");
}

int main() {
    while (1) {
        task1();   // 이벤트 1
        task2();   // 이벤트 2
        sleep(1);
    }
}
```
