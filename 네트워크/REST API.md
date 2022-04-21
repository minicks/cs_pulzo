<div align='center'>
    <h1>
        REST API
    </h1>
</div>



## 목차



1. [API](#1)

2. [HTTP API](#2)
3. [REST](#3)
4. [REST API](#4)
5. [RESTful API](#5)
6. [참조](#6)



<div id="1">

## 1. API(**Application Programming Interface**)

#### 위키

**API(응용 프로그램 프로그래밍 인터페이스)**는 컴퓨터나 컴퓨터 프로그램 사이의 연결

일종의 소프트웨어 인터페이스이며 다른 종류의 소프트웨어에 서비스를 제공

컴퓨터와 인간을 연결시키는 **UI(사용자 인터페이스)**와 반대로, **API**는 컴퓨터나 소프트웨어를 서로 연결

<hr>

#### 블로그

애플리케이션(응용프로그램)에서 사용할 수 있도록, 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스

즉, 애플리케이션이 어떤 프로그램이 제공하는 기능을 사용할 수 있게 만든 매개체

API의 한 가지 목적은 서버 시스템이 동작하는 방식에 관한 내부의 프로세스를 숨기는 것으로, 내부의 세세한 부분이 나중에 변경되더라도 프로그래머가 유용하게 사용할 수 있고 일정하게 관리할 수 있는 부분들만 노출



<div id='2'>

## 2. HTTP API

HTTP를 사용하여 프로그램끼리 소통하는 API

OPEN API, facebook API, kakao API 등의 대부분 API는 HTTP라는 통신 규칙으로 소통하는 API



그렇다면 HTTP를 사용하지  않는 API는?

IoT 환경에서 사용하는 MQTT, CoAP프로토콜 같은 것들이 있음.

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfX3e8%2FbtrobTrD4pA%2F011IGrAdyBWe5bQM3t0uy0%2Fimg.png)

<div id='3'>

## 3. REST(REpresentational State Transfer)

#### 정의

"**RE**presentational **S**tate **T**ransfer"

자원을 이름(자원의 표현)으로 구분해 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미합니다.

즉, **자원(resource)**의 **표현(representation)**에 의한 **상태 전달**을 뜻합니다.

- **자원** **:** 해당 소프트웨어가 관리하는 모든 것 ( 문서, 그림, 데이터, 해당 소프트웨어 자체 등 )
- **표현 :** 그 자원을 표현하기 위한 이름 ( DB의 학생 정보가 자원이면, 'students'를 자원의 표현으로 정함 )
- **상태 전달 :** 데이터가 요청되는 시점에 자원의 상태를 전달한다. ( JSON 혹은 XML을 통해 데이터를 주고 받는 것이 일반적 )

REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용

**웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일**

REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나



#### 개념

어떤 자원에 대해 CRUD(Create, Read, Update, Delete) 연산을 수행하기 위해 **URI(Resource)**로

GET, POST 등의 **방식(Method)**을 사용하여 요청을 보내며

요청을 위한 자원은 **특정한 형태(Representation of Resource)**로 표현



#### 구성 요소

**1.** **자원(Resource) - URI**

- 모든 자원에는 고유한 ID가 존재하고, 이 자원은 Server에 존재합니다.
- 자원을 구별하는 ID는 '/exgroups/:exgroup_id'와 같은 HTTP URI 입니다.
- Client는 URI를 이용해 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청합니다.



**2. 행위(Verb) - Method**

- HTTP 프로토콜의 Method를 사용합니다.

- HTTP 프로토콜은 GET, POST, PUT, PATCH, DELETE의 Method를 제공합니다. ( CRUD )

  | GET    | Read : 정보 요청, URI가 가진 정보를 검색하기 위해 서버에 요청한다. |
  | ------ | ------------------------------------------------------------ |
  | POST   | Create : 정보 입력, 클라이언트에서 서버로 전달하려는 정보를 보낸다. |
  | PUT    | Update : 정보 업데이트, 주로 내용을 갱신하기 위해 사용한다. (데이터 전체를 바꿀 때) |
  | PATCH  | Update : 정보 업데이트, 주로 내용을 갱신하기 위해 사용한다. (데이터 일부만 바꿀 때) |
  | DELETE | Delete : 정보 삭제, (안전성 문제로 대부분 서버에서 비활성화한다.) |



**3. 표현 ( Representation of Resource )**

- Client와 Server가 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등이 있습니다.
- JSON, XML을 통해 데이터를 주고 받는 것이 일반적입니다.



#### 특징

**1. Server-Client (서버-클라이언트 구조)**

- 자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 됩니다.
  - REST Server는 API를 제공하고 비즈니스 로직 처리 및 저장을 책임지고,
  - Client는 사용자 인증이나 context( 세션, 로그인 정보 ) 등을 직접 관리하고 책임집니다.
  - 역할을 확실히 구분시킴으로써 서로 간의 의존성을 줄입니다.

**2. Stateless (무상태)**

- HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖습니다.
- Client의 context를 Server에 저장하지 않습니다.
  - 즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해집니다.
- Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리합니다.
  - 각 API 서버는 Client의 요청만을 단순 처리합니다.
  - 즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안됩니다. ( DB에 의해 바뀌는 것은 허용 )
  - Server의 처리 방식에 일관성을 부여하기 때문에 서비스의 자유도가 높아집니다.

**3. Cacheable (캐시 처리 기능)**

- 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있습니다.
  - 즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있습니다.
  - HTTP 프로토콜 표준에서 사용하는 Last-Modified Tag 또는 E-Tag를 이용해 캐싱을 구현합니다.
- 대량의 요청을 효율적으로 처리할 수 있습니다.

**4. Layered System (계층 구조)**

- Client는 REST API Server만 호출합니다.
- REST Server는 다중 계층으로 구성될 수 있습니다.
  - 보안, 로드 밸런싱, 암호화 등을 위한 계층을 추가하여 구조를 변경할 수 있습니다.
  - Proxy, Gateway와 같은 네트워크 기반의 중간매체를 사용할 수 있습니다.
  - 하지만 Client는 Server와 직접 통신하는지, 중간 서버와 통신하는지는 알 수 없습니다.

**5. Uniform Interface (인터페이스 일관성)**

- URI로 지정한 Resource에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍처 스타일을 의미합니다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하며, Loosely Coupling(느슨한 결함) 형태를 갖습니다. 
  - 즉, 특정 언어나 기술에 종속되지 않음

**6. Self-Descriptiveness (자체 표현)**

- 요청 메시지만 보고도 쉽게 이해할 수 있는 자체 표현 구조로 되어있습니다.



<div id='4'>

## 4. REST API

- REST의 특징을 기반으로 API를 제공하는 것

공공데이터, 구글 맵, 마이크로 서비스 등 대부분이 REST API를 통해 제공

HTTP 표준을 기반으로 구현하기 때문에 HTTP를 지원하는 프로그램 언어를 사용하여 클라이언트와 서버를 구현할 수 있다.

REST API의 가장 큰 특징은 <u>각 요청이 어떤 동작이나 정보를 위한 것인지를 그 요청의 모습 자체로 추론이 가능한 것</u> 입니다.

REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약합니다.

- **첫 번째,** URI는 정보의 자원을 표현해야 한다.
- **두 번째,** 자원에 대한 행위는 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다.
  - 행위(Method)는 URI에 포함하지 않는다.



#### 설계 규칙

1. URI는 정보의 자원을 표현해야 한다.(리소스명은 동사가 아닌 명사를 사용한다)
2. 자원의 행위는 HTTP 메소드(GET, POST, PUT, DELETE)로 표현한다.
3. 슬래시(/)는 계층 관계를 나타낼 때 사용한다.
4. 소문자를 사용한다.
5. 밑줄(_)은 사용하지 않고 하이픈(-)을 사용한다.
6. 확장자(.txt, .png 등)를 사용하지 않는다.
7. URI의 마지막에 슬래시(/)를 포함하지 않는다.



<div id='5'>

## 5. RESTful API

REST의 특징과 설계 규칙을 잘 지켜서 설계된 API를 **RESTful한 API**라고 합니다.

즉, **REST의 원리를 잘 따르는 시스템을 RESTful이란 용어로 지칭**

이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것을 목적으로 성능이 중요하다면 꼭 RESTful하게 구현할 필요는 없음.



<div id='6'>

## 6. 참조

[API 위키백과](https://ko.wikipedia.org/wiki/API)

[REST 위키백과](https://ko.wikipedia.org/wiki/REST)

[REST 블로그_1](https://dev-coco.tistory.com/97#REST%EC%-D%--%--%EA%B-%AC%EC%--%B-%--%EC%-A%--%EC%--%-C)

[REST 블로그_2](https://jy-tblog.tistory.com/24)

[HTTP REST 블로그](https://bentist.tistory.com/37)