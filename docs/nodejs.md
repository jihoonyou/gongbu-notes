# nodejs

## 공부순서
~~[nodeschool](https://nodeschool.io/ko/about.html)~~
[x] [theNodeBeginnerBook](https://www.nodebeginner.org/index-kr.html)
[x] [인프런 nodejs](https://www.inflearn.com/course/node-js-%EC%9B%B9%EA%B0%9C%EB%B0%9C#description)
[] [생활코딩](https://opentutorials.org/course/3332)
[] [커리큘럼확인하여 부족한 거 찾기](https://www.fastcampus.co.kr/dev_camp_nodejs/)

## The Node Beginner Book
첫 번째 JavaScript의 구현체는 브라우저안에 살았습니다.
Node.js는 실제로 단지 다른 환경일 뿐입니다. Node.js는 브라우저 밖, 백앤드에서 JavaScript를 실행할 수 있게 해줍니다.
- 백앤드에서 당신이 지정한 JavaScript를 수행하기 위해서는, 잘 해석되고 실행되어야 합니다. Node.js가 하는 것이 바로 그 일입니다.
- 그 일은 구글 크롬 브라우저가 사용하는 JavaScript 실행환경과 동일한, 구글의 V8 가상머신을 사용해 이루어집니다.

use case
- 사용자는 웹 브라우저로 우리의 웹 애플리케이션을 이용할 수 있다.
- 사용자가 http://domain/start를 요청하면 파일 업로드 폼이 들어있는 웰컴페이지를 볼 수 있어야 한다.
- 업로드할 이미지 파일을 선택해서 폼으로 전송하면, 해당 이미지는 http://domain/upload로 업로드 되어야 하며, 업로드가 끝나면 해당 페이지에 표시된다.

Application stack
- 우리는 웹페이지를 제공해야 한다. 따라서 HTTP 서버가 필요하다.
- 우리는 서버는 어떤 URL 요청(request)을 받았는지에 따라 다르게 응답해야 한다. 따라서, 요청과 요청을 처리할 핸들러들을 연결짓기 위한 라우터(router) 같은 것이 필요하다.
- 서버로 도착한 요청들, 그리고 라우터를 이용해서 라우팅된 요청들을 만족시키기 위해서 실제적인 요청 핸들러(request handlers)가 필요하다.
- 라우터는 아마도 들어오는 어떠한 POST 데이터들도 다룰 수 있어야 한다. 그리고 해당 데이터를 다루기 편한 형태로 만들어 request handler 들에게 넘겨야 한다. 따라서 요청 데이터 핸들링(request data handling)이 필요하다.
- URL에 대한 요청을 다루는 것뿐 아니라 URL이 요청되었을 때 내용을 표시할 필요도 있다. 이 말은 즉, request handler 들이 사용자 브라우저로 콘텐트를 보내기 위해 사용할 수 있는 뷰 로직(view logic)이 필요하다는 이야기다.
- 마지막이지만 중요한 것으로는, 사용자가 이미지들을 업로드 할 수 있어야 하니까, 세부 사항을 다루는 업로드 핸들링(upload handling)이 필요할 것이다.

http server구축
```
var http = require("http");

http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.write("Hello World");
  response.end();
}).listen(8888);
```
- nodejs에 기본으로 포함된 http 모듈을 읽어 들인 다음, http라는 이름의 변수를 통해 접근을 할 수 있게 만든다.

```
var http = require("http");

var server = http.createServer();
server.listen(8888);
```
- 8888 port를 listen하는 서버
- createServer의 첫 번째 파라미터에 함수를 정의할 수 있음.

Node.js는 event driven(event driven callback)이다.
- 서버를 생성할 때 서버 생성 메소드의 파라미터로 함수를 넘깁니다. 요청이 올 때마다 파라미터로 넘긴 함수가 호출됩니다.
- 요청이 언제 발생할 지는 모르지만 이제 들어오는 요청을 처리할 곳 생겼습니다. 파라미터로 넘긴 함수입니다. 함수를 먼저 정의한 후 넘겼든 anonymous function으로 넘겼든 말이죠.
- 이 개념을 callback 이라고 합니다. 우리는 메소드에 함수를 넘기고, 메소드는 관련된 이벤트가 발생하면 이 함수를 거꾸로 호출(call back) 합니다.

onRequest 함수가 호출될 때 두 개의 파라미터가 넘어온다 request, response. 객체임.

모듈화를 통해 server.js를 nodejs의 모듈로 만들어서 index.js main파일에서 사용하기 가능.
var http = require("http");
- Node.js 내부 어딘가에 "http"라는 모듈이 있으며, 이를 require하고 지역변수에 할당하여 사용하는 것!
- 이렇게 하면 지역변수가 http 모듈이 제공하는 모든 public 메소드를 사용할 수 있는 객체가 됩니다.

routing - 다른 HTTP 요청이 코드의 다른 부분을 가리키도록 하는 것

```
function route(pathname) {
  console.log("About to route a request for " + pathname);
}

exports.route = route;
```
- router.js 모듈화

```
var http = require("http");
var url = require("url");

function start(route) {
  function onRequest(request, response) {
    var pathname = url.parse(request.url).pathname;
    console.log("Request for " + pathname + " received.");

    route(pathname);

    response.writeHead(200, {"Content-Type": "text/plain"});
    response.write("Hello World");
    response.end();
  }

  http.createServer(onRequest).listen(8888);
  console.log("Server has started.");
}

exports.start = start;
```
- router 함수를 파라미터로 넘길 수 있도록 server의 start() 함수를 확장

```
var server = require("./server");
var router = require("./router");

server.start(router.route);
```
- index.js를 확장합니다. 여기서 router 함수를 server로 주사(inject) 합니다. [depenecy injection](https://martinfowler.com/articles/injection.html)

blocking vs non-blocking
blocking
- node에서는 모든 게 병렬로 수행된다. 당신 code만 빼고.
Node.js는 다수의 동시작업을 처리할 수 있지만 thread를 나누는 방식으로 하지 않습니다. 사실 Node.js는 단일 thread입니다.
- 대신, Node.js는 동시작업을 event loop을 실행해서 처리하며 개발자들은 이것을 사용할 수 있습니다. 우리는 blocking 동작을 피하고 non-blocking 동작을 사용해야만 합니다.
- callback 합수를 다른 함수에게 넘겨야 합니다.

"child_process" 모듈을 사용하여 함.
- exec() 커멘드를 통해 shell커멘드를 Node.js안에서 실행
- 책의 예제에서의 exec()을 비동기적으로 처리하기 위해서는 exec()의 두번째 파라미터의 callback 함수를 사용해야한다.

하나의 해결책
- 현재 우리 애플리케이션은 사용자에게 보여주고 싶은 content를 request handler에서 HTTP server로 전달할 수 있습니다. 다음과 같은 여러 애플리케이션 레이어들을 거쳐 넘기는 식으로 식으로 말입니다. (request handler -> router -> server)
- 새로운 접근 방법은 다음과 같습니다: content를 server로 보내는 대신 server를 content로 보낼겁니다. 좀 더 자세히 이야기 하면, response 객체 (server의 callback 함수인 onRequest() 에서 얻은)를 router를 통해 request handler에게 주사(inject) 합니다. 이제 handler는 이 객체가 가진 함수들을 이용해서 스스로 요청에 응답할 수 있게 되었습니다.

## Node.js 웹개발로 알아보는 백엔드 자바스크립트의 이해
JavaScript를 통한 풀스텍 개발

npm init
- package.json이 생김

비동기로 동작하는 콜백함수.

nodemon을 사용하여 편하게.
- 변화에 자동으로 적용됨.

__dirname
- 최상위 루트를 나타냄 (노드에서 제공해주는 식별자)

var app = express()

```
app.get('/', function(req,res) {
  res.send("<h1>hello</h1>")
});
```

```
app.use(express.static('public'))
```
static file처리 (public에 static한 파일이 있을 경우)

post방식
- 보통 서버에 데이터를 보낼 때 사용.
- get방식은 url에 보내는 데이터가 url에 담김


app.use(bodyParser.json())
app.use(bodyParser.urlencoded({extended: true}))
- express 서버에 바디파서를 쓴다고 알려줘야 함.
- client와 server사이의 데이터를 보낼 때 인코딩이 필요.

var bodyParser = require('body-parser')
- post의 경우 body-parser를 통해서 받을 수 있음.

```

app.post('/email_post', function(req,res) {
  //get : req.param('email)
  console.log(req.body.email)
  res.send("<h1>welcome " + req.body.email + "</h1>")
})
```
routing을 모듈화 하여 app.js를 좀 더 가볍게 만들 수 있음.

query문 날릴 때, set사용해서 좀 더 깔끔하게 코드를 넘길 수 있음.

session
- 사용자가 로그인을 했을 때 서버에서 로그인정보를 메모리/DB에 어떤 ID값을 만들어서 저장하는 것
- 로그인했다는 상태값을 저장하여, 로그인 유무에 따라 다른 정보를 보여줌.
- 최근에는 상태값을 저장하지 않는 token값으로 로그인관리를 하기도 함

npm install passport passport-local express-session connect-flash --save-dev
- passport 인증관련 모듈 처리
- passport-local 페이스북, 구글 로그인 말고 일반적인 로그인 처리 (local db에 관리)
- express-session 세션관리 처리
- connect-flash 에러 메시지를 redirect해서 관리하는 것

passport.js 사이트를 참고하여, 필요한거 공부 (middleware)

로그인 구현시
- custom callback을 사용해야하는듯