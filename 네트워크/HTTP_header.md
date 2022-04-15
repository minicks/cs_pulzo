# HTTP 헤더

## HTTP란

- Hyper Text Transfer Protocol
-  인터넷에서 데이터를 주고 받을 때의 통신 규약(즉 프로토콜)

## HTTP 프로토콜

![image](https://user-images.githubusercontent.com/68271159/163570814-cddbfc41-0c47-469f-9543-ae316e3f7388.png)

http://www.ktword.co.kr/test/view/view.php?m_temp1=648



## HTTP 헤더

- 클라이언트와 서버가 요청 또는 응답으로 부가적인 정보를 전송할 수 있도록 해줌.

- 대소문자를 구분하지 않는 이름과 콜론 ':' 다음에 오는 값(줄 바꿈 없이)으로 이뤄짐.



## 일반 헤더(General Header)

- 일반적인 정보 담음
- 요청 프로토콜, 응답 프로토콜에서 둘 다 사용 가능
- Date : 메시지가 만들어진 날짜, 시간
- Cache-Control: 캐시에 관한 설정
- Connect: 현재 전송 완료 후 네트워크 접속을 유지할지 말지
(더 많은 헤더가 있지만 다른 블로그, MDN 문서에서 강조한 일부 헤더만 다룸.)
- ![image](https://user-images.githubusercontent.com/68271159/163570866-44fd0df6-f59b-40ba-9860-0740d36476ed.png)

## 엔티티 헤더(Entity Header)

- 바디에 대한 자세한 정보를 포함한 헤더

- Content-Length :  메시지 바디 길이(바이트 단위)
- Content-Type: 메시지 바디의 컨텐츠 종류, 인코딩

![image](https://user-images.githubusercontent.com/68271159/163570906-a9201078-1a41-4512-af3b-d183d2541882.png)

## 요청 헤더(Request Header)

- 클라이언트의 정보를 담음
-request 프로토콜에서 사용함

- Cookie: 전에 서버에게 받았던 쿠키를 서버에 보냄
- Host: 요청된 URL의 호스트명(도메인명)
- User-Agent: 클라이언트 프로그램에 관한 정보(운영체제, 브라우저)
- Authorization: 인증 토큰

![image](https://user-images.githubusercontent.com/68271159/163570942-1e54390e-d8b3-4b44-b66c-efb6b1c73cd5.png)

## 응답 헤더(Response Header)

- 서버의 정보를 담음
- 응답 프로토콜에서 사용함

- Server: 웹 서버 정보
- Set-Cookie : 쿠키를 브라우저에 보냄
- Location: 300, 201 응답일 때 어느 페이지로 이동할지

![image](https://user-images.githubusercontent.com/68271159/163570971-2926319b-5a4a-4686-b7c4-3d37f05e00f3.png)

![image](https://user-images.githubusercontent.com/68271159/163570981-99424535-fd21-4881-aaed-28d6a58c3448.png)

## X가 붙은 헤더들

- 2012년 폐기
- 커스텀 등록 헤더 (사용자가 임의로 정의한 헤더)


## 참고 자료
https://developer.mozilla.org/ko/docs/Web/HTTP/Headers
https://www.youtube.com/watch?v=mQTGmxendk8
https://velog.io/@pixelstudio/크롬-개발자-도구로-보는-HTTP-헤더-알아보기
