# React class vs function

## 공부자료
- [x] [생활코딩](https://www.youtube.com/playlist?list=PLuHgQVnccGMCEfBwnNGsJCQDiqSWI-edj)

## 과거(Hook 이전)
- 함수형 컴포넌트에서 state, life cycle API를 사용 할 수 없었음.
- hook의 도입으로 life cyle API, State 가능

## class 
1. required render()
2. 외부의 데이터를 this.props로 받음
3. state에 넣고 setState로

## function 
1. just return 자체가 render임
2. 첫번째 파라미터의 인자값으로 props를 받음 (props는 다르게 이름을 가져가도 됨)
3. useState로 state관리 가능
    - 배열이 return되고, 두개의 값으로 이루어짐
    - [0]은 state값, [1]은 state값을 바꾸는 함수

- useEffect -> 렌더가 실행되고 실행됨. == componentDidmount, componentDidUpdate

## React Lifecyle (class)
- componentWillMount() -> render() -> componentDidMount()
- state가 바뀌었을 떄
    - shouldComponentUpdate() - 변화감지. true시 하위작업 실행
    - componentWillUpdate()
    - render()
    - componenetDidUpdate()
- 컴포넌트 소멸될 떄 뒷처리
    - componentWillUnMount()

## React Lifecyle (function)
- useEffect를 사용
- useEffect 처음 render시행될떄 시행되고, render실행시마다 실행됨 (componentDidMount componenetDidUpdate)
    - useEffect는 여러개를 생성해서 사용할 수 있음
- userEffect의 return으로 componentWillUnMount구현
    - return이 userEffect전에 먼저 실행됨
- componenetDidUpdate를 hook에서
    - userEffect(func, [변수])
        - 변환 변수(값)에 대한 것만 처리가능하게
- componentDidMouunt 한번만실행되게
    - 두번째 인자에 빈 객체를 넣어서
    - []