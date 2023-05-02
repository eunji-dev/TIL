# CORS

교차 출처 리소스 공유 Cross-Origin Resource Sharing

출처(Origin) : `Protolcol`,`Host`,`Port`를 합친 URL<br>
=> `https://` + `www.domain.com` + `:3000`

- Protocol(Scheme) : http, https<br>
- Host : 사이트 도메인<br>
- Port : 포트 번호<br>
- Path : 사이트 내부 경로<br>
- Query string : 요청의 key와 value값<br>
- Fragment : 해시 태크<br>

CORS란 몇 가지 예외 조항을 두고 다른 출처의 리소스 요청이라도 이 조항에 해당할 경우에는 허용하는 정책

<br>

## CORS의 동작

1. HTTP 요청을 보낼때 브라우저는 요청 헤더에 Origin 이라는 필드에 출처를 함께 담아 보낸다.<br>
2. 서버는 응답헤더의 Access-Control-Allow-Origin 필드에 접근하는 것이 허용된 출처를 담아 클라이언트로 전달한다.<br>
3. 클라이언트에서 Origin과 서버가 보내준 Access-Control-Allow-Origin을 비교한다.<br>

=> 서버에서 Access-Control-Allow-Origin 헤더에 허용할 출처를 기재해서 클라이언트에 응답하면 CORS 에러를 해결할 수 있다.<br>

=> 출처를 비교하는 로직은 서버에 구현된 스펙이 아닌 브라우저에 구현되어있다.

<br>

### 프리플라이트 요청 (Preflight Request)

요청을 예비 요청과 본 요청으로 나눈다.<br>
OPTIONS 메서드를 통해 다른 도메인의 리소스에 요청이 가능한지 (실제 요청이 전송하기에 안전한지) 확인 작업을 하고, 요청이 가능하다면 실제 요청을 보낸다.

<br>

### 단순 요청 (Simple Request)

예비 요청을 생략하고 바로 서버에 직행으로 본 요청을 보낸 후, 서버가 이에 대한 응답의 헤더에 Access-Control-Allow-Origin 헤더를 보내주면 브라우저가 CORS정책 위반 여부를 검사한다.<br>

GET POST HEAD 메서드,<br>
Accept, Accept-Language, Content-Language, Content-Type (application/x-www-form-urlencoded, multipart/form-data, text/plain) 헤더만 단순요청을 사용할 수 있다.

<br>

### 인증정보 포함 요청 (Credentialed Request)

서버에 세션 ID가 저장되어있는 쿠키(Cookie) 혹은 Authorization 헤더에 설정하는 토큰 값 등 인증 관련 헤더를 포함할 때 사용하는 요청<br>
인증된 요청 역시 역시 예비 요청 처럼 preflight가 먼저 일어난다.<br>
요청에 인증과 관련된 정보를 담을 수 있게 해주는 credentials 옵션을 사용한다.

<br>

## 동일 출처가 아닌 경우 접근을 차단하는 이유

자바스크립트에서의 요청은 기본적으로 서로 다른 도메인에 대한 요청을 보안상 제한한다.<br>
로그인 토큰이 남아있는 브라우저에서 악성사이트에 접속할 경우 해당 사이트에서 토큰에 접근하여 해킹에 노출될 수 있는데 이때 브라우저가 악성 사이트의 응답 서버 출처를 보고 해당 접근을 차단할 수 있다.<br>

CSRF(Cross-Site Request Forgery)
XSS(Cross-Site Scripting)

<br>

`img`, `video`, `script`, `link` 태그<br>
=> 기본적으로 Cross-Origin 정책을 지원

`XMLHttpRequest`, `Fetch API` 스크립트<br>
=> 기본적으로 Same-Origin 정책을 따름
