# IPC(Inter Process Communication)

- 프로세스 간 통신
- 프로세스들 사이에 서로 데이터를 주고 받는 행위, 그에 대한 방법이나 경로 (-위키백과-)
- 같은 컴퓨터 내의 프로세스 간 통신, 다른 컴퓨터의 프로세스 간 통신
- 커널이 IPC 통신하는 방법을 제공

# 종류

## 파이프(PIPE)

- 통신을 위한 메모리 공간(버퍼)를 생성하여 프로세스가 데이터를 주고 받게 해줌.

### 익명 파이프

![https://t1.daumcdn.net/cfile/tistory/247CBC4357187A3411](https://t1.daumcdn.net/cfile/tistory/247CBC4357187A3411)

[출처](https://jwprogramming.tistory.com/54)

- 두 개의 프로세스를 연결.
- 하나는 쓰기만, 하나는 읽기만 가능함. (단방향 통신)→ 단순한 데이터 흐름을 가질 때 효율적.
- FIFO 구조
- 통신할 프로세스를 명확하게 알 수 있을 때 사용. (부모- 자식 프로세스 간 통신). 외부 프로세스에서 사용 불가능.
- 송수신 하고 싶으면, 파이프를 두 개 써야 함. → 구현이 복잡, 많은 프로세스가 통신할 경우 낭비 심함.

![https://t1.daumcdn.net/cfile/tistory/99E1BC3359FC780518](https://t1.daumcdn.net/cfile/tistory/99E1BC3359FC780518)

[출처](https://mangkyu.tistory.com/9)

### 명명된 파이프(Named PIPE)

- 익명 파이프가 확장된 상태(FIFO 구조)
- 통신할 프로세스를 모를 수도 있음. 서로 관련 없는 외부 프로세스와 통신 가능.
- 반이중 통신(읽기, 쓰기 가능하지만 한번에 한 방향으로만 통신 가능) → 전이중통신하고 싶으면 2개 파이프 필요.

### 메시지 큐(Message Queue)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile4.uf.tistory.com%2Fimage%2F9936B1335B975B8105D210](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile4.uf.tistory.com%2Fimage%2F9936B1335B975B8105D210)

[출처](https://doitnow-man.tistory.com/110)

- 메모리를 사용한 PIPE
- FIFO 구조, 단방향
- 메시지 큐에서 쓸 데이터에 번호를 붙여, 여러 프로세스가 동시에 데이터를 다룰 수 있다.

### 공유 메모리(Shared Memory)

- 프로세스 간에 메모리 영역을 공유
- 공유 메모리는 커널에서 관리함(프로세스가 커널에 공유 메모리 할당 요청. 커널이 메모리 공간 할당. 다른 프로세스가 접근 가능)

![https://postfiles.pstatic.net/20110313_253/akj61300_1299955250738qVkol_JPEG/K-22.jpg?type=w2](https://postfiles.pstatic.net/20110313_253/akj61300_1299955250738qVkol_JPEG/K-22.jpg?type=w2)

[출처](https://blog.naver.com/akj61300/80126200460)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile28.uf.tistory.com%2Fimage%2F995C864E5B9766171D9786](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile28.uf.tistory.com%2Fimage%2F995C864E5B9766171D9786)

[출처](https://doitnow-man.tistory.com/110)

- 대량의 정보를 다수의 프로세스에 배포 가능
- 양방향
- 빠름
- 공유 메모리 공간에 대한 접근 제어가 필요

### 메모리 맵(Memory Map)

- 메모리를 공유
- 파일을 프로세스 메모리에 맵핑해서 사용(공유 매개체가 파일+메모리)
- 주로 파일로 대용량 데이터 공유 시 사용

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile27.uf.tistory.com%2Fimage%2F9951304F5B9863F82D94DD](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile27.uf.tistory.com%2Fimage%2F9951304F5B9863F82D94DD)

[출처](https://doitnow-man.tistory.com/110)

### 소켓(Socket)

- 원격 컴퓨터와 연결을 의미하는 파이프 형태의 연결
- 서로 다른 컴퓨터에서 프로세스 간 데이터를 공유할 때 사용
- 클라이언트-서버 구조
- 양쪽 컴퓨터(IP 주소)에서 임의의 포트(파이프)를 정하고, 해당 포트 간 소통을 통해 데이터 주고 받음(양방향)

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcoRU8V%2FbtqUYHzqKoF%2FaukvQle0MCQnf1hcMAblJ1%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcoRU8V%2FbtqUYHzqKoF%2FaukvQle0MCQnf1hcMAblJ1%2Fimg.png)

[출처](https://cotak.tistory.com/45)

### 참고 자료

[https://www.youtube.com/watch?v=BW3Cr0-MFxE](https://www.youtube.com/watch?v=BW3Cr0-MFxE)

[https://doitnow-man.tistory.com/110](https://doitnow-man.tistory.com/110)

[https://gyoogle.dev/blog/computer-science/operating-system/IPC.html](https://gyoogle.dev/blog/computer-science/operating-system/IPC.html)

[https://jwprogramming.tistory.com/54](https://jwprogramming.tistory.com/54)

[https://mangkyu.tistory.com/9](https://mangkyu.tistory.com/9)