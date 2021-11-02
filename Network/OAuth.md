## OAuth

**OAuth2.0 : 인증을 위한 표준 프로토콜의 한 종류**
보안된 리소스에 엑세스하기 위해 클라이언트에게 권한을 제공하는 프로세스를 단순화하는 프로토콜 중 한 방법

### OAuth를 사용하는 이유

- 유저 입장에서는 많은 웹 서비스를 이용하고있고, 이 서비스들을 이용하기위해서는 각 서비스마다 회원가입 절차가 필요함. OAuth를 활용하면 중요한 서비스들의 ID와 Password만 기억해놓고, 해당 서비스를 통해서 소셜 로그인이 가능해져서 편리성이 비약적으로 상승함.
- 보안상의 이점으로는 검증되지 않은 앱에서 OAuth를 사용하여 로그인을 할 경우에도 유저의 민감한 정보가 해당 앱에 노출 될 일이 없고, 인증 권한에 대한 허가를 미리 유저에게 구해야해서 안전하게 사용이 가능함.

**그러나, 여전히 사용자 정보가 내 서버에 저장이 되는 것에는 변함이 없기때문에, 접근 권한 관리는 자기 서버의 몫이고, OAuth가 모든 것을 해결해주지는 않는다.**

### OAuth에서 알아야 할 용어들

- Resource Owner : 액세스 중인 리소스의 유저.
  ex) 'A'유저가 Github계정을 이용해 어떤 앱에 로그인 할 경우, Resource Owner는 유저 'A'임
- Client : Resource owner를 대신하여 보호된 리소스에 액세스하는 응용프로그램.
- Resource server : client의 요청을 수락하고 응답할 수 있는 서버.
  Authorization server : Resource server가 액세스 토큰을 발급받는 서버. 클라이언트 및 리소스 소유자를 성공적으로 인증한 후 액세스 토큰을 발급하는 서버를 일컬음.
- Authorization grant : 클라이언트가 액세스 토큰을 얻을 때 사용하는 자격 증명의 유형입니다.
- Authorization code : access token을 발급받기 전에 필요한 code. client ID로 이 code를 받아온 후, client secret과 code를 이용해 Access token 을 받아옴.
- Access token : 보호된 리소스에 액세스하는 데 사용되는 credentials. Authorization code와 - client secret을 이용해 받아온 이 Access token을 이용해 resource server에 접근을 할 수 있음.
- Scope : scope는 토큰의 권한을 정의함. 주어진 Access token을 사용하여 액세스할 수 있는 리소스의 범위.

### grant type

**클라이언트 앱이 엑세스 토큰을 얻는 방법. 여러가지 방법이 존재함**

1. Authorization Code Grant Type

   - 엑세스 토큰을 받아오기 위해 먼저 Authorization code를 받고나서 Access token과 교환하는 방법
   - 이 방법에서 Authorization code를 받아오는 절차를 거치는 이유는 보안성 강화 때문임.
   - Client에서 secret을 공유하고 엑세서 토큰을 가지고 오는 과정에서 탈취당할 위험이 있어서, Authorization code만 받아오고 서버에서 Access token 요청을 진행함.

2. Refresh Token Grant type

   - 유효 기간이 지나서 만료된 엑세스 토큰을 편리하게 다시 받아오기 위해 사용하는 방법
   - 일반적으로 Access token보다 Refresh token의 유효 기간을 더 길게 설정하기 때문에 가능한 방법
   - 서버마다 Refresh token에 대한 정책이 다르기 때문에 Refresh token 사용을 위해서는 해당 서버의 정책을 살펴봐야함

### 장점

- 유저 진입 장벽이 매우 낮아짐(원 클릭 로그인)
- 유저가 비밀번호를 기억할 필요가 없어짐
- 유저의 허용 여부에 따라 이메일, 프로필 사진, 닉네임 등의 기본정보를 얻을 수 있음
