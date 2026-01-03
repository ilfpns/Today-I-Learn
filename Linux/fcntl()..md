⇒ 파일 컨트롤 함수

⇒ 파일 디스크립터의 행동 규칙을 바꾼다

# fd?

⇒ file Descriptor

⇒ 커널이 관리하는 I/O 대상의 번호

```css
0 -> stdin
1 -> stdout
2 -> stderr
3~ -> 파일, 소켓, 디바이스, 파이프 ...
```

### 예제

| 대상 | fd 예 |
| --- | --- |
| 파일 | `open()` |
| 소켓 | `socket()` |
| 파이프 | `pipe()` |
| 디바이스 | `/dev/...` |

```c
fcntl(fd, cmd, args ...);
// file descriptor, cmd, etc...
fcntl(fd, f_GETFL, 0); 
// 현재 파일 조회, 뒤 args는 사용하지 않음
```

```c
int flags = fcntl(fd, F_GETFL, 0);
fcntl(fd, F_SETFL, flags | O_NONBLOCK);
// fd의 정보를 가져옴, 이를 비트마스킹 후 다시 저장
```

### 다양한 플래그

| 플래그 | 의미 |
| --- | --- |
| `O_RDONLY` | 읽기 전용 |
| `O_WRONLY` | 쓰기 전용 |
| `O_RDWR` | 읽기/쓰기 |

| 플래그 | 의미 |
| --- | --- |
| `O_NONBLOCK` | 논블로킹 |
| `O_APPEND` | write 시 항상 파일 끝 |
| `O_SYNC` | 동기 I/O |
| `O_DIRECT` | 페이지 캐시 우회 |
| `O_CLOEXEC` | (open 시) exec 후 close |

### CMD 명령

| cmd | 의미 |
| --- | --- |
| `F_GETFL` | 상태 플래그 조회 |
| `F_SETFL` | 상태 플래그 설정 |
| `F_GETFD` | fd 플래그 조회 |
| `F_SETFD` | fd 플래그 설정 |
