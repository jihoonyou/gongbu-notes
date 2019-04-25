# facebook-innovation-lab-react

## day 3 - 04/24/19

javascript this
- 자신을 포함하고 있는 객체

javascript window
- window 객체는 객체의 계층 구조에서 최상위에 존재하며 가장 기본적이면서도 중요한 객체
- 그래서 function을 그냥 define하면 this === window

전역공간에 적은 수의 함수와 변수가 있는게 좋음
- folder를 만드는 것처럼 객체로 안에 넣어서 사용하면 혼동이 없을듯. (c드라이브에 많은 directory가 있는 것)
- 변수의 이름에 해당 객체를 가르키는 this를 사용하지 않으면, window를 가르킨다

debugging
- preserve log를 눌러서 확인
- debugger
- breakpoint click해서 할 수 있음

javascript
- 웹을 위해서 태어난 컴퓨터 언어
- javscript를 사용하는 것에 대한 부끄러움이 있었음. (하지만, 이제는 바뀜) => 순수한 웹 기술로 만드는 것
- 구글에서 크롬의 성능을 좋게 하기 위해 parser를 만듦. 과거에는 웹브라우저만 제어했지만, Nodejs를 통해 컴퓨터를 제어

npm (package manager)
- nodejs의 앱 스토어 (nodejs로 만든 앱 스토어)
- npm install create-react-app => 프로젝트 내에 깔림
- npm install -g create-react-app => 컴퓨터 내에 깔림

react
- create-react-app my-app (directory name으로 react는 안됨)
- npm start => create-react-app을 통해서 생성된 server가 실행
- public안에 index.html 파일 수정
- index.html안에 <div id="root"></div>
- src/index.js
- from은 어느페이지에서 가져온 부품을 어떻게 사용하겠느냐.
- 처음 했을 때 화면이 이상한 이유는 default로 따라오는 css파일이 그대로 적용되어 있기 때문에
- JSX를 사용

props
- 예시 코드에서 Subject라는 component는 title, sub이라는 property를 갖고 있음.
- 해당 component(Subject)에서 {this.props.title}, {this.props.sub}로 가져옴.

state
- state에 값을 변경하면 state에 연관된 component에 대한 것들이 바뀐다.

기존에 headerTag(a,b) function에서 함수형으로 만든이유는 좀 더 dynamic하게 하려고.


## day 4 - 04/25/19

(초반부 놓침 self-study 필요)
npm run build??

npm install -g serve
youtube (react -9 배포하는 법 강의로 대체)

network 탭에서 Empty Cache and Hard reload
- cache를 지우고 다시 받게 하는 것
- 다운로드 용량 확인
- 1.7mb (리액트가 개발의 편의성을 위해 여러가지 기능을 추가해놨기 때문에..)
- create-react-app은 파일의 무게가 상당히 무거움 (local에서 개발 할 떄는 괜찮음)

npm run build
- production mode의 application을 만들 때(build할 때)
- 해당 command를 치면 build라는 directory가 생김
- build안의 index.html은 불필요한 공백을 없앤 것(용량이 훨씬 작음) src안의 다른 파일들도 용량을 줄이거나 보안적으로 좋지 않은 것, 에러메시지 등을 없앤다.
- **실제 서비스할 때는 빌드 안의 파일들을 사용해야 한다. 웹서버가 문서를 찾는 최상위 디렉토리에 이 build directory의 안쪽에 있는 파일들을 위치시킨다.
(실제로 서비스할 때는 build안에 있는 것을 파일을 쓰면 된다.)

npm serve
- npm install -g serve
- npm serve -s build (빌드라는 디렉토리를 document의 root로 하겠다)
- 결과 1.7mb가 125kb로 바뀜

props
- component를 조작하는 장치
- user와 component의 중계자
- component 바깥에서 조정
- 중첩된 component에서는, 부모 component가 자식 component에게 props를 넘김.
- 외부에서 조작하기 위해 사용 (button같은 것)

state
- component 내부에서 사용하는 데이터
- props값은 컴포넌트 안에서 마음대로 바꿀 수 없다. 그래서 내부적으로 state를 사용해 데이터를 조작.
- 내부에서 조작하기 위해 사용 (전선 같은 것)

**state나 props값이 바뀌면, react에서 render()를 다시 실행 => 새로 그려지는 효과
- var state같은 지역변수는 화면이 변환되는데 아무런 영향도 주지 않음.

event
- onClick={} (html에서는 onclick)
- 예제: a 가 클릭 됐을 때 해당 함수가 실행되길 바라는 것 => 약속으로 해당 함수의 첫번째 인자로 event객체가 들어온다!
- debugging tip: 화면이 reload되면 log 가 지워지므로 preserve log를 선택한다.
- this.state.mode = 'welcome'을 하면 안됨 (error발생!) 왜냐면 this가 undefined
- 해결책 해당 함수에 .bind(this)를 뒤에 붙여줌.

객체
- 안에 있는 것들 property
- 객체 안에 속해 있으면 method, 아니면 function
- Math는 내장된 객체, new Date는 새로운 객체를 만드는 것? (new Date는 객체를 만드는 공장)
- javscript에서 함수 호출할 때 new를 붙이면 객체를 만듦? (Java랑 다른 점 - java에서는 클래스로 객체 define해서 생성)
- 자바스크립트에서의 객체 지향은 함수로 이루어짐. new를 붙이면 객체, 아니면 함수. (new가 붙었을 때 생성자 함수 - constructor)
function a() {
    this.name = 'egoing'
}

class
- 분류, 그룹핑
- new 객체를 하면, constructor라는 것을 찾고 먼저 실행함.

prototype
- sum이라는게 없으면 prototype에서 찾기로 약속되어 있음.
- Person의 protytype property는 Person's prototype을 가리킴
- Person's prototype의  constructor property는 Person 을 가리킴

그럼 method는 prototype에 정의하는게 좋은건가?

__proto__
- 자신을 만드는 prototype을 가르킴
- 각각의 객체는 개개체의 프로토타입 객체를 __proto__를 통해 알 수 있음.

prototype에서는 없으면 p

최상위까지 가면 object의 __proto__로 가서 없으면 null값 리턴

constructor값이 같으면, 같은 공장 출신!

prototype을 통해 공유함수를 만드는듯

```
var p1 = {
            name: 'egoing',
            first:10,
            second:20,
            sum:function() {
                return this.first + this.second;
            }
        }
var p2 = {
            name: 'egoing',
            first:50,
            second:50,
            sum:function() {
                return this.first + this.second;
        }

function Person(_name, _first, _second) {
    this.name = _name;
    this.first = _first;
    this.second = _second;
    this.sum = function() {
        return this.first + this.second;
    }
}
function Person(_name, _first, _second) {
    this.name = _name;
    this.first = _first;
    this.second = _second;

}
    Person.prototype.sum = function() {
        return this.first + this.second;
    }

class Person {
    constructor(_name, _first, _second) {
        this.name = _name;
        this.first = _first;
        this.second = _second;
        this.sum = function() {
            return this.first + this.second;
        }
    }
}

```

node __.js 커멘드를 통해 웹을 벗어나 javascript를 실행할 수 있음.

bind
- javascript는 좀 더 유연해서, 


```
kim = {name: 'kim'};
lee = {name: 'Lee'};
function hi() {
    console.log('hi, ' + this.name);
}
hi.call(kim);
hi.call(lee);
```
- 여기서 this는 global 객체
- hi라는 함수를 실행할 때 this를 누구로 할지 정할 수 있음
call vs bind
- call은 호출, bind는 엮어주는 것
- bind는 call하지 않고, 연결만.
- bind는 hi를 복제하고(내부적으로 건들지 않게 하기 위해), hi가 가르키는 this를 kim으로
- 원래 hi는 건들지 않고, hi를 복제를 해서 그 함수를 리턴. (immutable)

```
            function(_event) {
              // this.state.mode = 'welcome';
              console.log(this);
              this.setState({mode: 'welcome'});
              _event.preventDefault();
            }.bind(this)
```
- 여기서 bind가 없으면 this는 undefined, 하지만 bind(this)를 하면 함수를 생성한 객체.
- onClick같은 event를 작성할 때 .bind(this)를 한다

this.setState
- why use setState? 이렇게 해야함
- 이렇게 하지 않으면, react가 알지 못함 그래서 render()가 호출되지 않고 
