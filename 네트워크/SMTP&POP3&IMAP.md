# SMTP & POP3 & IMAP

## 이메일 시스템

- 메일 서버
- 메일 클라이언트, MUA

## 메일 서버

- MTA (Mail Transfer Agent) - 이메일을 메일 서버에서 다른 메일 서버로 보내는 역할
  - sendmail
  - qmail
  - postfix
- MDA (Mail Delivery Agent) - 메일 서버에 도착한 메일을 사용자 계정으로 전달해 주는 역할

## 메일 클라이언트, MUA (Main User Agent)

- 웹 메일
  - 네이버 메일
  - 다음 메일
  - 카카오 메일
  - 지메일
- 설치 소프트웨어
  - Mozilla ThunderBird
  - Outlook
  - Mailbird
  - Post
  - Mailspring

![email_flow](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/f7a38afb-5c5d-4bcc-9291-324d4f472f77/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20220507%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20220507T175739Z&X-Amz-Expires=86400&X-Amz-Signature=b179f6b3008bbda9e1c5478ff4ab65a1421a4fdb8ef244ae55f5289304b16ffb&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)

## DNS 서버

- MX Record 확인 - https://intodns.com

## SMTP (Simple Mail Transfer Protocol)

- 이메일을 전송할 때 사용하는 프로토콜
- 기본 포트 번호로 25 사용 (보안 연결은 587 사용, 예전엔 보안 연결로 465를 사용했으나 지금은 거의 사용하지 않고 레거시로만 남아있음)
- 이메일 송신 프로토콜이 사용되는 경우
  - 클라이언트에서 작성한 메일을 서버로 전송할 때
  - 인터넷을 통해 서버간 메일을 전송할 때

## POP3 (Post Office Protocol 3)

- 이메일을 수신할 때 사용하는 프로토콜
- 기본 포트 번호로 110 사용 (보안 연결은 995 사용)
- 맨 끝의 숫자 3은 세 번째 버전을 의미
- 이메일 서버에 도착한 메일을 클라이언트로 가져올 때 사용
- 서버의 사서함으로부터 클라이언트 PC로 메일을 직접 다운로드 하는 형식
- 다운로드와 동시에 사서함에 있는 이메일이 삭제됨 (optional)
- 다운받은 메일은 오프라인 환경에서도 확인가능
- 별도 설정 없이 로컬 PC에서 메일을 삭제한 경우 서버에서 해당 메일을 확인 할 수 없음

## IMAP (Internet Message Access Protocol)

- 이메일을 수신할 때 사용하는 프로토콜
- 기본 포트 번호로 143 사용 (보안 연결은 993 사용)
- 이메일 서버와 동기화 되는 방식
- 메일 열람 후에도 서버에 이메일이 그대로 남아 있음
- 클라이언트에서는 메일의 헤더 부분만 보여주고, 해당 메일을 클릭하면 메일 내용과 첨부파일등의 분문을 다운로드 함
- POP 프로토콜 보다 빠름
- 메일을 확인할 때 마다 통신 트래픽을 높임
- 오프라인 환경에서는 메일 확인 불가
