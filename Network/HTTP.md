## HTTP

- HTTP/1.1(1997~), HTTP/2(2015~) => TCP 기반
- HTTP/3(시범적으로 적용하고는 있으나 아직 표준안이 없고, 현재도 개발중) => UDP 기반

### HTTP의 특징

- 클라이언트 서버 구조
  - 클라이언트가 서버에 요청을 보내면, 서버는 그에 대한 응답을 보내는 구조
  - Request Response 구조
- 무상태성
  - 서버가 클라이언트 상태를 보존하지 않음
    - 장점 : 서버의 확장성이 높음(어떠한 서버에 요청을 해도 똑같이 응답을 받을 수 있기 때문)
    - 단점 : 클라이언트가 추가 데이터를 전송해야됨(서버가 클라이언트의 정보를 저장하지 않기 때문)
  - 로그인이 필요한 서비스 같은 케이스는 유저의 로그인 상태를 유지해야하기 때문에, 쿠키, 세션, 토큰 등을 이용해 상태를 유지함
- 비연결성
  - 실제로 요청과 응답을 주고 받을때만 연결을 유지하고, 서버에서 응답을 주고나면 연결을 끊음.
  - TCP/IP는 기본적으로 연결을 유지한 상태로 있는데, 비연결성을 통해 연결을 유지하는 서버의 자원소모를 최소한으로 낮출 수 있음.
  - TCP/IP에 비해 HTTP는 기본이 연결을 유지하지 않는 모델임.
  - 일반적으로는 초 단위 이하의 빠른 속도로 응답함.
  - 하지만 트래픽이 많고, 큰 규모의 서비스에서는 비연결성이 한계를 보임.
    - 웹 브라우저로 사이트를 요청하면, HTML/CSS/JS에 더해 추가적인 이미지 등 많은 자원이 함께 다운로드 됨. => 해당 자원들을 각각 보낼때마다 연결을 끊고 다시 연결하는 것을 반복하는건 비효율 적임.
    - 현재는 HTTP 지속 연결(Persistent Connections)로 문제를 해결함. => 연결이 이루어지고 난 뒤, 각 자원들을 요청하고, 모든 자원에 대한 응답이 돌아온 후에 연결을 종료하는 방식.
    - HTTP/2, HTTP/3에서 더 많은 최적화
- HTTP 메시지
- 단순하고, 확장이 가능함

### HTTP 메시지

- HTTP 메시지는 Header와 Body로 구분할 수 있음
  - HTTP Header : 표현 헤더에 표현 데이터를 해석할 수 있는 정보를 제공함
  - HTTP Body : Message 본문을 통해서 표현 데이터를 전달함.
    - 데이터를 실어 나르는 부분을 Payload라고 함.
  - 표현은 요청 및 응답에서 전달할 실제 데이터를 뜻하며

#### HTTP Header

- 형식 : <Field-name> : <field-value>
- 용도 : HTTP 전송에 필요한 모든 부가정보를 담기위해 사용

  - Message Body의 내용 및 크기, 압축, 인증, 요청 클라이언트, 서버정보, 캐시정보 등
  - [표준 헤더의 종류](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)는 너무 많음
  - 필요 시에는 임의의 헤더 추가가 가능함

- 표현 Header : 요청과 응답 둘 다 사용함

  - [Content-Type](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Type) : 표현 데이터의 형식
    - [미디어 타입](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types), 문자 인코딩
      ex) - Text/html; charset=utf-8 - application/json - Image/png
  - [Content-Encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Encoding) : 표현 데이터의 압축 방식
    - 표현 데이터를 압축하기 위해 사용
    - 데이터를 전달하는 곳에서 압축 후에 해당 Header를 추가
    - 데이터를 읽는 곳에서는 해당 헤더의 정보로 압축 해제
      ex) - gzip - deflate - identity
  - [Content-Language](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Language) : 표현 데이터의 자연 언어
    ex) - ko - en - en-US
  - [Content-Length](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Length) : 표현 데이터의 길이
    - 바이트 단위로 표현
    - [Transfer-Encoding](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Transfer-Encoding)을 사용할 때는 해당 Header를 사용하면 안됨

- [콘텐츠 협상 Header](https://developer.mozilla.org/ko/docs/Web/HTTP/Content_negotiation) : Request할 때만 사용

  - Accept : 클라이언트가 선호하는 미디어 타입 전달
  - Accept-Charset : 클라이언트가 선호하는 문자 인코딩
  - Accept-Encoding : 클라이언트가 선호하는 압축 인코딩
  - Accept-Language : 클라이언트가 선호하는 자연 언어
    - 다음과 같은 조건에서는 기본 설정된 언어로 응답함
      - 요청 시 해당 Header를 보내지 않았을 시
      - 해당 Header의 언어를 지원하지 않을 시
      - 우선순위를 통한 지정이 가능함
        - Quality Values(q) 값 사용
        - 0~1까지의 범위를 소수점을 이용해서 설정이 가능하며, **값이 클 수록 우선순위가 높음**
        - 값을 생략하는 경우에는 1
          ex) Accept-Language : ko-KR, ko;q=0.9, en-US;q=0.8 - ko-KR;q=1 (q 생략) - ko;q=0.9 - en-US;q=0.8

- 주요 Header

  - Request에서 사용되는 헤더
    - From : 유저 에이전트의 이메일 정보
      - 일반적으로는 잘 사용하지 않으나 검색 엔진에서 주로 사용함
    - Referer : 이전 웹 페이지 주소
      - 현재 요청된 페이지의 이전 웹 페이지 주소
      - A -> B로 이동하는 경우, B를 요청할 때 `Referer : A`를 포함해서 요청함
      - 유입경로 수집이 가능해짐
      - referrer의 오탈자이지만 스펙처럼 굳어졌음.
    - User-Agent : 유저 에이전트 어플리케이션 정보
      - 클라이언트의 어플리케이션 정보(웹 브라우저 정보 등)
      - 통계 정보
      - 어떤 종류의 브라우저에서 장애가 발생하는지 파악이 가능해짐
    - Host : 요청한 호스트 정보(도메인)
      - **필수 헤더**
      - 하나의 서버가 여러 도메인을 처리해야 할 때, 하나의 IP주소에 여러 도메인이 적용되어 있을 때 호스트 정보를 명시하기 위해 사용
    - Origin : 서버로 POST 요청을 보낼 때, 요청을 시작한 주소를 나타냄
      - 여기서 요청을 보낸 주소 !== 받는 주소면 CORS 에러가 발생함
      - Request Header의 Access-Control-Allow-Origin하고 관련이 있음
    - Authorization : 인증 토큰(`ex) JWT`)을 서버로 보낼 때 사용되는 헤더
      - 토큰의 종류 + 실제 토큰 문자를 전송
        ex) Authorizaion : JWT YQxhZaSpbjpvcGVuc2VzYW1l
  - Response 에서 사용되는 헤더
    - Server : Request를 처리하는 Origin 서버의 소프트웨어 정보
    - Date : 메시지가 발생한 날짜와 시간
    - Location : 페이지 리디렉션
      - 웹 브라우저의 3xx 응답 결과에 Location Header가 있으면 Location 위치로 리다이렉트(자동 이동함)
      - 201 : Location값은 요청에 의해 생성된 리소스 URI
      - 3xx : Location값은 요청을 자동으로 리디렉션 하기위한 대상 리소스
    - Allow : 허용 가능한 HTTP 메서드
      - 405(Method Not Allowed)에서 응답에 포함
    - Retry-After : 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
      - 503(Service Unavailable) : 서비스가 언제까지 사용불가인지 알려줄 수 있음
      - 날짜로 표기해도 되고, 초 단위로 표기해도 됨

- [Cache Header](https://developer.mozilla.org/ko/docs/Web/HTTP/Caching)
  - Cache가 없으면?
    - 데이터가 변경되지 않아도 네트워크를 통해서 데이터를 다운로드 받아야함
      => 인터넷 네트워크는 매우 느리고 비쌈
    - 브라우저 로딩 속도가 느려짐
      => 느린 사용자 경험 제공
  - Cache-Control
    - 첫 요청을 보낼 때 해당 Header를 넣어서 보내면, 응답을 받았을 때 브라우저 Cache에 해당 응답 결과를 저장함
    - 두 번째 요청부터는 Cache를 우선 조회하고, 아직 유효한 Cache라면 해당 Cache에서 데이터를 가져옴
      - Cache 덕분에 Cache가 유효한 시간 동안 네트워크를 사용하지 않아도 됨.
        => 네트워크 사용량을 줄일 수 있음
      - 브라우저 로딩 속도가 개선됨
        => 빠른 사용자 경험을 제공
    - 만약 Cache의 유효시간이 초과한다면? => 다시 서버에 요청을 하고 응답을 받음
      => 이 때 다시 네트워크 다운로드가 발생 - 응답 결과를 받아 기존 Cache를 지우고 새 Cache로 업데이트함.
    - max-age : 캐시 유효 기간. 초 단위
    - no-cache : 데이터는 Cache해도 되지만, 항상 Origin 서버에 검증하고 사용. Origin 서버에서 검증이 불가능하면 이미 Cache된 데이터를 사용해도됨.
    - no-store : 데이터에 민감한 정보가 있으므로 저장하면 안됨. (메모리에서 사용한 뒤 최대한 빨리 삭제)
    - Expires : 캐시 만료일 지정
      - 캐시 만료일을 정확한 **날짜로 지정**
      - 현재는 Cache-Control : max-age쪽을 권장함.
      - Cache-Control : max-age와 같이 사용하면 Expires는 무시됨.
  - 검증 Header
    - 캐시 유효기간이 지났지만, 따로 변경점이 없기때문에 해당 데이터를 써도 되는 상황에 필요함
    - Last-Modified : 데이터가 마지막으로 수정된 시간
      - 첫 요청부터 해당 Header를 작성해주면 응답 결과를 Cache에 저장할 때 같이 저장됨
      - If-Modified-Since Header와 같이 이용하여 조건부 요청을 할 수 있음
      - 두번째 이후 요청에서 데이터가 수정되었는지를 검증함
        - 수정된 데이터가 없을 시에는 304(Not Modified)를, Body를 제외한 Header만 전송함.
        - 클라이언트는 응답으로 받은 Header 정보로 브라우저 Cache에서 Header 메타데이터(유효시간 등)를 갱신
        - 클라이언트는 Cache에 저장되어 있는 데이터를 재활용
        - 결과적으로, 네트워크 다운로드 자체는 발생하나, 용량이 적은 Header 정보만 다운로드함.
    - Modified Header의 단점
      - 1초 미만 단위로 캐시 조정이 불가능
      - 날짜 기반의 로직을 사용
      - 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 똑같은 경우에도 검증 절차는 거쳐야함
      - 서버에서 별도의 Cache 로직을 관리하고 싶은 경우에는 부적합함
    - ETag(Entity Tag)
      - 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠
        ex) ETag:"v1.1", ETag:"64lf5qq24ee8967wd4fe6h01n3m834l1"
      - 데이터가 변경되면 이름을 바꾸어서 변경(Hash를 다시 생성)
        ex) ETag:"64lf5qq24ee8967" => ETag"36uh8mq35dme467"
      - 단순히 ETag만 보내서 같으면 유지, 다르면 다시 받는 방식임
        - 첫번째 요청에서 요청을 받은 서버가 Header에 ETag를 작성해 응답함.
        - 클라이언트의 Cache에서 해당 ETag값을 저장함.
        - 캐시 시간이 초과되서 다시 요청을 해야하는 경우에 `If-None-Match`를 요청 헤더에 작성해서 보냄
        - 서버에서 데이터가 변경되지 않았을 경우, ETag는 동일하기때문에 `If-None-Match`는 false가 됨.
        - 이 경우에 304(Not Modified)를 응답하며, Body는 없고 Header로만 응답함.
        - 브라우저 Cache에서는 서버로부터 받은 응답 결과를 재사용하고 Header데이터를 갱신함
