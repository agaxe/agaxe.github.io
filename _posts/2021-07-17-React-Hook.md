---
layout: post
title:  "Hook"
categories: ['React']
---

# Hook

- 클래스 컴포넌트에서의 LifeCycle 과 상태관리를 함수형 컴포넌트에서 쉽고 간편하게 사용할 수 있는 함수
- Hooks 는 React 16.8 버전부터 지원한다.


# 특징

# 일반 Hook

## useState
- 컴포넌트의 상태관리 시 사용된다.
```js
const [state, setState] = useState(initialState);
```
- 최초 렌더링 시 `state` 와 initialState 는 값이 같다.
- `setState()` 로 상태값(`state`)을 변경할 수 있다.
- 상태값이 변경되면 컴포넌트의 리렌더링이 진행된다.

## useEffect
- 컴포넌트가 렌더링이 될 때마다 특정 작업을 할 경우 사용한다.

```js
useEffect(didUpdate);
```

- 클래스 컴포넌트의 componentDidMount 와 componentDidUpdate 를 합친 거랑 비슷하다.

```js
// componentDidMount
useEffect(() => {
    console.log('첫 렌더링!')
},[])

// componentDidUpdate
useEffect(() => {
    console.log('state 값이 변경될 때마다 실행!')
},[state])
```

- 컴포넌트가 언마운트되거나 업데이트 되기 직전에 어떠한 작업을 하고 싶은 경우 clean-up(정리) 함수를 넣어준다.
- 정리 함수는 주로 메모리 누수 방지 시 사용된다.

```js
// 업데이트 & 언마운트
useEffect(() => {
    console.log('mount!')

    // clearn up
    return() => { 
        console.log('unmount!')
    }
})

// 언마운트 일 경우에만
useEffect(() => {
    console.log('mount!')

    // clearn up
    return() => { 
        console.log('unmount!')
    }
},[]) // 두번째 인자에 빈 배열값 추가
```

## useContext

- 함수형 컴포넌트에서 Context 를 사용하는 경우 사용된다.
- Context 를 사용하여 상태값을 전역으로 사용할 수 있다.

# 추가 Hook

## useReducer

```js
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

- 컴포넌트 외부에서 상태 관리를 하는 경우 사용한다.
- useState 의 대체 함수

```jsx
const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

// component
function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```

- `initialState` 와 `reducer()` 를 외부 파일로 분리해서 사용할 수도 있다.

## useMemo
- 메모이제이션된 <mark>값</mark>을 반환한다.
- 성능을 최적화할 때 사용한다.
- 함수의 리턴값을 기억하여 특정 값이 변경되었을 경우에만 재연산을 한다.  
```js
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```
- 첫 번째 인수에는 함수, 두 번째 인수에는 (의존성)배열을 넣어준다.
- 두 번째 인수에 넣어준 배열의 값이 바뀌는 경우에만 첫 번째 인수의 함수가 실행된다.

## useCallback
- 메모이제이션된 <mark>콜백(함수)</mark>을 반환한다.
- 컴포넌트가 리렌더링되면 컴포넌트 안에 있는 함수가 새로 생성되어 성능에 좋지 않기 때문에 이를 최적화하기 위해 사용한다.
- 주로 렌더링이 자주 발생하는 컴포넌트의 최적화를 위해 사용한다.

```js
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```
- 첫 번째 인수에는 함수, 두 번째 인수에는 (의존성)배열을 넣어준다.
- 두 번째 인수에 넣어준 배열의 값이 바뀌는 경우에만 첫 번째 인수의 함수가 새로 생성된다.


## useRef
```js
const refContainer = useRef(initialValue);
```
- 컴포넌트의 HTML Element 에 접근하는 경우 사용한다.

```jsx
function TextInputWithFocusButton() {
    const inputEl = useRef(null);

    const onButtonClick = () => {
    // current 는 ref 값이 inputEl 인 element 를 가리킨다.
    inputEl.current.focus();
    };

    return (
    <>
        <input ref={inputEl} type="text" />
        <button onClick={onButtonClick}>Focus the input</button>
    </>
    );
}
```
- 컴포넌트의 로컬변수를 사용해야 하는 경우 사용한다.
- ref 안의 값이 변경되어도 렌더링이 되지 않는다.

```jsx
import React, { useRef } from 'react';

const RefSample = () => {
    const id = useRef(1);

    const setId = (n) => {
        id.current = n;
    }

    const printId = () => {
        console.log(id.current);
    }
    
    return (
        <div>refsample</div>
    );
};

export default RefSample;
```


## useImperativeHandle
- 부모 컴포넌트에서 자식 컴포넌트의 메서드 또는 ref 에 접근할 경우 사용한다.

```js
useImperativeHandle(ref, createHandle, [deps])
```
```jsx
// children
import React, { useRef, forwardRef, useImperativeHandle } from "react";

function FancyInput(props, ref) {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    }
  }));

  return <input ref={inputRef} />;
}

export default forwardRef(FancyInput);
```

```jsx
// parent
import React, { useRef } from "react";
import FancyInput from "./fancyInput";

function ParentComp(props, ref) {
  const FancyInputRef = useRef();

  const handleClick = () => {
    if (FancyInputRef.current) {
      FancyInputRef.current.focus();
    }
  };

  return (
    <div>
      <FancyInput ref={FancyInputRef} />
      <button onClick={handleClick}>버튼</button>
    </div>
  );
}

export default ParentComp;

```



## useLayoutEffect
- 레이아웃 배치(element) 가 진행되기 전에 상태값을 설정하는 경우 사용한다.
- 새로고침 시 상태값이 변경되어 깜빡거리는(?) 이슈를 해결할 수 있다. 
- `useEffect()` 와 형태가 같다.

```js
useLayoutEffect(() => {
  effect
  return () => {
    cleanup
  };
}, [input])


// ex
const [name, setName] = useState("");
const [age, setAge] = useState(0);

useLayoutEffect(() => {
    setAge(25);
    setName("sw");
}, []);
```

## useDebugValue
- React 개발자도구에서 사용자 Hook 레이블을 표시하는 데에 사용한다.

```js
function useFriendStatus(friendID) {
  const [isOnline, setIsOnline] = useState(null);

  useDebugValue(isOnline ? 'Online' : 'Offline');

  return isOnline;
}
```

## +Custom Hook
- 각각 다른 컴포넌트에서 자주 사용되는 로직을 hook 으로 만들어서 사용할 수 있다.

```js
// useInputs
import { useState, useCallback } from 'react';

function useInputs(initialForm) {
  const [form, setForm] = useState(initialForm);
  
  const onChange = useCallback(e => {
    const { name, value } = e.target;
    setForm(form => ({ ...form, [name]: value }));
  }, []);

  const reset = useCallback(() => setForm(initialForm), [initialForm]);

  return [form, onChange, reset];
}

export default useInputs;
```

- input 을 입력할 때 상태값을 변경해주는 useInput 이다.


---

### 참고

[https://ko.reactjs.org/docs/hooks-intro.html](https://ko.reactjs.org/docs/hooks-intro.html){:target="_blank"}   
[https://velog.io/@velopert/react-hooks](https://velog.io/@velopert/react-hooks){:target="_blank"}   