

## Thread 
- https://goodgid.github.io/What-is-Thread/
- https://afteracademy.com/blog/difference-between-mutex-and-semaphore-in-operating-system
- 프로세스
    - 실행 중인 프로그램
    - 메모리에 공간을 할당 받아 실행 중
    - 프로세스는 운영체제로부터 자원을 할당받는 작업의 단위
- 쓰레드
    - 프로세스내에서 실제로 작업을 진행하는 주체
    - 쓰레드는 프로세스가 할당받은 자원을 이용하는 실행의 단위
    - 코드, 데이터, 자원 -> 공유
    - PC, SP, Regiester, stack
        - 독립적인 작업을 수행하기 위함
- 차이:
    - Context Switching이 빠르다: 쓰레드는 프로세스보다 생성 및 종료시간, 쓰레드간 전환시간이 짧다
    - 자원 공유: 쓰레드는 프로세스의 메모리, 자원등을 공유하므로 커널의 도움없이 상호간에 통신이 가능
- Lock
    - 쓰레드의 경우 데이터, 자원 및 코드를 공유하기 떄문에 동기화 문제가 많이 발생
    - Mutex (mutual exclusion)
        - mutex object를 통해 process에 들어갈 수 있는 권한이 생김
            - critical section에 들어갈 때, mutex object를 생성해야 들어감
            - 그리고 다른 프로세스들은 생성 못함
        - locking mechanism

    - Semaphore
        - semaphore가 integer로.. 몇개의 프로세스가 임계구역에 접근
        - signaling mechanism
            - wait() and signal() methods
- Deadlock
    - 발생조건
        1. Mutual Exclusion
        2. Hold and Wait
        3. No Preemtion
        4. Circular wait
    - 해결법
        1. Deadlock Prevension
            - 그닥.?
        2. Deadlock Avoidance
            - Banker's algorithm
        3. Deadlock detect & recover
            - Preemption 또는 프로세스 일부 강제 종료
        4. 무시

## 서버에서 여러 연결을 효율적으로 처리하는방법
- IOCP
    - 뭔가 자바스크립트 콜백을 통한 비동기랑 비슷한듯?
    - 윈도우에서 사용함
    - 
- epoll

## DB
- Transaction
    - 데이터베이스의 상태를 변화시키는 하나의 논리적 기능을 수행하기 위한 작업단위로 한꺼번에 모두 수행되어야하는 연산들
    - ACID
        - Atomicity - transaction이 모두 반영되거나 하날도 안되면 rollback
        - Consistency - transaction이 일어나는 동안 DB에 변화가 있어도, 기존에 reference한 데이터를 기준으로 transaction 진행
        - Isolation - 동시에 Transaction이 일어나는 경우, 서로의 transaction에 연사작용을 할 수 없는 것, 즉 수행이 끝날때까지, 다른 transaction의 결과를 참조할 수 없음
        - Durability - transaction 성공적으로 이뤄지면, 영구적으로 적용
- SQL
    - DDL(Data Deifintion Language)
        - 데이터베이스를 정의하는 언어(테이블 구조 생성)
        - CREATE, ALTER, DROP, TRUNCATE
    - DML(Data Manipulation Language)
        - 데이터베이스의 입력된 레코드를 조회, 수정 삭제하는 언어
        - SELECT, INSERT, UPDATE, DELETE
    - DCL(Data Control Language)
        - 데이터베이스에 접근하거나 객체에 권한을 주는 역할을 하는 언어
        - GRANT, REVOKE, COMMIT, ROLLBACK
- Stored Procedure (DB에 함수 저장)
- NoSQL
    - SQL이 아닌 JSON형식의 트리형태의 DB

## 서버 클라이언트 통신
- 게임 네트워크
    1. 지연시간(latency)
    2. 연결안정성
    3. 순서비보장
- TCP,UDP
    - TCP
        - 연결 유무 확인하고 (3 way handshake)
        - 순서를 보장하고
        - 송신도 보장!
        - MMORPG, 보드게임...
    - UDP
        - 연결 유무 x
        - 순서보장 x
        - 송신보장 x
        - Reliable UDP로 보완
        - 격투게임, 슈팅게임 롤, ...
- 어떻게 동기화를 할 것인가
- 메시지를 어떤 방식으로 보낼 것인가

- 주소창에 입력하면 (www.google.com) : 학교에와서 laptop을 연결하고 brower에 url 타이핑
    1. 컴퓨터를 키면 DHCP(client program)가 실행됨 (DHCP는 UDP protocol을 이용)
        - 인터넷 접속을 위한 IP주소 할당을 받아야함(처음에 네트워크에 들어오면 IP주소가 없음)
        - 인터넷에 접속하기 위한 addr of first hop router
        - DNS서버에 www.google.com의 ip주소를 알아야함
    2. DHCP를 내보내는 상황에서 네트워크에 아는 상황이 없으므로, local network에 broadcasting
        - 그 중에 DHCP server process를 담고 있는 노드만 관심을 갖음 (router가 DHCP서버를 탑재하고 있다면)
        - DHCP server process까지 올라가고 DHCP ACK 브로드캐스트
        - 그러면 DHCP 메시지를 만든 노트북만 관심을 가짐
        - Client는 이제 본인의 ip addr, dns server의 name & addr , ip addr of first-hop of router
    3. DNS client process를 구동시킴 (HTTP request를 보내려면, DNS서버와의 connect가 필요함)
        - google.com의 ip 주소를 얻기 위함
        - DHCP를 통해 알아낸 DNS 서버 ip 주소가 들어감
        - first hop of router의 mac주소를 모름, ARP query 브로드캐스팅을 통해 알아냄 (router가 응답!)
    4. first hop of router에 도착하여 메시지를 보면, IP주소에는 DNS server 주소가 적혀있음
        - routing protocol (RIP, OSPF, Is-IS, BGP)
        - 목적지 서버로 도착
        - DNS 서버에서 google.com의 ip주소 정보를 보내줌
    5. 드디어 google.com으로 HTTP request
        - TCP위에서 동작함으로, connection setup을 해야함
            - 웹서버로 SYNC 메시지를 보냄 (transport 계층에서 만든 것이므로, application layer까지 안가도 됨)
            - 웹서버에서 다시 클라이언트로 (SYNC, ACK)
            - client에서 다시 (ACK을 보내며, 드디어 HTTP 메시지를 보냄) (여기도 application layer까지 안감)
            - 여기서 IP계층의 목적지는 웹 서버(google.com)가 적혀있음
                - 목적지를 가기위한 다음 홉은 First hop of router
                - 다음 홉을 가기위한 frame의 source MAC addr: 노트북, destination MAC addr: first hob of router addr
                - router는 routing table을 보고 다음 홉 어디 다음 홉 어디 Frame의 MAC addr 홉 바이 홉으로 건너감
                    - ARP는 일정시간 캐싱됨!( first hop of router의 위치를 20분동안 캐싱중)
                    - Router에서 다음 홉을 갈 때도, ARP를 다하고 캐싱!
            - 서버에 도착하면, 다시 클라이언트로 주고 결과물을 줌! 드디어 화면 display!