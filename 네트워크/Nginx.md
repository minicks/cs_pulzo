## Nginx(engine x, 엔진 엑스)
- 웹 서버 소프트웨어, 가벼움과 높은 성능을 목표로 함
- 웹 서버, 리버스 프록시 및 메일 프록시 기능
- Dropbox, Netflix 등에서 사용

#### Apache와 차이점
- Apache : 오픈 소스, 크로스 플랫폼 HTTP 웹 서버 소프트웨어
- 전 세계에서 가장 인기있는 웹 서버

![Apache server](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FwqmcJ%2FbtqGdRXyk3j%2F4wKc51yhEUDyHnEN0QOdG0%2Fimg.png)

- Apache : 클라이언트로부터 받은 요청을 처리할 때 새로운 프로세스 또는 스레드를 생성하여 처리, 요청이 늘어날수록 CPU, 메모리 자원 소모 증가

![Nginx server](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FTPBD0%2FbtqGdDFarXK%2FjRtmeHaWYBJQQxsKYa4cKK%2Fimg.png)

- Nginx : Event-Driven 구조로 동작, 한 개 또는 고정된 프로세스만 생성하여 사용, 비동기 방식으로 요청들을 concurrency하게 처리
- 프로세스, 스레드 생성 비용이 없고, 적은 자원으로 효율적 운영 가능
- 단일 서버에서도 많은 연결 처리 가능

#### 왜 Nginx
- 리버스 프록시를 통하여 서버 앞단에서 요청을 처리
    - 앞단에서 처리하는 과정으로 보안적인 부분 향상 가능
    - 웹 어플리케이션이 DB와 대부분 직접적으로 연결되어 있어 최전방에 있으면 보안에 취약해짐
- 스위치 역할을 할 수 있음
    - 프로세스 응답 대기를 막고, 요청 분배 등

#### 기존 웹 서버와 차이점
- 동시에 처리할 수 있는 연결 수를 비약적으로 증가시킴
- 설계를 다음과 같은 방식으로 구현
    - 고정된 수의 worker 프로세스만 관리
    - 이 프로세스는 blocked 되지 않고,, listen소켓과 connection소케의 이벤트 기반으로 non-blocking으로 동작

![기존 web](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_blocking.png)

- 기존에는 precess per connection 또는 thread per connection 방식으로 동작
- listen socket을 통해 요청 받는 것은 여러 개의 listen socket을 non-blocking으로 수행하지만, 실제 connection socket을 통해 처리하는 과정이 blocking 방식으로 수행됨

![Nginx web](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_nonblocking.png)

- 연결을 전담으로 하는 프로세스, 스레드를 두지 않음
- config에 지정된 수의 worker 프로세스만 고정되어 있고, woker 프로세스들이 listen socket, connection socket 2개의 이벤트를 모두 처리

## 리버스 프록시

#### 프록시 서버
![Proxy server](https://upload.wikimedia.org/wikipedia/commons/thumb/2/27/Open_proxy_h2g2bob.svg/1920px-Open_proxy_h2g2bob.svg.png)

- 프록시 서버(proxy server) : 클라이언트가 자신을 통해서 다른 네트워크에 간접적으로 접속할 수 있게 해 주는 컴퓨터 시스템이나 응용 프로그램
- 보안, 접근 제안, 사용률 기록, 트래픽 분산 등을 위해 사용
- 클라이언트 호스트와 원격 리소스 사이에 프록시 서버를 배치하는 포워드 프록시, 인터넷 리소스 앞에 배치하는 리버스 프록시로 나뉘어짐

#### 리버스 프록시
![Reverse proxy](https://upload.wikimedia.org/wikipedia/commons/thumb/6/67/Reverse_proxy_h2g2bob.svg/1920px-Reverse_proxy_h2g2bob.svg.png)

- 실제 서버를 감추는 역할과 함께 로드 밸런서 역할도 수행 가능
- 클라이언트와 Nginx가 HTTP 통신을, 그리고 Nginx가 웹 어플리케이션과 HTTP 통신을 진행
    - Django의 경우 Nginx가 gunicorn과 HTTP 통신을, gunicorn과 Django가 WSGI 통신을 함
    - WSGI(Web Server Gateway Interface) : 파이썬에서 웹 서버와 통신하기 위한 인터페이스

## Nginx 사용하기
- nginx.conf : Nginx의 작동하는 방식을 결정하는 구성파일로, Nginx 설치시 `/etc/nginx/nginx.conf`에 위치
- 파일의 작성과 관련한 내용보다 어떠한 설정을 할 수 있는지를 위주로 작성

#### nginx.conf

- worker_processes : 발생하는 이벤트를 처리하는 프로세서의 수로 일반적으로 CPU의 core수만큼 할당하고 auto로 설정하면 자동으로 설정
- events : 네트워크 동작 방법과 관련한 설정
    - worker_connections : 하나의 프로세서가 동시에 몇 개의 연결을 처리할 수 있는지를 의미하고 보통 512 또는 1024로 설정
    - use epoll : epoll 방식으로 이벤트를 처리해 줌
        - epoll : linux 소켓을 관리하는 방법중 하나로, 이외에도 poo, select 방식이 있음
        - epoll 방식은 Nginx의 모든 소켓 파일을 찾아보는게 아니라 현재 활성화 된 소캣만 확인해서 연결을 설정하는 방식, poll 방식에서 업그레이드된 방식
- http : nginx로 들어오는 웹 트래픽 처리 방법, 방향을 지정
    - upstream : `upstream 'HOST이름'`형태로 작성
        - URI라우팅에 사용되는 server의 통합 닉네임
        - load balancing 방식으로 기본적으로 round-robbin을 사용하지만, least_conn으로 클라이언트와 가장 적게 연결된 서버 순으로 연결, ip_hash로 클라이언트 IP를 hash해서 특정 클라이언트는 특정 서버로 연결하는 등 설정 가능
        - weight=5 형식으로 가중치를 두면, 5번 연결 후 다은 서버로 넘기는 설정 가능
        - slow_start=30s 형식으로 슬로우 스타트 설정 가능
        - backup 으로 모든 서버가 오류 상태일 때 동작하는 서버 설정 가능
    - server : 서버 상에서 2개 이상의 웹 사이트를 실행할 수 있음
        - 사이트 정적 문서 루트 지정, 각 사이트별 별도 보안 정책 지정, 오류 페이지 통일, 각 사이트별 서로 다른 SSL 인증서 사용 등 작업 가능

#### Nginx 내부 구조

###### 프로세스 모델

![프로세스 모델](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_process-model.png)

- 1개의 master 프로세스와 3종류의 자식 프로세스로 구성
    - master process : 특권 명령을 수행(privileged operations)
        - listen socket에 port 바인딩
        - Nginx 설정 읽기
        - 자식 프로세스 생성
    - child process
        - cache loader : 디스크 기반 캐시를 메모리에 불러오고 종료되는 프로세스로 Nginx 시작시 실행됨
            - 보수적으로 스케줄링, 리소스 요구사항 낮음
        - cache manager : 주기적으로 실행되어, 디스크 캐시를 설정된 사이즈로 유지하기 위하여 캐시 엔트리를 정리
        - worker : 모든 작업을 처리
            - 네트워크 연결, 디스크에 컨텐츠를 read / write, upstream server와 통신 등

```
# service nginx restart
* Restarting nginx
# ps -ef --forest | grep nginx
root     32475     1  0 13:36 ?        00:00:00 nginx: master process /usr/sbin/nginx 
                                                -c /etc/nginx/nginx.conf
nginx    32476 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32477 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32479 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32480 32475  0 13:36 ?        00:00:00  _ nginx: worker process
nginx    32481 32475  0 13:36 ?        00:00:00  _ nginx: cache manager process
nginx    32482 32475  0 13:36 ?        00:00:00  _ nginx: cache loader process
```
- 다음과 같은 방식으로 확인할 수 있음

###### worker 프로세스
- Nginx의 worker는 싱글 스레드로 독릭접으로 실행
- worker 프로세스들은 문맥 전환을 줄이기 위해 non-blocking 방식으로 동작
- shared cache data, session persistance data, other shared resources 방법으로 공유 메모리를 통하여 정보 공유 가능

###### worker 내부 구현

![worker](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_worker-process.png)

- worker 프로세스틑 Nginx 설정에 따라 초기화되고, master process에 의해 listen socket을 제공받음
- 새로운 connection 요청이 들어오면 이벤트가 발생, connection 종류에 따라 알맞은 상태 기계에 할당
    - HTTP state machine
    - Stream state machine (raw TCP)
    - Mail state machine (SMTP, IMAP, POP3)

![state machine](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_request-flow.png)

- 각 state machine은 어떻게 요청을 처리해야하는지 알려주는 명령어의 집합

###### 무중단 설정변경, Nginx binary 업데이트

![](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_load-config-1.png)

![](https://www.nginx.com/wp-content/uploads/2015/06/infographic-Inside-NGINX_load-binary.png)

## 참조
- https://ko.wikipedia.org/wiki/Nginx
- https://ko.wikipedia.org/wiki/%EC%95%84%ED%8C%8C%EC%B9%98_HTTP_%EC%84%9C%EB%B2%84
- https://docs.microsoft.com/ko-kr/troubleshoot/developer/webapps/aspnetcore/practice-troubleshoot-linux/2-2-install-nginx-configure-it-reverse-proxy
- https://icarus8050.tistory.com/57
- https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%EC%84%9C%EB%B2%84
- https://juneyr.dev/nginx-basics
- https://www.nginx.com/blog/inside-nginx-how-we-designed-for-performance-scale/
- https://livlikwav.github.io/study/NGINX-inside/