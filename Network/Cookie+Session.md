## Cookie

- 어떠한 웹사이트에 접속했을 때, 서버가 일방적으로 클라이언트에 전달하는 작은 데이터
- 서버가 웹 브라우저에 정보를 저장하고 불러올 수 있는 수단
- 해당 도메인에 대해 쿠키가 존재하면, 웹 브라우저는 도메인에게 http 요청 시 쿠키를 함께 전달

### Cookie의 특성

- 삭제하지 않는한 사라지지 않는다. => 장시간 보존해야하는 정보 저장에 적합함.
- 필요한 정보가 Hashing되어 저장된다.

### Cookie 전달 방법

- 서버가 Response 헤더에 Set-Cookie 라는 프로퍼티에 이름과 값을 저장함
- 클라이언트는 서버로부터의 Response에 Set-Cookie를 확인함.
- 그 후로는 클라이언트가 서버에 Request할 때 마다 Cookie의 이름과 값을 보내게 됨.

### Cookie의 Options

- Domain : 서버와 클라이언트로부터 Request의 도메인이 일치하는 경우 Cookie 전송
- Path : 서버와 클라이언트로부터 Request의 세부경로가 일치하는 경우 Cookie 전송
- MaxAge or Expires : Cookie의 유효기간 설정 => 일정 시간 후 자동 소멸 가능
- HttpOnly : 스크립트에서 Cookie 접근을 막고 브라우저에서만 접근 가능하게 하는 등 접근 가능 여부 설정 => Cookie는 `<Script>`태그로 접근이 가능 => XSS 공격에 취약함 => 개인정보는 담지 않는 것이 좋음.
- Secure : HTTPS 프로토콜에서만 Cookie 전송 여부를 결정
- SameSite : CORS Request에 대해서 Cookie의 전송 여부를 결정 => CSRF 공격을 막는데 매우 효과적 \*CSRF : Cross site request forgery

  - 옵션에 따른 서버의 Cookie 전송 여부

    1. Lax : GET 요청만 Cookie 전송이 가능
    2. Strict : Cookie 전송 불가
    3. None : 모든 요청에 대해 Cookie 전송이 가능 => HTTPS 프로토콜 + Secure 쿠키 옵션이 따로 필요함

## Session

- 서버와 클라이언트간의 연결이 활성화된 상태
- 데이터를 서버에서 관리
- Cookie에 데이터에 대한 ID를 암호화한 상태로 부여를 홤.

### Session 전달 방법

- 클라이언트에서 유저 정보와 처리할 항목을 서버에 요청으로 보냄
- 서버는 DB에 정보를 저장함
- DB는 Session_ID를 반환해줌.
- 서버는 Response 헤더의 Set-Cookie에 Session_ID를 암호화한 상태로 담아서 클라이언트에 전달함.

---

- Session_ID를 가지고있는 상태에서 재요청을 할 때는 유저 정보 대신에 Session_ID를 넣어 서버에 요청을 보냄.
- 서버는 DB에 Session_ID를 확인하고 정보를 업데이트함.
- DB는 업데이트가 완료됐다고 서버에 Response를 보냄.
- 서버는 클라이언트에게 정보를 업데이트했다고 Response를 보냄.

### Cookie와 Session의 차이

- Cookie : http의 무상태성(stateless)을 보완해주는 도구

  - 접속 상태 저장 경로 : 클라이언트
  - 장점 : 서버의 부담을 덜어줌
  - 단점 : Cookie 자체는 인증이 아님

---

- Session : 접속 상태를 서버가 가짐(Stateful). 접속 상태와 권한 부여를 위해 Session_ID를 Cookie로 전송

  - 접속 상태 저장 경로 : 서버
  - 장점 : 신뢰할 수 있는 유저인지 서버에서 추가로 확인 가능
  - 단점

    - 하나의 서버에서만 접속 상태를 가지기때문에 분산에 불리함
    - 서버의 메모리에 Session 정보를 저장하고 있기 때문에, 서버의 이용자가 많아질 수록 저장공간의 일부분을 항상 Session 정보 저장하는데 사용을 하기때문에 사용 가능한 메모리의 양이 줄어들어 서버의 성능 저하
    - Cookie를 사용하고 있기 때문에, Cookie의 한계를 그대로 가지고 있음. (XSS 공격에 취약함)
