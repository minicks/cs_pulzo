# DNS

### Intro

host: 인터넷에 연결된 각각의 장치 

→ 통신하려면 IP주소 필요함.

DNS: Domain Name System. 

도메인 주소를 IP 주소로 반환하는 역할.

- IP 주소를 기억하지 않아도 됨.
- 서버 IP 주소 변경에 쉽게 대처 가능.

![Untitled](DNS%204a9f8/Untitled.png)

이미지 출처: [https://cnu-jinseop.tistory.com/77](https://cnu-jinseop.tistory.com/77)

### 구조

- 계층, 역트리 구조
- 상위 레벨의 DNS 서버는 바로 하위 레벨의 DNS 서버 목록, ip 주소를 알고 있음.

![https://t1.daumcdn.net/cfile/tistory/997DA9405BDFB7B71E](https://t1.daumcdn.net/cfile/tistory/997DA9405BDFB7B71E)

이미지 출처: [https://ijbgo.tistory.com/27](https://ijbgo.tistory.com/27)

- 경계는  ‘.’으로 구분(마지막 .은 생략됨)
- 알파벳, 숫자, - 만 사용 가능

- 루트 도메인
    - ‘.’ (www.naver.com.)
    - 도메인을 구성하는 최상위 영역
    - 전세계 13개
    
    [https://ko.wikipedia.org/wiki/루트_네임_서버](https://ko.wikipedia.org/wiki/%EB%A3%A8%ED%8A%B8_%EB%84%A4%EC%9E%84_%EC%84%9C%EB%B2%84)
    

- TLD(Top-Level Domain)
    - 최상위 도메인
    - 6가지 유형. 도메인 성격에 따라 분류.
        - gTLD(Generic) : 일반적으로 사용. (com, net, org, edu, gov, mil)
        - ccTLD(Country Code) : 국가 최상위 도메인. (kr)
        - sTLD(Sponsored): 전문가 집단, 민족 공동체 등(.asia, .museum)
        - Infrastructure : 중요한 인프라
        - grTLD(Generic-restricted): 특정 기준을 충족하는 사람, 단체(.name, .pro)
        - tTLD(test): 개발 테스트 용(.test)
        

### 동작 방식

- 로컬에 있는 DNS 캐시 정보 확인
    - 동적 DNS 캐시: 이전 조회를 통해 저장
    - 정적 DNS 캐시: hosts 파일
    - `ipconfig /displaydns`
    
- DNS 캐시에 원하는 정보가 없다면, DNS서버로 쿼리
    
    ![https://media.vlpt.us/images/goban/post/5717ceb7-79f2-41d3-86e5-7e48bfd6ac58/DNSLogic.png](https://media.vlpt.us/images/goban/post/5717ceb7-79f2-41d3-86e5-7e48bfd6ac58/DNSLogic.png)
    
    이미지 출처: [https://velog.io/@goban/DNS와-작동원리](https://velog.io/@goban/DNS%EC%99%80-%EC%9E%91%EB%8F%99%EC%9B%90%EB%A6%AC)
    
    1. 사용자가 브라우저에 www.naver.com이라는 주소를 검색
    2. 맨 처음에 로컬 dns 서버를 만남. (디폴트로 가입한 통신사(인터넷 서비스 제공자 = ISP)가 제공하는 DNS 서버로 연결됨. - [https://ko.wikipedia.org/wiki/도메인_네임_시스템](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C) 마음에 안 드는 경우(속도가 느리거나, 프라이버시가 침해된다고 생각하는 등), 다른 public dns를 사용할 수 있음. - [구글의 public dns](https://developers.google.com/speed/public-dns),  [1.1.1.1 public dns](https://1.1.1.1/ko-KR/dns/) 등이 있음. 단, 본인이 신뢰할 수 있다고 생각하는 DNS 서버를 사용해야 함!)
        
        이 로컬 서버가 Root DNS 서버에게 www.naver.com 에 대해 물어봄
        
    3. Root DNS 서버는 .com을 관리하는 top level DNS 서버의 정보를 로컬 DNS 서버에게 알려줌
    4. 로컬 DNS 서버는 .com을 담당하는 top level DNS 서버에게 www.naver.com 에 대해 물어봄.
    5. top level DNS 서버는 naver.com을 담당하는 DNS 서버의 정보를 로컬 DNS 서버에게 알려줌.
    6. 로컬 DNS 서버는 naver.com을 담당하는 DNS 서버에게 www.naver.com 에 대해 물어봄.
    7. 이번에 만난 DNS 서버는 www.naver.com 의 IP주소를 알고 있어서, 이를 로컬 DNS 서버에게 알려줌. DNS 는 이 정보를 로컬 캐시에 저장함.
    8. 클라이언트에게 IP 주소를 알려줌. → 이 IP주소를 활용해서 네이버 사이트에 접속할 수 있음.
    

참고)

**TTL**

Time To Live

결괏값을 캐시에서 유지하는 시간

길면? 응답 시간 감소, DNS 서버 부하 감소 ↔ 도메인 관련 정보 변경 시 정보 갱신 느림 

→ 서비스 특성에 맞게 조정하기.

**hosts**

운영체제가 호스트 이름을 ip주소에 매핑할 때 사용하는 컴퓨터 파일. plain text 파일. ([](https://ko.wikipedia.org/wiki/Hosts))

보안 이슈(예- naver.com을 입력했는데, 사기꾼의 ip주소로 연결되는 등)

### DNS 주요 레코드

- A: 도메인 주소를 IP주소(IPv4)로 매핑
- AAAA : 도메인 주소를 IP주소(IPv6)로 매핑
- CNAME(Canonical Name): 도메인 주소에 대한 별명 - 예)www.naver.com, naver.com
- NS(Name Server): 호스팅 영역의 네임 서버

### 참고 자료

[DNS가 뭔가요? + 도메인, A Record, CName](https://www.youtube.com/watch?v=6fc9NAQkcv0)

[WEB2-Domain Name System-6.DNS의 원리](https://www.youtube.com/watch?v=iM07I1X7qkg)

[hosts - 위키백과, 우리 모두의 백과사전](https://ko.wikipedia.org/wiki/Hosts)

IT 엔지니어를 위한 네트워크 입문(고재성, 이상훈 저/ 길벗)
