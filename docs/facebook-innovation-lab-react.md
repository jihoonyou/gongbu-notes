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
