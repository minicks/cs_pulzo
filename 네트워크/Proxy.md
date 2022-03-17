# 발표 정리

# Proxy

- 대리, 대리인, 대용물(네이버 영어 사전)
- 스프링의 프록시 패턴, 네트워크의 프록시 등 → 네트워크의 프록시
    - 참고) 스프링의 프록시 패턴: 프록시 객체가 원래 객체를 감싸서 클라이언트의 요청을 처리하게 하는 패턴
- 프록시 서버: 프록시 역할을 하는 서버(대리인 역할을 하는 서버)
    - 클라이언트의 대리인 역할: forward proxy
    - 서버의 대리인 역할: reverse proxy

# Forward proxy

[https://t1.daumcdn.net/cfile/tistory/990743455A43A1A109](https://t1.daumcdn.net/cfile/tistory/990743455A43A1A109)

(출처: [https://yunyoung1819.tistory.com/9](https://yunyoung1819.tistory.com/9))

- 클라이언트와 인터넷 사이에 위치
- 클라이언트 대신 서버에게 요청 보냄. 서버에게서 받은 응답을 클라이언트에게 줌.
1. 캐시를 통한 자원 저장 → 응답 시간 감소, 네트워크 병목 현상 방지
2. 익명성(개인 식별 정보 헤더를 서버에 전하지 않을 수 있음) → 개인 정보 보호
3. 필터링, 로깅
    
    예) 학교→ 교육용 사이트만 O.
    

# Reverse Proxy

[https://t1.daumcdn.net/cfile/tistory/992759465A43A1DA30](https://t1.daumcdn.net/cfile/tistory/992759465A43A1DA30)

([https://yunyoung1819.tistory.com/9](https://yunyoung1819.tistory.com/9))

- 인터넷과 서버 사이에 위치
- 서버 앞에 위치하여, 서버로 향하는 요청 처리
1. 캐시를 통한 자원 저장
2. 보안(서버 정보를 클라이언트에게 숨김)
3. 로드 밸런싱(Load Balancing. 부하 분산)
    
    서버에게 온 요청을 여러 대 서버에게 나눠주는 것.
    
    동작하는 계층에 따라 보통 4, 7 계층으로 나눔. 
    
    1. L4 로드 밸런싱(IP+포트 번호로)
        
        
        ![https://post-phinf.pstatic.net/MjAxOTEyMTBfNCAg/MDAxNTc1OTU1MzY3OTM2.nG91HOEOh6Sc1AuUgbN3O4pcnEI-rh24UKSrrrjkrcsg.VcG18MidW4az7Oh0RQfRPLDBHNRyGayE1BsQxDImL3Ig.JPEG/L4-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200](https://post-phinf.pstatic.net/MjAxOTEyMTBfNCAg/MDAxNTc1OTU1MzY3OTM2.nG91HOEOh6Sc1AuUgbN3O4pcnEI-rh24UKSrrrjkrcsg.VcG18MidW4az7Oh0RQfRPLDBHNRyGayE1BsQxDImL3Ig.JPEG/L4-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200)
        
        ([https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903](https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903))
        
    2. L7 로드 밸런싱(IP+포트번호+URI, http header, cookie 등)
        
        
        ![https://post-phinf.pstatic.net/MjAxOTEyMTBfMjA1/MDAxNTc1OTU1MzgxODY5.odnG4CRES0e5bH7sOKyWRP1c8uO_XC4VX9A3HPeI1JQg.lNL2eJYbMz6NX1e5YFzfHDMQHn4YrdOJR2VYHmq5e1Ig.JPEG/L7-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200](https://post-phinf.pstatic.net/MjAxOTEyMTBfMjA1/MDAxNTc1OTU1MzgxODY5.odnG4CRES0e5bH7sOKyWRP1c8uO_XC4VX9A3HPeI1JQg.lNL2eJYbMz6NX1e5YFzfHDMQHn4YrdOJR2VYHmq5e1Ig.JPEG/L7-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200)
        
        ([https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903](https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903))
        

예시)

**URI에 따라 다른 서버로 연결**

![%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%208cf9a/Untitled.png](%E1%84%87%E1%85%A1%E1%86%AF%E1%84%91%E1%85%AD%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%208cf9a/Untitled.png)

(출처: 공통 PJT 팀 노션- 효전님)

**무중단 배포**

![https://postfiles.pstatic.net/MjAxODA5MjBfMjMw/MDAxNTM3NDIyNzIzOTcx.Diez1l4rZp-2yu5TWTHVHs87y8i4Ho0X_OPFzyFcFq8g.qjuXnsRijiseJtUKjYmxxm909x_m5wVRGgOCOBCVlfQg.PNG.songintae92/image_4422194461537422699876.png?type=w966](https://postfiles.pstatic.net/MjAxODA5MjBfMjMw/MDAxNTM3NDIyNzIzOTcx.Diez1l4rZp-2yu5TWTHVHs87y8i4Ho0X_OPFzyFcFq8g.qjuXnsRijiseJtUKjYmxxm909x_m5wVRGgOCOBCVlfQg.PNG.songintae92/image_4422194461537422699876.png?type=w966)

(출처:[https://blog.naver.com/songintae92/221362831110](https://blog.naver.com/songintae92/221362831110))

배포할 때 변경 사항 있는데 서버가 하나라면 잠깐이지만 서버가 중단됨. 

서버에 서로 다른 포트로 사이트를 띄운 후에, Nginx의 reverse proxy를 이용하여 포트를 번갈아가면서 접근하게 하면 됨. 

# 참고 자료

[https://www.youtube.com/watch?v=YxwYhenZ3BE](https://www.youtube.com/watch?v=YxwYhenZ3BE)

[https://www.youtube.com/watch?v=lg-wHikZg0Q](https://www.youtube.com/watch?v=lg-wHikZg0Q)

[https://www.youtube.com/watch?v=u4O4zHdiFhk](https://www.youtube.com/watch?v=u4O4zHdiFhk)

→ 테코톡 유튜브 

[https://ko.wikipedia.org/wiki/프록시_서버](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%EC%84%9C%EB%B2%84)

[https://yunyoung1819.tistory.com/9](https://yunyoung1819.tistory.com/9)

[https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=songintae92&logNo=221362831110](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=songintae92&logNo=221362831110)

→ 무중단 배포

[https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903](https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903) → 로드 밸런싱

[https://github.com/minicks/cs_pulzo/blob/main/네트워크/Nginx.md](https://github.com/minicks/cs_pulzo/blob/main/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/Nginx.md)

→ nginx 발표 by 영준님