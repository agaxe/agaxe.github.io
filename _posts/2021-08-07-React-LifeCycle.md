---
layout: post
title:  "LifeCycle"
categories: ['React']
---

# LifeCycle

- 리액트 컴포넌트가 **마운트**, **업데이트**, **언마운트** 될 때의 과정
- 특정 과정이 발생할 때 호출되는 메서드를 LifeCycle Method 라고 한다.
- 공식 문서에 있는 [도표](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/){:target="_blank"}를 보면 한눈에 확인 할 수 있다.

## 마운트

- **constructor**
- **getDerivedStateFromProps**
- **render**
- **componentDidMount**
 
### constructor
- 컴포넌트의 생성자
- 컴포넌트가 만들어지면 가장 먼저 실행된다.
- constructor 안에 setState 를 호출하면 안 된다.

```js
constructor(props){
  super(props);
  console.log('constructor') 

  console.log(props) // {name: "sw"}
  this.state = { count: 0, name : '[기본 name값]' };
}
```

### getDerivedStateFromProps
- props 로 받은 값을 state 에 추가하는 경우 사용
- static 키워드를 사용하여 호출
- return 을 통해 state 에 추가

```js
  static getDerivedStateFromProps(props, state) {
    console.log("getDerivedStateFromProps");
    console.log(props, state); // {name: "sw"}, {count: 0, name: "[기본 name값]"}

    if(props.name !== state.name){
      return { name: props.name }; // (*)
    }
    return null; // 아무 일도 일어나지 않음
  }

  // (*) 다음에 실행되는 render 메서드에서 값이 변경된 것을 확인할 수 있다. 
  // {name: "sw"}, {count: 0, name: "sw"}
```

### render 
- 컴포넌트를 렌더링하는 메서드 
- 클래스 컴포넌트에서 반드시 구현되어야 한다.

```jsx
render(){
  console.log("render");
  console.log(this.props, this.state) // {name: "sw"}, {count: 0, name: "sw"}

  return(
    <div>안녕?</div>
  )
}
```

### componentDidMount
- 컴포넌트의 첫 번째 렌더링이 완료되었을 때 실행 (한 번만 실행됨)
- 주로 DOM 을 참조하는 작업이나 비동기 통신(ajax, fetch, axios)을 하는 경우 사용한다.

```js
componentDidMount(){
  console.log("componentDidMount");
}
```

## 업데이트

- getDerivedStateFromProps
- **shouldComponentUpdate**
- render
- **getSnapshotBeforeUpdate**
- **componentDidUpdate**

### shouldComponentUpdate
- return 값이 true 인 경우에만 리렌더링이 진행된다.
- 주로 최적화를 하는 경우 사용된다.

```js
shouldComponentUpdate(nextProps, nextState){
  console.log("shouldComponentUpdate");
  console.log(nextProps, nextState); // count를 +1 한 경우 => {name: "sw"}, {count: 1, name: "sw"}
  
  return nextState.count <= 10; // count 값이 10 이하인 경우에만 render(), componentDidUpdate() 이 실행됨
}
```

### getSnapshotBeforeUpdate
- return 값이 `componentDidUpdate()`의 3번째 인자로 전달된다.

```js
getSnapshotBeforeUpdate(prevProps, prevState) {
  console.log("getSnapshotBeforeUpdate");

  if(prevState.count >= 5){ // count 값이 6 이상이 되면 '스냅샷!' 을 반환한다.
    return "스냅샷!";
  }
  return null;
}
```

### componentDidUpdate
- 리렌더링이 된 뒤에 마지막으로 호출되는 메서드
- 3번째 인자로 `getSnapshotBeforeUpdate()`에서 return 된 값을 받는다.

```js
  componentDidUpdate(prevProps, prevState, snapshot) {
    console.log("componentDidUpdate");

    console.log(prevProps, prevState, snapshot);
    // count 값이 5 이하인 경우 => {name: "sw"}, {count: 0~4, name: "sw"}, undefined
    // count 값이 6 이상인 경우 => {name: "sw"}, {count: 5~n, name: "sw"}, "스냅샷!" 
  }
```

## 언마운트

- componentWillUnmount

### componentWillUnmount
- 컴포넌트가 제거되기 전에 호출된다.

```js
componentWillUnmount() {
  console.log("componentWillUnmount");
}
```

## +오류 처리

### getDerivedStateFromError
- 하위의 자식 컴포넌트에 에러가 발생한 경우 호출된다.
- static 키워드를 사용하여 호출

```js
static getDerivedStateFromError(error) {
  console.log("componentWillUnmount");
  console.error(error);

  return { hasError: true };
}
```

### componentDidCatch(error, info)
- 자식 컴포넌트에서 오류가 발생했을 때 호출
- '커밋' 단계에서 호출된다.

```js
componentDidCatch(error, info) {
  console.error("componentDidCatch");

  console.log('error',error)
  console.log('info',info)
}
```

---

### 참고

[https://ko.reactjs.org/docs/react-component.html](https://ko.reactjs.org/docs/react-component.html){:target="_blank"}   
[https://react.vlpt.us/basic/25-lifecycle.html](https://react.vlpt.us/basic/25-lifecycle.html){:target="_blank"}   