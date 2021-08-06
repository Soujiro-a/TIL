## TCP(Transmission Control Protocol) : 전송 제어 프로토콜

### TCP/IP 4 계층(+OSI 7 계층)

|       TCP/IP 4계층       |                              OSI 7계층                               |
| :----------------------: | :------------------------------------------------------------------: |
|    어플리케이션 계층     |     응용 계층(Application Layer)<br>`HTTP, DNS, SSL, SMTP, FTP`      |
|    어플리케이션 계층     | 표현 계층(Presentation Layer)<br>`JPEG, GIF, MPEG, ZIP, ASCII, MIME` |
|    어플리케이션 계층     |       세션 계층(Session Layer)<br>`SQL, Sockets, RPC, NETBOIS`       |
|        전송 계층         |           전송 계층(Transport Layer)<br>`TCP,UDP, NETBEUI`           |
|       인터넷 계층        |              네트워크 계층(Network Layer)<br>`IP, ICMP`              |
| 네트워크 인터페이스 계층 |      데이터 링크 계층(Data Link Layer)<br>`Ethernet, FDDI, PPP`      |
| 네트워크 인터페이스 계층 |    물리 계층(Physical Layer)<br>`CDMA, GSM, NICs, CSMA/CD, Fiber`    |

- TCP/IP 4 계층이 OSI 7 계층보다 먼저 개발되었음.
- 두 계층의 나열 부분이 정확하게 일치하지는 않음.
- **IP보다 TCP가 더 높은 계층에 존재하기 때문에 IP의 한계를 보완할 수 있음**

### 계층 이동을 통한 전달 (OSI 7 계층 기준)

1. 응용 계층에서 표현 계층으로 내려오면서 헤더가 붙는다.
2. 세션 계층까지 오면서 데이터가 만들어짐.
3. 전송 계층으로 내려오면서 전송 계층의 헤더가 붙게 되어 Segment가 된다.
4. 네트워크 계층으로 내려오면서 네트워크 계층의 헤더가 붙으면서 Packet이 된다.
5. 데이터 링크 계층에서는 데이터 링크 계층의 헤더와 *FCS라는 tailer가 붙으면서 Frame이 된다.
   => *FCS(Frame Check Sequence) : Frame 끝 부분에 수신측의 에러검출을 돕기 위해 삽입하는 Field
6. 물리 계층에서 Ethernet Header(Preamble, SFD 등)이 붙고, 이를 BitStream을 통해 Bit로 바꾸어 전송하게 됨.
7. 전송이 된 후에는 역순으로 처리되어 물리 계층 => 응용 계층으로 이동한다.

- 응용 계층 => 물리 계층 : Encapsulation. 물리 계층 => 응용 계층 : De-encapsulation

#### 계층 별 데이터 단위

- 응용, 표현, 세션 계층 : Data
- 전송 계층 : Segment
- 네트워크 계층 : Packet
- 데이터 링크 계층 : Frame
- 물리 계층 : Bit

### TCP Segment 정보

- 출발지 Port(원본 Port), 목적지 Port(도착 Port)가 있으며, IP Packet의 출발지 및 도착지 IP 정보를 보완할 수 있음.
- 그 외에도, 전송 제어, 순서, 검증 정보 등을 포함하고 있음.

### TCP 특징

- 연결 지향 - TCP 3 way handshake
  1.  클라이언트는 서버에 접속을 요청하는 SYN 패킷을 보냄
  2.  SYN요청을 받은 서버는 클라이언트에게 SYN과 ACK가 설정된 패킷을 발송함
  3.  SYN+ACK 패킷을 받은 클라이언트는 서버에게 ACK를 보냄
  - 위 3개의 handshake가 끝난 뒤에 클라이언트는 서버에게 데이터를 보내는게 가능
  - 혹은, 클라이언트가 서버에게 ACK를 보낼 때 데이터도 같이 전송할 수 있음.
  - SYN : Syncronize, ACK : Acknowledgement
- 데이터 전달 보증
  - 데이터 전송이 성공적으로 이루여졌다면 이에 대한 응답을 돌려줌
- 순서 보장
  - 클라이언트에서 패킷을 보낼 때, 서버에 패킷 순서대로 도착하지 않는다면 다시 패킷 전송을 요청할 수 있음.
    => 이를 통해 비신뢰성(순서를 보장하지 않음)을 보완할 수 있음.
- 신뢰할 수 있는 프로토콜

### UDP(User Datagram Protocol)의 특징

- 비 연결 지향
- 데이터 전달을 보증하지 않음
  - 데이터 수신 여부를 확인하지 않음
- 순서를 보장하지 않음
- 단순하고 빠름
- 신뢰성보다 연속성이 중요한 서비스에서 자주 사용됨
  ex) 라이브 스트리밍
