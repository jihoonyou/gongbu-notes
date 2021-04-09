# REST API

rest스럽지 않다? rest가 아닌 것 같다?
- rest의 모호함..
- REpresentational State Transfer
  - a way of providing interoperability between computer systems on the Internet

REST의 시작 (역사)
- WEB (1991)
 - Q: 어떻게 인터넷에서 공유할 것인가?
 - A: 정보들을 하이퍼텍스트로 연결한다. 표현방식: HTML, 식별자: URI, 전송방법: HTTP (HTTP는 HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 프로토콜입니다)
- HTTP/1.0 (1994-1996)
 - "How do I imporve HTTP without breaking the Web?" - 기존의 HTTP로 구현된 웹을 망가트리지않고 어떻게 HTTP 더 좋게?
- REST (2000)
 - 박사 논문으로 나옴
- CMIS (2008)
- Micorosoft REST API Guidelines (2016)

REST API
- REST 아키텍쳐 스타일을 따르는 API

REST
- 분산 하이퍼미디어 시스템(예: 웹)을 위한 아키텍쳐 스타일

아키텍쳐 스타일
- 제약조건의 집합 (즉 제약조건을 다 따라야 REST라고 하는듯?)

REST를 구성하는 스타일
- client-server, stateless, cache, uniform interface, layered system, code-on-demand(optional)
 - code-on-demand(코드를 서버에서 보내서 실행하는 것)
 - uniform interface가 만족하기 힘듦

Uniform Interface의 제약조건
- identification of resources
 - resource가 URI로 식별되면 된다
- manipulation of reousrces through representations
 - 리소스를 만들거나 업데이트하거나 삭제할 때, 메시지에 표현을 담아 조건을 달성하는 것
- self-descriptive messages (대부분의 REST API에서 지켜지지 못하고 있음)
 - 메시지는 스스로를 설명해야한다.
```
GET / HTTP/1.1
```
```
GET / HTTP/1.1
Host: www.example.org
```
```
HTTP1.1 200 OK
[ { "op": "remove", "path: "/a/b/c"}]
```
```
HTTP1.1 200 OK
Content-Type: application/json-patch+json

[ { "op": "remove", "path: "/a/b/c"}]

```
- hypermedia as the engine of application state(HATEOAS) (대부분의 REST API에서 지켜지지 못하고 있음)
 - 애플리케이션의 상태는 Hyperlink를 이용해 전이되어야한다.

왜 uniformal interface가 필요한가?
- 서버와 클라이언트가 각각 독릭접으로 진화한다.
- 독릭접진화: 서버의 기능이 변경되어도 클라이언트를 업데이트할 필요가 없다.
- 하지만, 독릭접진화를 달성하기위해 uniform interface가 만족해야한다.

REST가 지켜지고 있는 사례
- 웹
 - 웹사이트가 변경되었다고 해도, 웹 브라우저를 업데이트할 필요는 없다 vice versa
 - HTTP명세가 변경되어도, HTML명세가 변경되어도 웹은 잘 동작

웹이 단단한 이유 - 상호운용성(interoperability)에 대한 집착
- Referer 오타지만 안 고침
- charset 잘못 지은 이름이지만 안 고침
 - encoding이어야 하는듯? 하지만 그 당시 개발자들이 개념이 모호해서 지은듯?
- HTTP 상태코드 416 포기함
- HTTP/0.9 아직도 지원함 (크롬, 파이어폭스)
 - 크롬에서 0.9지원 안하려고 해봤지만, 결과적으로 몇몇 웹사이트의 proxy가 망가져서 지원을 다시 하게됨.

꼭 지켜야 하는가?
- If you think you have control over the system(서버-클라이언트 동시개발 또는 클라이언트를 마음대로 조종가능하거나) or aren't interested in evolvability(웹처럼 진화), don't waste your time arguing about REST.

Solution
1. REST API를 구현하고 REST API라고 부르는 것.
2. REST API 구현을 포기하고 HTTP API라고 부르는 것.
3. REST API가 아니지만 REST API라고 부르는 것. (현재 상태)

why self-descriptive and HATEOAS are neeeded?
- self-descriptive
 - 서버나 클라이언트가 변경되더라도 오고가는 메시지는 언제나 self-descriptive 하므로 언제나 해석이 가능하다.
- HATEOAS
 - 어디서 어디로 전이가 가능한지 미리 결정되지 않는다. 어떤 상태로 전이가 완료되고 나서야 그 다음 전이될 수 있는 상태가 결정된다.

정리
- 오늘날 대부분의 "REST API"는 사실 REST를 따르지 않고 있다.
- REST의 제약조건 중에서 특히 Self-descriptive와 HATEOAS를 잘 만족하지 못한다.
- REST는 긴 시간에 걸쳐(수십년) 진화하는 웹 애플리케이션을 위한 것이다.
- REST를 따를 것인지는 API를 설계하는 이들이 스스로 판단하여 결정해야한다.
- REST를 따르겠다면, Self-descriptive와 HATEOAS를 만족시켜야한다.
 - Self-descriptive는 custom media type이나 profile link relation 등으로 만족시킬 수 있다.
 - HATEOAS는 HTTP 헤더나 본문에 링크를 담아 만족시킬 수 있다.
- REST를 따르지 않겠다면, "REST를 만족하지 않는 REST API"를 뭐라고 부를지 결정해야 할 것이다.
 - HTTP API라고 부를 수도 있고
 - 그냥 이대로 REST API라고 부를 수도 있다.

참고
[resource][https://www.youtube.com/watch?v=RP_f5dMoHFc]

## REST API
- REST형식의 API
- 핵심 컨텐츠 및 기능을 외부 사이트에서 활용할 수 있도록 제공되는 인터페이스
-  클라이언트는 이러한 REST API들을 조합한 어플리케이션을 만들 수 있게 되었습니다
1. 첫 번째, URI는 정보의 자원을 표현해야 한다.
2. 두 번째, 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.