## Proxy

**클라이언트와 서버 사이에 대리로 통신을 수행하는 것**
=> 해당 기능을 하는 서버를 Proxy Server라고 함

클라이언트, 혹은 서버가 다른 네트워크에 간접적으로 접속할 수 있기 때문에,
보안, 캐싱을 통한 성능 트래픽 분산의 장점을 가짐

### 사용 예시

A나라에 있는 클라이언트에서 특정 데이터가 필요한데, 해당 데이터의 Origin Server는 B나라에 있다고 가정을 해보자.

A -> B로 직접 접근하여 데이터를 가져오는데 2초가 걸린다고하면 A나라의 모든 클라이언트는 2초를 기다려야 해당 데이터를 받을 수 있음.
이를 해결하기 위해 클라이언트와 서버 사이에 Proxy Cache Server를 도입할 수 있다.
A국가에 Proxy Cache Server를 두고, Origin Server에 있는 데이터를 Proxy Cache Server에 넣어놓고, A국가의 클라이언트는 모두 해당 Proxy Cache Server를 통해 자료를 가져오도록 함.

### Proxy-Cache Header

- Cache-Control : public
  - 응답이 public Cache에 저장되어도 괜찮음.
- Cache-Control : private
  - 응답이 해당 사용자만을 위한 것. private Cache에 저장해야함. (기본값)
- Cache-Control : s-maxage
  - Proxy Cache에만 적용되면 유효기간
- Cache-Control : no-cache
  - 데이터는 Cache해도 되지만, 항상 Origin Server에 검증하고 사용.
- Cache-Control : no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안됨 (메모리에서 사용 후 최대한 빨리 삭제)
- Cache-Control : must-revalidate
  - Cache 만료 후, 최초 조회 시 Origin Server에 검증해야 함
  - Origin Server 접근 실패 시, 반드시 오류가 발생해야함 - 504(Gateway Timeout)
  - Cache 유효기간 내라면 Cache를 사용함
- Pragma : no-cache
  - HTTP/1.0 하위호환
  - 확실한 캐시 무효화 응답을 위해서는 해당 Header를 포함한 `no-cache, no-store, must-revalidate`까지 Header에 넣어줘야 함
- Age : 60 (HTTP 헤더)
  - Origin Server에서 응답 후, Proxy Cache 내에 머문 시간(초 단위)

#### no-cache VS must-revalidate

- no-cache의 경우

  - Cache 서버에 요청을 하고 Proxy Cache Server에 도착했을 때 Origin Server에 요청을 하게 됨.
  - 그 후 Origin Server에서 검증 후 304 응답을 하게 됨.
  - 만약 Proxy Cache Server와 Origin Server간 네트워크 연결이 단절되어 접근이 불가능하다면, 오류가 아닌 오래된 데이터라도 보여주자는 개념으로 200(OK)으로 응답을 함.

- must-revalidate의 경우
  - 만약 Proxy Cache Server와 Origin Server간 네트워크 연결이 단절되어 접근이 불가능하다면, 504(Gateway Timeout)오류를 보냄.
  - 중요한 정보가 Origin Server에서 데이터를 못받았다고해서 예전 데이터로 뜨면 큰 문제가 발생할 수 있으니 must-revalidate를 써주는게 좋음.
