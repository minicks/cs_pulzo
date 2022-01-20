# Cache

- 컴퓨터 과학에서 데이터나 값을 미리 복사해 놓는 임시 장소 by. wiki
- 일시적인 특징이 있는 데이터 하위 집합을 저장하는 고속 데이터 스토리지 계층 by. aws
- 속도가 빠른 장치와 느린 장치 사이에서 속도 차에 따른 병목 현상을 줄이기 위한 메모리(버퍼)



- 불필요한 데이터 통신을 줄여 네트워크 비용을 감소 

- 네트워크 병목 현상을 줄여 속도 향상

- 서버 접근 횟수를 줄여 서버 응답 속도 향상 및 과부하 방지



## 지역성

### 시간 지역성(Temporal Locality)

- 한 번 접근한 데이터는 가까운 미래에 다시 접근할 가능성이 높을 것

### 공간 지역성(Spatial Locality)

- 한 번 접근한 데이터와 가까이 있는 데이터는 접근할 가능성이 높을 것
- 메모리에 접근할 때 해당 주소를 포함하는 블록을 전부 캐시에 가져옴

### 순차 지역성(Sequential Locality)

- 한 번 접근한 데이터부터 순차적으로 접근할 가능성이 높을 것



## 캐시의 종류

- 캐시는 운영 체제, 네트워킹 계층(콘텐츠 전송 네트워크(CDN), DNS 등), 웹 애플리케이션 및 데이터베이스를 비롯한 다양한 기술 계층에 걸쳐 적용되고 활용

| **계층**      | **클라이언트 측**                                            | **DNS**                                            | **웹**                                                       | **앱**                                                       | **데이터베이스**                                             |
| ------------- | ------------------------------------------------------------ | -------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **사용 사례** | 웹 사이트에서 웹 콘텐츠를 검색하는 속도 가속화(브라우저 또는 디바이스) | 도메인과 IP 간 확인                                | 웹 또는 앱 서버에서 웹 콘텐츠를 검색하는 속도를 높입니다. 웹 세션 관리(서버 측) | 애플리케이션 성능 및 데이터 액세스 가속화                    | 데이터베이스 쿼리 요청과 관련한 지연 시간 단축               |
| **기술**      | HTTP 캐시 헤더, 브라우저                                     | DNS 서버                                           | HTTP 캐시 헤더, CDN, 역방향 프록시, 웹 액셀러레이터, 키-값 스토어 | 키-값 데이터 스토어, 로컬 캐시                               | 데이터베이스 버퍼, 키-값 데이터 스토어                       |
| **솔루션**    | 브라우저별                                                   | [Amazon Route 53](https://aws.amazon.com/route53/) | [Amazon CloudFront](https://aws.amazon.com/cloudfront/), [ElastiCache for Redis](https://aws.amazon.com/elasticache/redis/), [ElastiCache for Memcached](https://aws.amazon.com/elasticache/memcached), [파트너 솔루션](https://aws.amazon.com/marketplace/) | 애플리케이션 프레임워크, [ElastiCache for Redis](https://aws.amazon.com/elasticache/redis/), [ElastiCache for Memcached](https://aws.amazon.com/elasticache/memcached), [파트너 솔루션](https://aws.amazon.com/marketplace/) | [ElastiCache for Redis](https://aws.amazon.com/elasticache/redis/), [ElastiCache for Memcached](https://aws.amazon.com/elasticache/memcached) |

### CPU 캐시

![메모리 계층 구조 - 나무위키](https://ww.namu.la/s/893cc4cb9901911dd7fbf7e151f8768f0a10d00d6b50bc9ad2b634810c19723f7c5464bc7701d8cfbfa7a4c3027ec10198c1cfcb92b598bd0eccea6202beb28ad9241b19f65f819f678129b64a09348a)

- L1, L2, L3 캐시 메모리(Level)
  - L1: 프로세서와 가장 가까운 캐시, 8~64KB, CPU 내장
    - I$(Instruction Cache) : 메모리의 text 영역 데이터
    - D$(Data Cache) : text 영역을 제외한 데이터
  - L2: 용량이 큰 캐시, 64KB~4MB
  - (L3): 여러 코어가 공유, ~8MB, 성능에 영향 적음

![04.jpg](https://it.donga.com/media/itdonga/media/2010/05/19/04.jpg)



## 적중률(hit ratio)

![img](https://blog.kakaocdn.net/dn/cQPsmQ/btqQwojNc2Y/4vxPowyRkS2qSOZULZCvfk/img.png)

- 적중률 = 캐시 적중 수 / 전체 메모리 참조 횟수

![8장 캐시기억장치](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAfsAAABjCAMAAACrF1l6AAAB7FBMVEX///8AAAD///3///r8///3//////jX19f///f0///5//+rq6v05s7F4vivr6/7+/v///NISEiGhobMzMyampovLy9+fn5biarXupj/7tgAABLZ8PqujGcAAEllKgBVCgBcgae31evg+P/03L/MsI83NzePj4/IpoMAK1bq6up0mrtuRQAAAAnt+f/r///m5uZvQi0rT3y8vLw9AACMrtChwdv//+wAADwAABsANl4ZTHPx3sSEWTxTLB5JAAAAADU6bJRjPTEmAABaNC8AACUZIlbmyqqZcEZvSCIQO3Dx6N3DydHQy8Pf5ewAACzawqe6m30wAACtwNM+HDUfC0M0FDZGHCk7YozR2+XCrZlWJQDq4trA0eBjVUlXMhRLJRwALF8bAAAAEFAcGExTHwwnLFikpbOGd3h9kKp6iZWinphHXnRbd5OllYPLvrRGRFiJemghFzBaRlB+ZFkfACVlSi2IXSOihGyki5QvGhObkqGJiYKVdlZicoqch4A5S2kAIjc7DgBgTkxTWnBMXoQ7Iy6JZT0jAC1lOQlEPVRubHkJMVBCKionCiaRo7hZTEVfZ3w8CCBPNSNkLR4AHkGWbDtsREJ3WkvBrq+CZlEwOkdpTSk7AikAHDFxcIaCVkJ9XmVDIQBBBRRBNi+FSBR2AAAbcElEQVR4nO1di3/TRrYeS47txI6lxMZEJN1NcEgQxRhEYhrELikPE2QbG29b7CqwUNqEmMSkTdns3oSwPJqyKTftdnsX6L5ub//RO2dmJEvyI2nicOldfb9f4pc0mnO+OTNnRnOOEHLhwoULFy5cuHBhhzjTsWcle/eo5LZDaPDujUWtivLuCgrM9u+yKs2h3mn1K2fKwCX2rArbxMBcMBiM4r/K3fYUmA2Gw8ESbv+VsBKc6WpPoRT8UtSo7PzuSloeIi/agpMnLYhrXcRvqkElHM3tqPDh8RY/SveiVITgYqvDXgd8j4qyMOopCUL+dHtKFLSPJwQvNPCCp7irvoQ3DENgvaj0aUYWVs8eE4TC4E8si1OsVhZ6Cv/1aPjkfudxwoBnCGothDzzO6y9+FntWqYMhr0PPywJ4slJQdCm/q+5j4/hf30HcA/I/Ue7ynx7kr72Hd1dxxp6SBUnPmbllMFaB97CI3WqZb/aANyvrHW5RNSeTKBfOLnH5HgO0quePPJTK2xgtHamdI/KwC910y9mO/G/Xw7if/mhnZbfJpDWSLhv33hv517YebevPgFFBZam2WdSQ8J9s8o2vRj3roX71JfH6Bu+Bfcpwj23E8dCnai9p+TzrxjRxPw5wj16I3xCyv2OUQ0ylOhnG/fls8d2XrL6tAv5luz2QblvjPznzQSxcZ8+wd604p7YvXZ/7KfUlyF11XIx9R5uwMu2/p1x/0Zgl9yDdwcwuT/tJyhAseJvGPe/G6sN3HbAt5KnYRXyT72vHF1jK+7R+aaCvHuw9n50kr1pzP00qX32HNj9AONePNndrLOBb39nayL8L6x1Vh922qlvyX36ZtOf9gS75N6Jt09HCJZt3Ou47/t9Q9p+jw2DjzTurfO3nKNiK+75htznY7HYyh828P8iK2LQOJ5xX44ZKGLui6T2du65SAfKTztLJmWAn6TbZwR2N0495/DqWnGvlZr+tCcwuOf9/mCCr8aKXXx1Loc4f0SByVpJnUsg3V8F0TUlkoGGrkcimWbjla3Px9xnK0UvEapwIci0j/xypYh8/mwwgQoH4Nssbhq6ElEck97lFedszuRejyi4CrgMMpEkn7jz/dkK+ahFIorRRjRsxfp5sGbGkDlLMLjX/QZyDl9vYEwPR6FOekK9NRc0ahcR16bxWeFp5Fs9HJymjGWxTmgLtnO/0PvA3lxN7iOd2V5cTmUT64cJwkVwhXN6Zc/Wnhxg3IuPS+Ciih/j7k3FRK9hgV4NafevJWcThSNIut0B/Rcq/PEOym9ic2ICoIF9hwj2MYnt3P9QFPjVMaQ9GkfSRUOgvKdY3RQ/60cDuNz3OhFXvpJAw9h51x7bLBd3lsODyAaD+zJuMOvdoScJNIW7hoVpxL/o5m5sCtwq5kzF2qQTOQPW8X6YVXAbvt7AfA7lT0CF+9G60QXxhQvT5WJhDIVuelEc/6r9ME7HdJV4doEPuy0FYtXl7Q3Y4L7smZa1LzI5AVeZCRJYvYbUq3MleWASvRYw7tUinZ7AcKh0YaXLyeT6JBrFFQ1Eu1Dqkw50CXeB0uGO1Kc5Wc6/w3pzwQArzmH3WJXpSTKvqnFPplx5ej3gHqXeP0Z/Nf0wwDL0uA7yGffpa/ifr6uM2yfmpA+O4btIsZgM8VfTclL1WBiw+XrqRfZmG9zjGoh/Poj4v1i4x2bQicQZ/PoJ5R6Ey18jtYMCpc8t/m0BirGTb3Cf+rKTzjexMEwQFMfFrOOvUu+9nmW/2nivg9FIFw5K2OzXN5OkE2SzVa16uIOIpp7qTE+Qn5p0+s4+nxJl495HB2bOv1rjvo8oD1/cLKiwSV9sk3nGvTEQ44EKm8s67XLIeK+ewFXMQQducSFs3Iu/ZR+4Lef3hPsPDiKfnXsqiF6eqHE/QNSUhumdtf0O08r3zVuVZXD/Xo17Jgjh/swQKOT1cD/KLERXEoToS2NVXKl1pl3yVSBcArvnZ0u+xSGUvtxibur7kK0QDkOxrbjXlQ6L3VONSbU5YWiTvVmwrctcIQcY/lo1gy4NGXU1ub/inFjauGc84at+PFlX/QJThnQLrtCCezGcs9o9rVAaZF+tDfeSIUPZ4iiKJ+llbdxTQV4z92JlZCQKN5/Up0wr8T+CS5Y+BVeX0TD+KoBVF7rZhdnyy/hI8SpIJzdsANkoLq5Eix2Z6aLcTzLuDUukJEGLGMPcdxDuxd+C0kfrLdEKDSoLtVMvEDKhcthc0h/BKpDAnad9Pv8MxBCsc7KktbKpP8HhWnQkFhspIivM8qsgRq4p911IPH8QxQ8jk/vQd1AmdEDSw9arNlWmIRv3TJDXbvcM8QMzSvkhbp8BuiBd+H5GCea4gUkvEp/NK5FvZxLqF3gehN3R0PM5JdxwyuOEdq4fccOnu7ipI17xV0U2OdBO4pPzF8JwPd/xotIVOlBC0kZOqG57sXb4+4wf91NfKZnleTyFeAifoFgufziBtG8fKOFicwry21yv5S8d8SLpXDd2VYdQYT7LJgrq2X7sxN5Rss/DidR/ZjLc+hEBqQ9koQxmvtTdsswaQnhQ9E2NYf1MeA1B+ia6fM9wcwi983one7rfS+2DGYwWwV9oZGrkiySQjHUaxBPf+4MwOEW21S55GHahCB2K8bEhmMPfwpwOi5eE2U0XHIYvbM7CtgNfpASn5BAvk7rmaLE+vx+0pkdaFlUutvrVBNQaSu2Ckjmjdj5SW6YSrCByGJEVf+QWtlc0HJ/0e/GpCQ2qTAWB2sNXuKzIG7HmayJEFqrtk6efKfzNVv53i8BrXpx5XZC+wIIJL3exCsibayg/S+g/69rvDgEl03Rqty243Ltw4cKFCxcuXLhw4cKFCxcuXLhw4cKFCxcuXLhw4cKFCxcuXLhw4cKFCxcuXLhw4cKFCxcuXLj4t4Fv+ckWMbfa0jfWQC1+4Z41ILHcs2k72vkZI/T1gy1iO/M91hDd0PWtjt9TCPaUW9p1m/i+nyq+Q1+NYD9J/XrOIb5Q96YNEJIyQpdIzHI1SpOprWzURRlzH9LgdF+FhiKaacw4OYdQ32VW5es011X6svGrAH8QOJu6BdrT2BUqs/Wx2PG3rJ/Eq9uNdLbXsybXTk7X1np6o9Hogudip+17koINXqNUfDOTFwfaG2bJKPKPqfh9Rl4OyC4nyBC9S9Pr1BRcH9BpT76WcuSkS22wHIcLdWa1IwQWezZGorHZbzpZ3hW+GvYnZVlQjx6sO/g4Ed5XvfqQVLtvP1bUYs9ctHLjBMtNARCSSdB5/Br7LC4cmouGH52mSW0w9GAGX0EW1i0B8toG6XUgCJirKpGIUnk8jXwf74h79QHT0ey2sgfUgQO6+NWvHOGoLIdMoHzrLhEf9KUtgfiPrtHUEwSCn4hvfs5efxINLniw2UBSI1xwlin4HYuCVdoQVKwkn2KIL1611yB9N+dVPUOcMLCTZJCN4IeIezkbUVZtuQrUm+yNtrKBrWDRM05zRiDpeRGJr+BYkvwIEPL0s9wUpKPErRz3A3Fb3ub4FXxI4ANbe7JlKRs9BVZGAsA1JZMUICNIYGfcD9yRcXEJIfDujk4n0L69wzJIzFLxh5DvBhQX+mKaZeI0M+qq7/QbXNfEN7knWIdMI6a+COI3bXW+CalqgHukhbH4fTcT2FTs3L9MgKpxJaTtRv9vBUh0M3wxGS4N2Liv1Z2DvCt9N7sY92RoIBlFzTRmU6AKyr22iFt59dygxe4B4o1xOZnM/sbKPaS1qmGKXD1kZKnlIC/FzrgniRBHD2NdZncaSM4v7HuYYYOtAOKP4gGMck+y/kiQ19XI4MffgDZM9aUvgfie/Q7u+yY6knLSnhjcdgD/jJiyatiL78NxVGf3gJBn5+25HulB1huN2rgftWcQ/RhoB+75Z2TQf3ujZ25xkP44QFiOn/ApLO1gGmzYZverJ1A2NmPnPvXQ8iF0lqja5H4YWhJ3Y8eCEu4bQ9jKgfSVN4qIy658feAOS94gXh1i3NO0er5nsZ65V4P0x0uT8D89GTDE7wMbTluafujWkFiJZezc2xSs3ibVNbknrhT/23Zzv9pDcMjoN0JXjtF84/YMSGu27nmYSELsnrg4JEta3yT9bX7hDlan+l2llzqmpNGi+OXa6YUjeXDZfTZh1EHLB6pAk3vpU3Lk1OaLozsb21pw/ztnHp4C0wi9kmbmi+b0MGsmhApq96TbC0HjZjkBC3eI+OmvDPHFR6AmSw426bPcInH/Jq1XXbLq4r+o7g3uQ99BSdzH0etHHala22v34vOD6K+JBdyOjyCtAk97CIcVJbyx8uO+eSNnifQ5aQmQGwqJL+74sz8ST57IApnxhvFwWEsqTh3gGvfc8iZNWhnAl9Kxo5MkKG9WYnNGYqMTJIORwb3IRurje2L3PzmvBKWCJ7UR372TrD4HRVDuF+7QRHM1O6fzpRr3oSf9iJ+aJOM9dgSZ+PqGshIzMkXFn5atfX7qOc1M2MLus/7qJu6geopevozNSs9A5lr0UlvaRFom2wtJD4ORMBm3spFs40eb6BF/JFK+Eg13QJ/P6dVoJjl8WhamhsATN446Q1vfGTrHy4YVQlkaN1ZxjfQf+Qe1/mp4fg38a5N7rZe421hybqMDZfHEIhrGrmwE3Nkw5T7w135UgJ4h9BF89L1gndLuuX/ZWcXqqK5A4Uwp2jSkk63OftPQG9D9soAlx3+yHqZp0rjjRG6O1obD4hP7hoxpIp1K5Odr7s3oPHlOj8l9lfQG4gvcPMbw9Ph6z1wQPHksvBJmGckg8ewy1JA62OJjqucW3GPfDDxBkhq32o/K4yT/Z9kzpE2rD72Q1Y7HlRY/vDuNlrvpuA4o9xLE6PwnUPl6LpMjSaLNR8BA7sApa2rrAuslz9jzXUvTKMB6RT6JVJZSND/v9b3CghjcB5QuZmp8tVlGNPJom8LtBAq9BRmZzbnZrrkve4owciSg12ZKgaS/oUfzCTyZZl1DOUY1Qhqcvrjv+95o8G/zMAePRqEmy3Qw4By10UrYJadF8DkUH6TfDs9Dz9hlcp8tGcsMWrRJhiZukYylE52Ue23WGHOacs9hnYp/P0i62MAMSp0rRiILnn7x/WM03ffAOGRGJZkN1cO4mS2eooZv5JO2eTza1KmSj4wxslzH/bCxBkO556q44SrhYGW2tsSQ94z7qAmX4WBuatD2YAltkRyaOgfC8EnHkgvH8lFiHYc+8iJ9xnz+zK59PTKrhOmwesJQCvkIDo45hdIb5AeyTKFZ1leDe94U35xpcWXPeICJDweLz/bXljvg53vkSnQtTHY+pYNfoOKvjhPuLeK38vX07OcJyFCa0EsofrGDZDom3OMr+HE/nfqin8yi8UUFodUaV+FuTlvdTyV7NAbd199MrXNlk2Jm93w1WkrKstecGGg/FuXyn6CigQqVQ/wPr5V71HdNhk6U+Pna4gV7NlRLYnrgHr55cZgo4PiOs30x7kUL95Al74yV+w9alG5yz5lZ+gy791VniPjmIaFDWHzy3J+a+FbucRuGEVQmfj5f/cHha+o1K2SLKtn7E2Cn3Pn6GYnqIb2zNpPzgd2j9XHFi9Qr7KFDhPuXJdLEQ3PgEtTWF5tAhfy2/EnK7KWxOK7cC1Mveq2ncvT55sSAPFGCtGqLH2Xn/iuyjvklcRlTnzb1w0ifD4fQ9dTwjhPkDdA5o417ppQ6u294vkFs1hTf2eeb6yFvAx3EwbXYl5V739QcFl5ZHiSfRp3zjBqMBbXQBFFDuG6IrIaVcBH61W481QIJ0/+ASk0BE3KCcA8uKLZ3cY01w5NQu2TTS9Kl97fpeH+JSN3w8UHNuP/lELKs3xtyWLmnUwKOrutJzbmXDrPXTzqbHbId+PBMhczUAh8cM7nHSuFgKRH4B+59H9SvWptosGzajPvASWhDfY7Hz9nsnp7J1vVacG9McUMntpiLrH4Vzq2CEyn+Ez6Kr3rALa3ewg5V/sBcJn+3hAr/OHSop0juQY0EmyeMg2SyuB31myJx4M1m6o77l114UwjS5i85RFKt63rpa3hm42drOyz1vKaE6/o0ia33SGSFl88qu8tyx1XPFbu0M/M5X/lwiSlF+9t8Qrt/J8Gp+LemZzbgnn+3v/EhRPJ1xwnxSUs1jhex9H62tgMm00TBIWN+fxG4x+I3XYZyDuGw+sjhGQr7ScBTvJwgZG91NzjWDvXQTKWHOdda7wgg1rtZ1/aW7MKbE4PAqwfhxXnH4aFBy4f0QwWbYvUJteYyuURvrLfO8ZWM5w/A021wJWI7uxtjALThhSc+cODvUKUYD4FgmmqCQv2D7bj/TjQ+RMTiLznvScYtK2Xcvzax9MoCWzwaaapgQ3x+oXe34lNn/dU2HCYuuZ1Mmkn7MZYH1cn+uhYqWk2W2+bdVN+bks1SbzAsOQZNi2+zlfjbvZccaJ/4w08TSMjuznRc/EyhRUjachcuXLhw4cKFCxcuXLhw4cKFCxf//6BlrEuRvP3GScBxHyVrex66bjsV8dn6PSl6Zqs7sPbrOy/4hiLb9LnwPx9UR0p8wbaLQv/BtlM3a99koK1aY5R8hSv0NoGeI7eJ9BuDzgtoy6egdOMukiDXrWrz5aOWO4Nc9Vy74k32EtqrCVjrp1t9IhUWM1eNwt0aJbzSnnCphvAZ9sXv+vF8o5fpw1ox2HNAHXeWjZuUq5PkJXQZXzViCCx+SYXWl3rIHcA+o91oYdiDCfu5JPI0a222JzYSjUYrHkvpAWo83CPjPhMHT5+89AZzr/llOZkNTsMmVKi7vhJVIv7qrbtsx14W4swEYaD5zfldQ/JsRBf+ACFwu7sIJ8OuYolxr31LbscC93wS9qn6lZKxOSH0eISGDZKNBfpI2J9cP92BxL/bb12Z3HPZqF8OwdYi6SOqF3bD6xfW26LDJNqNPMs+/3gDt4yr+9vGvb7SszHTifuRxZ65dkUvIW0hpkSqIFa89oBw9Zxh5tD9Ycjr403ObwPgnjnZrxffsZ4Caxsj0QVPd/yEyb3vl6Q0wn0VtlBXwUgJ9yEIPwod6Ee1J1yHIP6Mcp9VYKsx7Frss40XlwbxP+m29Uao73+s95LTV0zuCYxtpW0B/2taUNzTYmfOTkDFMrjXFj3mLfjsubkg7EpT6jdktA1wW45w3+xW73bu2wlkC5+F+zh5FLqlz0/DVkfCPQ20GLgbDi4wM/Ydh7ZNuYeoXVmFIFMb9+nT3krviHECReq2dRsW3eVT457EZbaL+wDjPk24b99TcdMTnUk5mafcBxbuTQvVlR+/J6ZvbClOttgP0g60iMvhBy434F6LUFhchKkhK/dM6Sb3gWdk+yF8pIHDl45kSyxmDNHgZPHPytL3dGsAiaW2Bhyp32OHIJmws21sYCeQPiWNzeSexnwNjAdaP9l6m7Byz5VPsRYot2wDnJM0nSmtViHp3DiqxmaAey5bGaHa5LIjRJTyBmzGud7zZBcPEt4GWsVkxRtxr0Yp6OCXHYmOLJ6A3YRetnMudJQOWyb3jAr4KB3oZr28dJEocfmI+OIB9vXOTdM4e2wNcEkL96F7/RIEbUnvWWcRw9bhfoAGtxvc06AnNPBgJdYOPznw6yNk9M2D3RsjDw9Rgo3jseDb+AXH1psqU5q59UX6rL8AwZlED8134vB7avmtud/6fL1Edl3Gr/SukDke96I7T7abGRtvmVXSpqA97l15Am1cuumFXA2wRXh1wuszdreDNSAr9/kH2NylW0NIOuzlFmK90SiE+IVnV772GOkM1BNoCXTKuGfxZ402SO4IgV8/IFvCF45auAe66K5WJ8R/QovYijJpox/C5CF4xpuNxUCuKJ6/jFz3HL272LMRW4EvYiPX9926tlePXkc17kUlUilCWB6NnqhGqnOd8cuaMss+ZmealQChZNDnp4jdA8fD3/Ub/Tvi/0VN1OgG2AxdmoQ+g3aB1U7fcxYPcL5EAlcM7gMV2rto0xAthHi/koHIPsHYLEnOedyPxPvzEGkKkkiP2WDUPu4tvp50UVZWIJFCteRb/i5qOP5m2GKCK5zF3/IQXvUyE2m2nTlPJ/Kr40jCfaYMUzovxLyQHoDX/QlQQOq9PaSdgHEvfYNnWhtodQyl8FybW8RfLnfHz/aTwZxbw699jLz8PgpjE6z6FP4D919i7pnNf9RlcL/M5imMe0YYp5XM/iywNo1mSfcpPsaXhXUeg3voP/UMnBNYfNB4k71vkQS0fjhGuc9uGL1tu7knvp50a5o4NHmstdqm+QINWyQ79aWbsFZ1uIO0efE861QLTGlUCVrNVxLNUcDi3wry8KQsh85mdr3s0hqM+3WwTo6PeFHq/QTd+M95SZ+PdZieiESUVx81HN40qmzg/v1jqMosodzPuDeoN7hXrx/agMWZxZtGadrK9Q06Lusx0lsPXLOlkeBpJh26cpQdccyxA1FqWtoM4V7LIC1IN6LvDffQ5w/vJ5EltRFR/LKTLmkR7r0QDdJFwyf7rjUptRwbATVEF5/SQURcjPVuGJ6dtrYRhOhatg62Z6DciyfZdTk9ezthuOrE18M6HNjfdEu+NkPrzri3ALj3Vcxmbbp+tCAzyDoEc/PVQSjKmM3K9hQihbskHRSd4+Vv2q/PWd6ypCoqiSFotCl+R6jN7481456taJIIPca9lzb9+MVmUUN6JAF1ZxG2PMyF1CsOt35gD9d2MLILnrkM+K1UU9pMTsR2zzJ+GdyPNmu9NaemMfeWjCSOJV4z+xL1/x1+sZ37/TC+S45EIg3AuGepd1rPwrYNvXLrrtIB63qgqBbccy9LVrvvY7ljtlghYQNHnCx1GUsS6vU58GmDi3u4no+I60VMehjWXwTfX7qRejaB52lYjXzC6POJ9801D8FDjbi3r805uY8bAXY068rZFtzTM1OM+xaRoPep2QT+0s5ZsaEg+ird7mLcdzu5x22dn8LcX/RywD0d6l9tZbkG92T1wgzF2suF/AYoP4kqGW71YTj3Cjuhas8cdqnL35WQfmY+h0JffxNtEYKHSNBU6hObpfXZ629Pt4TUSfZG+gL78Gccsqat7Wb0ITaC6NpbpHTpQiYCEUk/3qsnmHHPTW3isTK72FOfbXG34MsXpr3a6t2cfmMzIZ7fpKMUXz0w7UX5d+Yy5bsl37ubGb58ZRppvRl/ecs7AEak3Rlc2fxhwwJGJyGTir+yyyiybYPeFjXGdQ6/YXFngvX7ZuBzSLTrOm9v8nlHmg3zV20ttuFUUdx6br4IdRDZMRq939louXONzQR4TL0z/UF7YGqEaIUTLN8aYYvwrfnF1uFTEjMJvhyL1bKe+rJwD1eJtGVh0oULF21FQKFwzfPfD5xM0c5U1C5cuHDhwkXb8L+B1f5NInmpoAAAAABJRU5ErkJggg==)



## 캐시 설계 시 고려 요소

- 캐시 크기
- 인출 방식(Fetch Algorithm)
- 사상 함수(Mapping Function)
  - 어떤 주 메모리 블록들이 어떤 캐시 슬롯을 공유할 것인지 결정
  - 직접, 연관, 집합 연관 사상
- 교체 알고리즘(Replacement Algorithm)
  - 어느 슬롯 데이터를 제거할 것인지 결정
  - LRU, LFU, FIFO
- 쓰기 정책(Write Policy)
  - 즉시, 나중 쓰기
- 블록 크기(Block Size)
- 캐시 수

![img](https://blog.kakaocdn.net/dn/d3m8Rk/btqQE8gcenk/Ey7R1QfyC2KO1dZShREGZK/img.png)



## References

- 위키백과 : https://ko.wikipedia.org/wiki/%EC%BA%90%EC%8B%9C
- 동아 : https://it.donga.com/215/
- aws : https://aws.amazon.com/ko/caching/
- mdn : https://developer.mozilla.org/ko/docs/Web/HTTP/Caching
- web cache : https://rinae.dev/posts/web-caching-explained-by-buying-milk-kr
- http cache : https://web.dev/http-cache/
- 우테코 발표자료 : https://drive.google.com/file/d/1RLv6bHT5QNc8fRf-8zQFrAYn7l6vLlvJ/view
- 캐시 원리 : https://parksb.github.io/article/29.html
- 강의 자료 : http://elearning.kocw.net/document/lec/2011_2/dunksung/YouGyunA/13.pdf
- 정리 : https://kimtaehyun98.tistory.com/48