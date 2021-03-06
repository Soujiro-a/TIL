## Deploy

**개발한 서비스를 사용자가 이용가능하게 하는 과정**

### 과정

1. Development
   - Local 환경에서 개발 및 테스트
   - Sample Data, Dummy Data를 이용
   - 변경사항이 있어도 문제가 되지 않음
   - 모든 구성원이 각자 환경에서 진행
2. Intergration
   - 각자 환경에서 개발된 부분을 취합
   - 코드 충돌이 없는지 확인
   - 코드가 다른 코드에 문제를 일으키진 않는지 확인
3. Staging
   - Production단계와 가장 유사한 환경에서 테스트
   - 복제된 실제 데이터를 이용해 테스트
   - 모든 관계자들에게 검증하는 단계
4. Production
   - 개발환경과는 구분 된 환경
   - 실제 데이터를 이용
   - 실제 서비스가 제공되는 단계

### 주의점

- 각자 환경이 다르기 때문에, **환경 설정을 코드와 분리하는 것**이 중요
  => 작성한 코드가 다른 환경에서 작동할 수 있게 하려면? 1. 상대 경로 사용 2. 환경에 따라 포트를 분기할 수 있도록 환경변수 설정 3. Docker와 같이 개발 환경 자체를 통일시키는 솔루션 사용
  => 어플리케이션의 모든 설정이 코드와 분리되어있는지 확인하기 위해서는? - 어떠한 인증정보의 유출 없이 오픈 소스가 될 수 있는지를 확인하는 것

### Deploy Strategy

내가 개발한 서비스를 외부 사용자들이 접속할 수 있게 하려면?
=> AWS S3를 이용해 정적파일로 **Build**하여 Client 어플리케이션을 배포할 수 있음

AWS S3를 통해 Client 어플리케이션을 제공하고 있는 상황에, 사용자가 멀리 떨어져있는 경우에서 더 빠르게 서비스를 제공하려면?
=> AWS CloudFront를 통해 데이터를 분산시켜 저장해뒀다가 가까운 지역에서 데이터를 주는 방식으로 더 빠르게 서비스 제공이 가능함

Client 어플리케이션을 통해 요청과 응답을 주고받을 Server를 배포하려면?
=> 안정적인 서비스 제공을 위해 AWS EC2와 같은 가상의 PC를 빌려 서버코드를 구동할 수 있음

데이터베이스를 사용하려면?
=> 직접 구축하는 건 시간과 노력이 더욱 많이 들어가기 때문에, RDS 서비스를 이용해 Server 데이터를 저장, 제공하는 데이터베이스를 배포하는게 좋음

도메인을 통해 서비스에 접속하려면?
=> AWS Route53을 사용하여 직관적인 도메인 주소를 작성하고 해당 주소를 이용해 서비스에 접근하도록 할 수 있음.

#### Build

- 불필요한 데이터를 없애고, 통합 및 압축을 통해 배포하기 최적화 된 상태를 만드는 것
- 데이터 용량이 줄어들고, 웹 사이트 로딩 속도가 증가함
