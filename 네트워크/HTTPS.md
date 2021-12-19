# HTTPS

## HTTPS(HyperText Transfer Protocol Secure) 란?

- SSL, TSL 프로토콜을 사용하여 HTTP의 보안을 강화한 프로토콜
- 구글에서 HTTPS를 사용하는 웹 사이트에 가산점 부여 => SEO 향상

## SSL(secure sockets layer)

- 서버와 클라이언트 사이에 암호화된 연결을 만들어 도난 방지
- TLS(Transport Layer Security)는 표준화된 SSL의 정식 명칭
- 인증 기관(CA)로 부터 인증서를 발급 받아 사용
- 대칭키, 공개키 방식을 혼합하여 사용
- 공개키 방식으로 대칭키를 전달
- 대칭키로 암호화, 복호화, 서버, 클라이언트 간 통신 진행
- 키교환 알고리즘으로 주로 RSA, Diffie-Hellman 알고리즘 사용

### 인증서 발급 과정

![How does a certificate authority validate a certificate?](https://d1smxttentwwqu.cloudfront.net/wp-content/uploads/2019/07/ca-diagram-b.png)

1. 사이트에서 인증 기관으로 사이트 정보와 공개키를 보냄
2. 인증기관에서 이 정보를 검증
3. 인증기관의 개인키로 인증서에 서명하여 사이트로 전송
4. 인증기관의 공개키는 브라우저에 내장되어있음

### HTTPS 통신 과정

![TLS 핸드셰이크](https://cf-assets.www.cloudflare.com/slt3lc6tev37/5aYOr5erfyNBq20X5djTco/3c859532c91f25d961b2884bf521c1eb/tls-ssl-handshake.png)

1. TCP handshake 진행
2. 서버에서 클라이언트에 인증서를 전송
3. 브라우저에 내장된 공개키로 인증서 복호화
4. 복호화된 서버의 공개키로 클라이언트의 대칭키를 암호화
5. 암호화된 클라이언트의 대칭키를 서버에 전송
6. 서버의 개인키를 이용하여 클라이언트의 대칭키를 복호화
7. 대칭키를 이용하여 암호화된 통신

# References:

- https://www.youtube.com/c/%EC%9A%B0%EC%95%84%ED%95%9CTech
- https://www.cloudflare.com/ko-kr/learning/ssl/what-happens-in-a-tls-handshake/
- https://aws-hyoh.tistory.com/34?category=768734
- https://brunch.co.kr/@sangjinkang/38