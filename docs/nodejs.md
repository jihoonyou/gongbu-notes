# nodejs

## 공부순서
~~[nodeschool](https://nodeschool.io/ko/about.html)~~
[] [theNodeBeginnerBook](https://www.nodebeginner.org/index-kr.html)
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