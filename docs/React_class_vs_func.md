# React class vs function

## 공부자료
[x] [생활코딩](https://www.youtube.com/playlist?list=PLuHgQVnccGMCEfBwnNGsJCQDiqSWI-edj)

## 과거(Hook 이전)
함수형 컴포넌트에서 state, life cycle API를 사용 할 수 없었음.

## class 
- required render()
- this.props

## function 
- just return
- first parameter takes props -> props.
- hook -> useState()
- useEffect -> 렌더가 실행되고 실행됨. == componentDidmount, componentDidUpdate