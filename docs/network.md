# network

## 공부자료
[x][강좌1~4](https://www.youtube.com/playlist?list=PLXvgR_grOs1BjBZiePPZMR1PmZybazxg6)

[][slides](https://gaia.cs.umass.edu/kurose_ross/ppt.htm)

- 슬라이드로 충분한듯 

~~[] [이대강좌](http://www.kocw.net/home/search/kemView.do?kemId=1046412)~~

~~[][책](http://www.yes24.com/Product/Goods/45543957)~~


## Ch.1 컴퓨터 네트워크와 인터넷
인터넷 - 전 세계적으로 수십업 개의 컴퓨터 장치를 연결하는 컴퓨터 네트워크
- 사물들도 연결되게 때문에 computer network -> host or end system

패킷 - 한 종단 시스템이 다른 시스템으로 보낼 데이터를 가지고 있을 때, 송신 종단 시스템은 그 데이터를 세그먼트로 나누고 각 세그먼트에 헤더를 붙인다. 
- 패킷은 목적지 종단 시스템으로 네트워크를 통해 보내지고, 목적지에서 원래의 데이터로 다시 조립된다.

종단시스템(end system)은 통신 링크와 패킷 스위치(라우터와 링크 계층 스위치)의 네트워크로 연결된다.
- 송신 측과 수신 측 사이에서 각 패킷은 통신 링크와 패킷 스위치를 거치게 된다.

종단시스템은 ISP(Internet Service Provider)를 통해서 인터넷에 접속한다

소켓 인터페이스 - 한 종단 시스템에서 수행하는 프로그램이 어떻게 인터넷 인프라 구조에게 다른 종단 시스템에서 수행되는 특정 목적지 프로그램에게 데이터를 전달하도록 요구하는지를 명시.

프로토콜 - 둘 이상의 통신 개체 간에 교환되는 메시지 포맷과 순서뿐 아니라, 메시지의 송수신과 다른 이벤트에 따른 행동들을 정의
- 어떤 일을 수행하려면 둘 이상의 통신 개체가 함께 인식하는 프로토콜이 필요
- 프로토콜의 정의를 통해 사람들은 상호 호환되는 시스템과 제품을 만들 수 있다

인터넷에서 모든 종단 시스템은 IP 주소라고 하는 주소를 갖는다.
- 소스 종단 시스템이 패킷을 목적지 종단 시스템으로 보내고자 할 때, 소스는 패킷의 헤더에 목적지의 IP 주소를 포함한다.

회선교환(circuit switching) vs 패킷교환(packet switching)
- 링크와 스위치의 네트워크를 통해 데이터를 이동시키는 방식
- 회선 교환이 요구에 관계없ㄷ이 미리 전송 링크의 사용을 할당
- 패킷 교환은 요구할 때만 링크 사용을 할당

회선 교환
- 예약 필요
- 전화망
- 보장된 일정 전송률로 데이터를 보낼 수 있음
- pros
- cons
  - 비활용시간에 낭비 (전화통화 중 이야기를 중단하여도, 다른 네트워크가 사용 불가)
  - 1Mbps를 동시에 10명이만(예시 - 1 Mbps/100 kbps) 지원 (각각의 사용자에게 100 kbps 예약)

패킷 패킷 교환
- 예약 X
- 일정 시간내에 전달 보장 X
- 11명의 사용자가 동시에 활동할 확률이 매우 낮음. -> 10명 이하면 지연 X, 11명이면 지연발생 가능(하지만 확률이낮음)
- pros
  - 전송용량 공유에 더 효율적
  - 간단, 효율, 구현비용이 적음
- cons
  - 가변적, 예측할 수 없는 큐잉지연
  - 실시간 서비스에 맞지 않음

### 라우터에서의 지연

처리지연(processing delay)
- 패킷 헤더를 조사하고 그 패킷을 어디로 보낼지를 결정하는 시간

큐잉지연(queing delay)
- 패킷은 큐에서 링크로 전송되기를 기다린다

전송지연(transmission delay)
- 패킷의 모든 비트를 링크로 밀어데는데 필요한 시간
- 패킷의 길이 L 비트, 링크의 전송률 R bps
  - L/R

전파지연(propagation delay)
- 링크의 처음부터 라우터까의 전파에 필요한 시간
- d (라우터 A-B 사이의 거리), s (링크의 전파속도)
  - d/s

전송지연 vs 전파지연
- 전송지연은 라우터가 패킷을 내보내는 데 필요한 시간(패킷 길이와 전송률의 함수이며, 두 라우터 사이의 거리와는 관계없다)
- 전파지연은 비트가 한 라우터에서 다음 라우터로 전파되는 데 걸리는 시간(두 라우터 사이의 거리에 대한 함수며, 패킷 길이나, 링크 전송률과 관계없다)
예시
- 100km마다 요금계산소(라우터), 고속도로 요금계산소 사이(링크), 차 시속 100km 속도 유지, 10대의 차가 순서대로 줄을 맞추어 달린다는 가정, 각 자동차(bit), 10대 전체(패킷), 각 요금계산소는 12초마다 한 대의 차를 서비스(전송)
- 요금계산소가 전체 자동차를 밀어내는 데 걸리는 시간 2분 (전체 차량대열이 전송되기 전에 요금계산소에 저장 되어야 함) (라우터에서의 전송 지연)
- 한 자동차가 한 요금계산소에서 다음 계산소로의 이동에는 100km(100km/hour) 1시간이 걸림 (전파지연)

큐잉지연
- 큐에 도착하는 평균를 a(패킷/초), R 전송률 비트가 큐에서 밀려나는 비율(비트/.초), 편의상 모든 패킷이 L비트라고 가정,비트가 큐에 도착하는 평균율은 La 비트/초, 큐가 매우 커서 무한대 비트를 저장한다고 가정
- traffic intensity - La/R
  - La/R > 1이면, 비트가 큐에 도착하는 평균율이 비트가 큐에서 전송되는 비율을 초과, 이 경우에 큐는 긑없이 증가하고 큐잉지연은 무한대에 도달한다
  - 트래픽 강도가 1보다 크지 않게 시스템을 설계하라
  -  La/R <= 1인 경우, 패킷이 주기적으로 도착한다며나, 즉 하나의 패킷이 L/R초마다 도착한다면, 이때 모든 패킷은 빈 큐에 도착할 것이고 큐잉 지연이 없다
  - 반면에 N개 패킷이 동시에 (L/R)N 초마다 도착한다고 하자. 그러면 처음에 전송된 패킷은 큐잉 지연이 없다. 하지만 두번째 전송된 패킷은 L/R초의 지연을 가진다. n 번째 전송된 패킷은 (n-1)L/R 초의 큐잉 지연을 겪는다.
  - 트래픽강도가 1에 가까워질수록 지연(도착률 > 전송속도), 0에 가까워질수록 큐의 길이는 줄어듦(도착률 < 전송속도)

패킷손실
- 큐의 용량은 유한함
- 트래픽 강도가 1의 가까워질 때, 저장할 수 없는 패킷의 경우, drop -> lost하게 된다. 
- 손실 패킷은 모든 데이터가 궁극적으로 출발지에서 목적지까지 전달되었다는 것을 보장하기 위해 종단간에 재전송 될 수 있다

종단간 지연
출발지 호스트와 목적지 호스트 사이에 N-1개의 라우터가 있다고 가정, 네트워크 혼잡X(큐잉 지연 무시), 각 라우터와 출발지 호스트의 처리 지연은 dproc, 각 호스트와 출발지 호스트에서의 전송률은 R 비트/초, 각 링크에서 전파 지연은 dprop
d(end-end) = N(drpoc + dtrans + dprop)
- dtrans = L/R

프로토콜 계층과 서비스 모델
- 비행기에 의해 출발지에서 목적지로 수송

티켓(구입)    ---   티켓(항의)

수하물(검사)   --   수하물(클레임)

탑승구(탑승)   --   탑승구(하차)

활주로 이륙    --   활주로 착륙

비행기 라우팅  ---  비행기 라우팅

   --  비행기 라우팅  -- 

- 각 계층은 아래 게층과 연계하여 어떤 기능, 서비스를 구현한다.
- 티켓팅 계층과 그 아래에서는 카운터 간에 사람의 전송이 이루어진다.
- 수하물계층과 그 아래에서는 수하물 창구사이에서 사람과 수하물의 전송이 이루어진다.
  - 수하물 계층에서는 이 서비스를 이미 티켓을 가진 승객에게만 제공함을 유의
- 탑승구 계층에서는 사람과 수하물의 출발-탑승구와 도착- 탑승구 사이에서 전송이 이루어진다.
- 이륙/착륙 계층에서는 사람과 수화물의 활주로와 활주로 사이에서 전송이 우러어진다.
- 각 계층은 1. 그 계층에서 어떤 동작을 취하고(탑승구 계층에서 비행기에 사람을 오르내리게 하는 것) 2. 그 계층 바로 아래 계층 서비스를 이용함으로써(탑승구 계층에서 이착륭 계층의 활주로와 활주로 간의 승객 이동을 이용하는 것) 서비스를 제공
** 시스템이 계층구조를 가질 떄, 그 계층이 제공하는 서비스의 구현을 변경하는 것이 쉬워짐**

애플리케이션 계층
- 네트워크 애플리케이션과 애플리케이션 계층 프로토콜이 있는 곳
  - HTTP(웹 문서 요청과 전송), SMTP(전자메일 전송), FTP(두 종단 시스템 간의 파일 전송)
- 사람에게 친근한 www.___.com 이 32비트 네트워크로 주소로 변환하는 네트워크 기능 (DNS가 도움)
- 한 종단 시스템에 있는 애플리케이션이 다른 종단 시스템에 있는 애플리케이션과 정보 패킷을 교환하는데 프로토콜을 사용
  - 정보 패킷 - message

트랜스포트 계층
- 클라이언트와 서버 간에 애플리케이션 계층 메시지를 전송하는 서비스
  - TCP, UDP 프로토콜 (애플리케이션 계층 메시지를 전달)
    - TCP - 애플리케이션에 연결지향형 서비스를 제공: 목적지로의 애플리케이션 계층 메시지 전달 보장과 흐름제어, 긴 메시지를 짧은 메시지로 나누고 혼잡제어 기능 제공, 네트워크가 혼잘할 때 출발지의 전송속도를 줄임
    - UDP - 비연결형 서비스를 제공: 신뢰성, 흐름제어, 혼잡제어를 제공하지 않는 아주 간단한 서비스
- 트랜스포트 계층 패킷 - segment

네트워크 계층
- 한 호스트에서 다른 호스트로 datagram을 라우티하는 책임을 진다.
  - 메일 서비스를 이용하기 위해 목적지 주소가 적힌 편지를 전달하는 것처럼, 출발지 호스트에서 인터넷 트랜스포트 계층 프로토콜(TCP or UDP)은 트랜스포트 계층 세그먼트와 목적지 주소를 네트워크 계층으로 전달. 
  - 그 다음에 네트워크 계층은 목적지 호스트의 트랜스포트 계층으로 세그먼트를 운반하는 서비스를 제공
- 네트워크 계층은 두 가지 주요 요소를 갖는다
  - IP 데이터그램의 필드를 정의하며 종단 시스템과 라우터가 이 필드에 어떻게 동작하는 지 정의하는 프로토콜을 갖고 있다.(IP protocol)
  - 출발지와 목적지 사이에서 데이터그램이 이동하는 경로를 결정하는 라우팅 프로토콜을 포함한다.
- IP 프로토콜가 여러 라우팅 프로토콜을 갖고 있지만, IP 계층으로 불림
- 네트워크 계층 패킷 - datagram

링크 계층
- 네트워크 계층은 출발지와 목적지 간 일련의 패킷 스위치(라우터)를 통해 데이터그램을 라우트한다.
  - 경로상의 한 노드(호스트 혹은 패킷 스위치)에서 다른 노드로 패킷을 이동하기 위해, 네트워크 계층은 **링크 계층 서비스에 의존**해야한다.
  - 각 노드에서 네트워크 계층은 데이터그램을 아래 링크 계층으로 보내고, 링크 계층은 그 데이터그램을 경로사으이 다음 노드에 전달한다. 다음 노드에서 링크 계층은 그 데이터그램을 상위 네트워크 계층으로 보낸다.
- 링크 계층에서 제공하는 서비스느 그 링크에서 채용된 특정 링크 계층 프로토콜에 의해 결정된다.
  - 예) 이더넷, 와이파이 그리고 케이블 접속 - DOCSIS 프로토콜
- 링크 계층 패킷 - frame

물리 계층
- 링크 계층의 기능이 전체 프레임을 한 네트워크 요소에서 이웃 네트워크 요소로 이동하는 것이라면, **물리 계층의 기능은 프레임 내부의 각 비트를 한 노드에서 다음 노드로 이동하는 것**
  - 프로토콜들은 링크에 의존하고 더 나아가 링크의 실제 전송 매체에 의존한다

OSI 모델
OSI 7 layer - 애플리케이션, 프레젠테이션, 세션, 트랜스포트, 네트워크, 데이터 링크, 물리 계층
- 프레젠테이션 계층
  - 통신하는 애플리케이션들이 교환되는 데이터의 의미를 해석하는 서비스를 제공
  - 데이터 기술(애플리케이션이 데이터가 표현/저장되는 내부 포맷을 걱정하지 않아도 되게 해준다)뿐만 아니라 데이터 압축과 데이터 암호화를 포함 
- 세션 계층
  - 데이터 교환의 경계와 동기화를 제공(체킹포인트와 회복 방법)
2개 개층이 없는 이유
- 필요에따라 서비스를 애플리케이션 개발자가 애플리케이션에 넣을 수 있음

캡슐화
- 송신하는 종단 시스템의 프로토콜 스택의 아래로 데이터를 보내며, 중간의 링크 계층 스위치와 라우터의 프로토콜 스택을 위아래로 거치고, 수신하는 종단 시스템의 프로토콜 스택 상위로 보내는 물리적 경로.
  - 프로토콜의 모든 계층을 구현하지 않음, 일반적으로 이들은 하위 계층을 구현,
    - 링크 계층 스위치는 1~2계층(물리,링크)
    - 라우터는 1~3 계층
    - 호스트는 1~5 계층 모두 구현
1. 송신 호스트에서 **애플리케이션 계층 메시지**는 트랜스포트 계층으로 보내진다. 
2. 트랜스포트 계층은 메시지에 수신 측 트랜스포트 계층에서 사용될 추가 정보를 더한다. **애플리케이션 계층 메시지와 트랜스포트 계층 헤더 정보는 모두 트랜스포트 계층 세그먼트를 구성**한다. (트랜스포트 계층 세그먼트는 애플리케이션 계층 메시지를 캡슐화한다.)
  - 추가된 정보는 수신측의 트랜스포트 계층이 그 메시지를 적절한 애플리케이션으로 보내도록 하는 정보와 메시지의 비트들이 변경되었는지 아닌지를 결정하게 하는 오류 검출 비트를 포함한다.
3. 트랜스포트 계층은 세그먼트를 네트워크 계층으로 보내며 **네트워크 계층은 출발지와 목적지 종단 시스템 주소와 동일한 헤더정보를 추가하여 네트워크 계층 데이터그램을 만든다.**
4. 이 데이터그램은 링크 계층으로 전달되고 **링크 계층도 자신이 헤더 정보를 추가하고 링크 게층 프레임을 만든다.**


## Ch2 Application Layer
Client-server paradigm
- server: permanent IP address
  - always-on host
- clients: may have dynamic IP addresses
  - contact, communicate with server, do not communicate directly with each other
- example: HTTP, IMAP, FTP

Peer-peer architecture
- arbitrary end systems directly communicate
- example: P2P file sharing

Process communicating
- within same host, two process communicate using **inter-process-communication**
- processes in different hosts communicate by exchanging **messages**

Sockets
- process sends/receives messages to/from its socket

To receive messages, process must have identifier
- includes both IP address and port numbers associated with process on host.

TCP
- reliable transport b/w sending and receving process
- flow control: sender won't overhelm receiver
- congestion control: throttle sender when network overloaded
- connection-oriented: setup required between client and server processes
- does not provide: timing, minimum throughput guarantee, security

UDP
- unreliable data transfer b/w sending and receiving process
- does not provide: reliability, flow control, congestion control, timing, throughput guarantee, security, or connection setup.

HTTP: hypertext transfer protocol
- uses TCP
- stateless

Non-persistent HTTP
1. TCP connection opened
2. at most one object sent over TCP connection
3. TCP connection closed
- response time = 2RTT + file transmission time


Persistent HTTP
1. TCP connection opened to a server
2. multiple objects can be sent over single TCP connection b/w client and server
3. TCP connection closed

RTT: tiem for a small packet to travel from client to server and back

HTTP request messages
POST, GET, HEAD, PUT

HTTP response status codes
status code appears in 1st line in server-toclient response message.
- 200 OK
  - request succeeded, requested object later in this message
- 301 Moved Permanetly
  - requested boject moved, new location specified later in this message
- 400 Bad Request
  - request msg not understood by server
- 404 Not Found
  - requested document not found no this server
- 505 HTTP Version Not Supported

cookies
- HTTP GET/response interactino is stateless
- Web sites and client browser  use cookies to maintain some state between transactions
- four components:
1. cookie header line of HTTP response message
2. cookie header line in next HTTP request message
3. cookie file kept on user’s host, managed by user’s browser
4. back-end database at Web site
used for:
- authorization
- shopping carts
- recommendations
- user session state

Web caches (aka proxy servers)
- Goal: satisfy client requests without involving origin server
- user configures browser to point to a (local) Web cache
- browser sends all HTTP requests to cache
  - if object in cache: cache returns object to client
  - else cache requests object from origin server, caches received object, then returns object to client
- Web cache acts as both client and server

Conditional GET
- Goal: don’t send object if cache has up-to-date cached version
- client: If-modified-since: <date>
- server: HTTP/1.0 304 Not Modified

HTTP/2
- Key goal: decreased delay in multi-object HTTP requests
- HTTP1.1:
  - server responds in-order(FCFS)
  - with FCFS, small object may have to wait for transmission  (head-of-line (HOL) blocking) behind large object(s)
  - loss recovery (retransmitting lost TCP segments) stalls object transmission
- HTTP2:
  - incread flexibility at server in sending objects to client
  - transmission order of requested objects based on client-specified object priority (not necessarily FCFS)
  - divide objects into frames, schedule frames to mitigate HOL blocking

HTTP/3
- adds security, per object error- and congestion-control (more pipelining) over UDP

E-mail
- user agents
- mail servers
- SMTP
  - protocol b/w mail servers to send email messages
    - client: sending mail server
    - server: receiving mail server


DNS: Domain Name System
- hostname-to-IP-address translation
- host aliasing
- load distribution

Root, Top Level Domain, Authoritative

tit-for-tat
- every 30 secs: randomly select another peer, starts sneding chunks (optimistically unchoke)

Streaming multimedia: DASH(Dynamic, Adaptive, Streaming over HTTP)
- sever
  - divides video file into multiple chunks
  - each chunk encoded at multiple different rates
- client
  - periodically estimates server-to-client bandwidth
  - can choose different coding rates at different points in time (depending on available bandwidth at time), and from different servers

CDN(Content distribution networks)
- challenge: how to stream content (selected from millions of videos) to hundreds of thousands of simultaneous users?
  1. single, large "mega-server"
  2. store/serve multiple copies of videos at multiple geographically distributed sites


## Ch3 Transport Layer
provide logical communication b/w application processes running on different hosts
- sender: breaks application messages into segments, passes to network layer
- receiver: reassembles segments into messages, passes to application layer
- TCP, UDP
  - UDP: demultiplexing using destination port number(only)
  - TCP: demultiplexing using 4-tuple: source and destination IP addresses, and port numbers
transport layer: logical communication between **processes**
network layer: logical communication between **hosts**
- host receives IP datagrams
  - each datagram has source IP address, destination IP address
  - each datagram carries one transport-layer segment
  - each segment has source, destination port number
- host uses **IP addresses & port numbers** to direct segment to appropriate socket

UDP: User Datagram Protocol
- best effort service
- connectionless

UDP checksum
- Goal: detect errors (i.e., flipped bits) in transmitted segment

rdt = Reliable data transfer protocol
rdt1.0: no error

rdt2.0: channel with bit erros
- ACKs: receiver explicitly tells sender that pkt received OK
- NAKs: receiver explicitly tells sender that pkt had errors
  - sender retransmits pkt on receipt of NAK
  - stop and wait: sender sends one packet, then waits for receiver response

rdt2.1: sender, handling garbled ACK/NAKs
- in case ACK/NAK corrupted
  - sender retransmits current pkt with sequence number to each pkt
  - receiver discards duplicate pkt

rdt2.2: a NAK-free protocol
- same functionality as rdt2.1, using ACKs only
- instead of NAK, receiver sends ACK for last pkt received OK

rdt3.0: channels with errors and loss
- New channel assumption: underlying channel can also lose packets (data, ACKs)
- Approach: sender waits “reasonable” amount of time for ACK 
  - retransmits if no ACK received in this time
  - if pkt (or ACK) just delayed (not lost):
  - use countdown timer to interrupt after “reasonable” amount of time
- pipelining
  - go-back-N
    - sender: "window" of up to N
      - cumulative ACK
    - receiver: always send ACK for correctly-received packet so far, with highest in-order seq #
  - selective repeat
    - receiver individually acknowledges all correctly received packets
    - buffer

TCP flow control (application에서 과다): one sender too fast for one receiver
- what happens if network delivers data faster than applicatino layer removes data from socket buffers?
- a mechanism to the calamity of a receiver being over-run by a sender that is sending too fast – it allows the RECEIVER to explictly control the SENDER so sender won’t overflow receiver’s buffer by transmitting too much, too fast 
- the receiver informs the sender how much free buffer space there is, and the sender is limited to send no more than this amount of data.  

Contestion control (network layer에서 과다): too many senders, endeing too fast
- “too many sources sending too much data too fast for network to handle”

TCP congestion control: AIMD(Additive Increase Multiplicative Decrease)
- senders can increase sending rate until packet loss (congestion) occurs, then decrease sending rate on loss event

TCP congestion control: details
- TCP sender limits transmission: LastByteSent - LastByteAcked <= cwnd
  - cwnd is dynamically adjusted in response to boserved network congestion

TCP slow start
- initial rate is slow, but ramps up exponentially fast

QUIC: Quick UDP Internet Connections
- application-layer protocol, on top of UDP
