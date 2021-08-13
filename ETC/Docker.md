## Docker

**Linux Container 기술을 기반으로 하는 오픈 소스 서비스**

- 어플리케이션 실행 환경을 코드로 작성 가능
- OS를 격리화하여 관리

### Linux Container

**Linux 기반 기술 중 하나. 필요한 라이브러리, 어플리케이션을 모아서 별도의 서버처럼 구성한 것**

- Container는 네트워크 설정, 환경 변수 등의 시스템 자원으로 이루어져있음
- 각 Container가 시스템 자원을 독립적으로 소유하고 있음

#### 특징

1. 프로세스의 구획화
   - 특정 Container에서 작동하는 프로세스는 기본적으로 해당 Container 안에서만 엑세스 가능
   - 특정 Container에서 작동하는 프로세스는 다른 Container의 프로세스에게 영향을 줄 수 없음
2. 네트워크의 구획화
   - 기본으로 각 Container에 IP 주소가 할당되어 있음
3. 파일 시스템의 구획화
   - Container안에서 사용되는 파일 시스템도 구획화가 되어있어, 명령이나 파일 등의 엑세스를 제한할 수 있음.

### Docker를 왜 사용해야 하는가?

- 작업 환경을 표준화할 수 있음
  - 엔지니어들은 자신이 개발하는 어플리케이션이 대표적인 운영체제(Windows, MacOS, Linux)들에서 어떻게 구동될지 생각하고 개발해야함.
  - 어플리케이션마다 환경이 다르기때문에 변경할 부분이 생기기 때문임.
  - 만약 특정 OS에서만 사용한다고 해도, 환경 변수나 홈 디렉토리처럼 사용자에 따라 달라지는 구성이 있음.
  - 개발과 실행에 대한 환경 설정이 코드로 정해져있다면 이러한 고민으로부터 벗어날 수 있고, **가상머신이나 Docker를 사용해 리소스를 격리시킴**으로서 가능함.

#### 리소스 격리성

**실제로는 하나의 컴퓨터를 사용하지만, 여러 개의 컴퓨터를 이용하는 것과 같은 방법**

##### 종류

- 가상머신(VirtualBox, VMware 등) : 개발 환경이나 사용 환경을 이미지로 저장하고, Host운영체제 위에 Guest운영체제를 올리는 방식
- Docker : Host운영체제 위에서 실행하여, 각 개발 환경이나 사용 환경을 격리하여 관리하는 방식

###### 가상머신과 Docker의 차이

- 격리성 : 가상머신 > Docker
- 성능 : 가상머신 < Docker
  - 가상머신과 달리, Docker는 OS위에 다른 OS를 실행하는게 아니므로 더 좋은 성능을 낼 수 있음
- 어플리케이션의 환경 격리성을 중심으로 하는 가상머신
- Container의 관점에서 개발자와 사용자 커뮤니티를 중심으로 혜택을 제공하는 Docker

[Docker CLI Docs](https://docs.docker.com/engine/reference/commandline/container_run/)

### 자주 쓰는 CLI 명령어

#### Image

- `docker image pull <Registry/Repository:tag>` : Registry에서 image 혹은 Repository를 가져옴
- `docker image ls` : image 리스트 출력
- `docker image rm <Registry/Repository:tag>` : 해당하는 image를 삭제. 해당 image가 사용되고있는 Container가 존재한다면 Container쪽을 먼저 삭제한 뒤 image삭제가 가능함

#### Container

- `docker container run --name <Container이름> --rm <Registry/Repository:tag> [Command] <ARG..>`
  - run : Container 실행
  - Options
    - --name : Container의 이름 할당
    - --rm : Container를 일회성으로 실행함. Container가 중지 및 종료될 때 관련 리소스를 모두 제거
      **-- 그외 자주 사용하는 Options --**
    - -p : 로컬호스트와 Container의 포트를 연결. `로컬호스트포트:Container포트`와 같은 방식으로 작성함.
  - Command : 초기 Container 실행 시 수행되는 명령어. image에 따라 다름.
  - ARG.. : Command에 넘겨질 파라미터
- `docker container ps -a`
  - ps : Container 리스트 출력. Default는 실행 중인 Container
  - -a : 종료된 Container를 포함한 모든 Container를 출력
- `docker container rm <Container이름>` : Container를 골라 삭제함. <Container이름>위치에는 ps 명령어를 통해 확인할 수 있는 NAMES 혹은 Container ID를 사용함
- `docker container cp <앞 폴더 경로> <뒤 폴더 경로>` : 앞 폴더 경로에 있는 파일들을 뒤 경로에 복사함.
- `docker container commit <Container이름> <원하는 image Repository명>` : 해당Container 변경 사항을 이용해 Repository의 이름을 가진 새 Image를 만듬.

#### ETC

- `docker build --tag <name:tag> <폴더 경로>` : 폴더 경로에 있는 Dockerfile을 찾아 name:tag 형식으로 image 파일 생성
