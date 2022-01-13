## 목차
- [목차](#목차)
- [CORS(Cross-Origin Resource Sharing, 교차(다른) 출처 리소스 공유)](#corscross-origin-resource-sharing-교차다른-출처-리소스-공유)
    - [CORS를 누가 알아야 하는가?](#cors를-누가-알아야-하는가)
    - [출처(origin)](#출처origin)
    - [SOP(Same-Origin Policy)](#sopsame-origin-policy)
    - [CORS를 사용하는 경우](#cors를-사용하는-경우)
- [CORS 등장 배경](#cors-등장-배경)
    - [JSONP(JSON with Padding)](#jsonpjson-with-padding)
- [동작 방식](#동작-방식)
    - [프리플라이트 요청(preflighted request, 예비 요청)](#프리플라이트-요청preflighted-request-예비-요청)
    - [단순 요청(Simple requests)](#단순-요청simple-requests)
    - [인증정보를 포함한 요청](#인증정보를-포함한-요청)
    - [HTTP 응답 헤더](#http-응답-헤더)
    - [HTTP 요청 해더](#http-요청-해더)
- [출처](#출처)

## CORS(Cross-Origin Resource Sharing, 교차(다른) 출처 리소스 공유)

#### CORS를 누가 알아야 하는가?

> 모든 사람이요, 진짜로

CORS는 추가 HTTP헤더를 사용, 한 출처에서 실행 중인 웹 어플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제

![CORS예시](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/cors_principle.png)

- https://domain-a.com FE, JS 코드가 XMLThhpRequest를 사용 https://domain-b.com/data.json 요청
- 보안상의 이유로 브라우저는 스크립트에서 시작한 교차 출처 HTTP 요청 제한
- 서버에서는 정상적으로 동작(requset 200) but CORS는 브라우저에서 판단함

#### 출처(origin)
웹 콘텐츠에 접근할 때 사용하는 URL 스킴, 프로토콜, 호스트(도메인), 포트
- Javascript 에서 console.log(location.origin)으로 출력 가능

#### SOP(Same-Origin Policy)
- 웹에서 리소스 요청을 제한하는 정책 중 하나
- 포트의 경우 달라도 같은 출처로 인정해 줌 (IE 제외)
- 2011 [RFC 6454](https://datatracker.ietf.org/doc/html/rfc6454#page-5)에서 처음 등장한 보안 정책
- 다른 출처에 대한 제약이 없다면, CSRF(Cross-Site Request Forgery), XSS(Cross-Site Scripting)에 취약

#### CORS를 사용하는 경우
- XMLHttpRequest, Fetch API 호출
    - Fetch API : ajax를 구현하는 기술중 하나로, XMLHttpRequest와 비슷한 API, 좀더 강력하고 유연하게 조작가능
    - 
- 웹 폰트(CSS내 @font-face에서 교차 도메인 폰트 사용 시)
- WebGL 텍스쳐
- drawImage()를 사용해 캔버스에 그린 이미지/비디오 프레임
- 이미지로부터 추출하는 CSS Shape

## CORS 등장 배경
- 대부분 하나의 서버에서 브라우저의 모든 요청을 처리했지만, 점점 다양한 기능이 추가됨
- 서로 다른 출처로부터의 요청을 주고 받을 수 없어 JSONP로 해결
- 상속 비보안 문제로 CORS로 대체

#### JSONP(JSON with Padding)
- 웹브라우저에서 실행되는 JS는 동일 출처 정책에 따라 직접적인 HTTP통신 불가능, HTML script태그의 요소는 외부 출처로부터 조회된 내용을 실행하는것이 허용

```HTML
<script type="application/javascript"
        src="http://server.example.com/Users/1234?callback=parseResponse">
</script>
```

- JSON데이터를 클라이언트가 지정한 콜백 함수를 호출하는 유효한 JS문법으로 감싸 클라이언트에 전송

```
parseResponse({"Name": "Foo", "Id": 1234, "Rank": 7});
```

## 동작 방식
- 새로운 HTTP 해더를 추가함으로써 동작
- 서버 데이터에 side effect를 일으킬 수 있는 HTTP method(GET을 제외한 method)에 대해 CORS명세는 브라우저가 요청을 OPTIONS메서드로 preflight(사전 전달)하여 지원하는 메서드를 요청, 서버의 허가가 떨어지면 실제 요청을 보냄
- 서버는 클라이언트에게 요청에 인증정보(쿠키, HTTP인증)을 함께 보내야 한다고 알려줄 수 있음
- CORS실패는 오류의 원인이지만, 보안상의 이유로 JS에서는 오류의 상세 정보게 접근할 수 없으며, 오류 발생 여부만 알 수 있고, 정확한 오류를 알기위해 브라우저 콘솔을 봐야 함

#### 프리플라이트 요청(preflighted request, 예비 요청)
- OPTIONS method를 통해 다른 도메인 리소스로 HTTP 요청을 보내 실제 요청이 안전한지 확인
- Cross-Site 요청은 유저 데이터에 영향을 줄 수 있기 때문에 미리 전송(preflighted)

![프리플라이트 요청 CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/preflight_correct.png)

- 예비 요청 후 본 요청 활용
- OPTIONS method를 통하여 Origin, Access-Control-Request-* 등의 헤더 요청
- 실제 POST요청에 Access-Control-Request-*헤더가 필요하지 않고 OPTIONS 요청에만 필요
- POST 요청에 따라 Access-Control-Allow-Mehods, Access-Control-Allow-Headers와 같은 응답 보내줌

#### 단순 요청(Simple requests)
- 일부요청은 CORS preflight를 트리거하지 않음
- 다음 조건을 모두 만족하는 요청을 말함
    - GET, HEAD, POST
    - 헤더는 Accept, Accept-Language, Content-Language, Content-type
    - Content-Tpye헤더는 다음 값만 허용
        - application/x-www-form-unlencoded
        - multipart/form-data
        - text/plain
- 제한적이여서 일반적으로 구현되지 않음
    - JWT token만 사용하더라도 사용 불가능
    - REST API에서 더욱 활용 힘듬

![단순 요청 CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/simple-req-updated.png)

- Origin헤더에 대한 응답으로 Access-Control-Allow-Origin: * 으로 응답, 모든 도메인에서 접근 가능을 의미

#### 인증정보를 포함한 요청
- 인증정보를 포함한 요청에서 쿠키 없이 자격 증명을 보내지 않음
- Access-Control-Allow-Origin에 *를 사용할 수 없으며, 명시적 URL을 사용해야 함
- 응답 헤더에 Access-Control-Allow-Credentials: true가 존재해야 함

![인증정보 요청 CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/cred-req-updated.png)

- 쿠키 정보를 담아서 보내줌

#### HTTP 응답 헤더
- Access-Control-Allow-Origin
    - Access-Control-Allow-Origin: <origin> | *
        - origin에 상관없이 모든 리소스 접근 허용
    - Access-Control-Allow-Origin: https://mozilla.org
        - origin을 지정하고 모든 리소스 접근 허용
- Access-Control-Expose-Headers
    - 브라우저가 접근할 수 있는 헤더를 화이트리스테 추가할 수 있음
- Access-Control-Max-Age
    - preflight request요청 결과를 캐시할 수 있는 시간
- Access-Control-Allow-Credentials
    - true일 때 요청에 대한 응답을 표시할 수 있는지 나타냄
- Access-Control-Allow-Methods
    - 접근에 허용되는 메서드 지정
- Access-Control-Allow-Headers
    - 실제 사용할 수 있는 헤더 지정

#### HTTP 요청 해더
- Origin
    - cross-site 요청 또는 preflight request의 출처
- Access-Control-Request-Method
    - 사용 가능한 메서드 요청
- Access-Control-Request-Headers
    - 사용 가능한 헤더 요청

## 출처
- https://developer.mozilla.org/ko/docs/Web/HTTP/CORS
- https://ko.wikipedia.org/wiki/JSONP