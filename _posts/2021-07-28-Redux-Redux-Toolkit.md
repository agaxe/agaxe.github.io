---
layout: post
title:  "Redux Toolkit"
categories: ['Redux']
---

# Redux Toolkit (RTK)

- 기존의 Redux 를 더욱 쉽고 간결하게 구현할 수 있는 Redux 공식 라이브러리
- Redux DevTools Extension 과 Redux middleware(thunk, logger), immer 등의 라이브러리가 기본으로 포함되어 있다.


## 주요 함수

### configureStore

- `createStore` 를 랩핑하여 기존의 `createStore` 역할을 한다.
- 해당 함수를 통해 Redux DevTools Extension 과 Redux middleware 를 설정할 수 있다.

```js
// Before
const store = createStore(counter)

// After
const store = configureStore({
  reducer: counter,
  //middleware: [thunk, logger]
})
```


### createAction

- 액션 타입 문자열을 인자로 받고, 해당 타입을 사용하는 액션 생성자함수를 반환한다.

```js
// Before
const INCREMENT = 'INCREMENT'

function incrementOriginal() {
  return { type: INCREMENT }
}
console.log(incrementOriginal()) // {type: "INCREMENT"}


// After
const incrementNew = createAction('INCREMENT')

console.log(incrementNew()) // {type: "INCREMENT"}
```


### createReducer

- 객체를 사용하여 reducer를 작성할 수 있는 함수 (Switch 문 사용 x)
- 내장되어 있는 immer 라이브러리를 통해 불변성을 유지할 필요가 없다.
- ES6 의 [computed 속성](https://ko.javascript.info/object#ref-715){:target="_blank"}을 사용하여 type문자열 변수로 키를 작성할 수 있다.
- 첫 번째 인자는 초깃값 객체(initialState), 두 번째 인자는 reducer 객체를 받는다.

```js
// Before
function counter(state = 0, action) {
  switch (action.type) {
    case INCREMENT:
      return state + 1
    case DECREMENT:
      return state - 1
    default:
      return state
  }
}
```
```js
// After
const increment = createAction('INCREMENT')
const decrement = createAction('DECREMENT')

const counter = createReducer(0, {
  [increment.type]: state => state + 1,
  [decrement]: state => state - 1 // [decrement] == [decrement.type]
})
```


### createSlice

- action과 reduder를 합쳐서 선언할 수 있는 함수

```js
const counterSlice = createSlice({
  name: 'counter',
  initialState: 0,
  reducers: {
    increment: state => state + 1,
    decrement: state => state - 1
  }
})
``` 
```js
const { actions, reducer } = counterSlice
const { increment, decrement } = actions
```

---

### 참고

[https://redux-toolkit.js.org/](https://redux-toolkit.js.org/){:target="_blank"}  
[https://soyoung210.github.io/redux-toolkit](https://soyoung210.github.io/redux-toolkit){:target="_blank"}   
