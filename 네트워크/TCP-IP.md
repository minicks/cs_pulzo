# TCP/IP
- Transmission Control Protocol/Internet Protocol

## 프로토콜
- 장비 사이에서 메시지를 주고 받는 양식과 규칙 체계

## TCP/IP
- 인터넷 프로토콜 중 가장 중요한 TCP와 IP를 합쳐 부르는 용어로, 인터넷 동작의 가장 중심이 되는 통신규약
- 데이터 흐름 관리, 정확성 확인을 위한 TCP, 패킷을 목적지까지 전송하는 IP
- IP주소 체계를 따르고, IP routing을 이용해 목적지에 도달, TCP의 특성을 활용해 송신자, 수신자의 논리적 연결을 생성하고 신뢰성을 유지할 수 있도록 하겠다는 의미

# TCP/IP 4 Layers
![TCP/IP 4 Layers](https://blog.kakaocdn.net/dn/uSn7R/btq9ml8Irna/cFTH47v7ynIR2UO9q9Tw70/img.png)

- TCP/IP 4 계층은 OSI 7계층과 비교할 수 있음

## [OSI 7 계층](osi7layer)
- 국제표준화 기구에서 개발, 네트워크 프토토콜 디자인과 통신을 계층으로 나눈 것
- 하위 계층은 하드웨어, 상위 계층은 소프트웨어

## TCP/IP 4 계층
- OSI 모델을 기반으로, 상업적, 실무적으로 이용할 수 있게 단순화된 모형
- 실제 TCP와 IP만 생각하면 OSI 3, 4 계층에 해당함

### 1계층 Network Interface
- 물리적으로 테이터가 네트워크에 어떻게 전송하는지 정의
- 물리적 주소로 MAC을 사용, 데이터는 프레임 단위로 구성

### 2계층 Internet
- 네트워크상 최족 목적지까지 연결되도록 연결성을 제공
- 단말을 구분하는 주소로 IP를 사용
- ex) IP

### 3계층 Transport
- 통신간의 노드 연결 제어, 신뢰성 있는 데이터 전송하는 계층
- ex) TCP, UDP

### 4계층 Application
- 사용자 인터페이스 역할을 담당
- ex) FTP, HTTP

# TCP
- Transmission Control Protocol
- 두 호스트가 교환할 때, 데이터, 승인 메시지 형식을 정의하고, 데이터 간 신뢰성 있는 전달을 위한 규격
- 데이터 패킷에 일련 번호를 부여하여, 데이터 손실을 찾아내 교성, 순서 재조합을 통하여 전달할 수 있게함

# IP
- Internet Protocol
- OSI 네트워크 계층에서 호스트 주소 지정, 패킷 분할 및 조립 기능 담당
- 비신뢰성, 비연결성의 특징
	- 비신뢰성 : 흐름에 관여하지 않기 때문에, 정보가 제대로 도착했는지 보장하지 않음
- 현재 사용하는 IP 버전은 IPv4, IPv6
	- IP 0부터 3버전은 1977~1979년 사용되었고, 실험적 버전

## IPv4
- 전 세계적으로 사용된 첫 번째 인터넷 프로토콜
- 총 12자리(32비트)로 구성, 네부분으로 나뉘어 지고, 각 부분은 0~255까지의 3자리수로 표현
- 고갈 우려로 인하여 IPv6가 등장, 2011년 2월 4일부터 IPv4주소가 소진되어 할당 중지
- 클래스 
	- A 클래스 (1.0.0.1 ~ 126.255.255.254)
	- B 클래스 (128.0.0.1 ~ 191.255.255.254)
	- C 클래스 (192.0.0.1 ~ 233.255.255.254)

## IPv6
- IPv4의 소진 및 한계로 인해 제안되었고, 대부분의 운영체제에서 지원
- 특징
	- 128비트 길이
	- 호스트 자동 지정 : IPv6 네트워크게 접속하는 순간 자동적으로 네트워크 주소 부여받음
	- 패킷 크기 확장
	- 효율적 라우팅

# 참조
- [wikipedia-프로토콜](https://ko.wikipedia.org/wiki/%ED%86%B5%EC%8B%A0_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
- [OSI & TCP/IP](https://tgyun615.com/60)
- [wikipedia-TCP](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
- [wikipedia-IP](https://ko.wikipedia.org/wiki/%EC%9D%B8%ED%84%B0%EB%84%B7_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
	- [wikipedia-IPv4](https://ko.wikipedia.org/wiki/IPv4)
	- [wikipedia-IPv6](https://ko.wikipedia.org/wiki/IPv6)
