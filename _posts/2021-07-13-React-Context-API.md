---
layout: post
title:  "Context API"
categories: ['React']
---

# Context API
- 리액트에서 사용하는 데이터를 전역으로 관리할 수 있다.
- 부모 컴포넌트에서 자식 컴포넌트로 props를 계속해서 보내는 번거로움을 해결할 수 있다.

# 예제 파일 구성
- 예제는 codesandbox 에서 확인할 수 있다.

```markdown
- /src
  - App.js
  - parent.js
  - children.js
  - other.js
  - /context
    - index.js
```
[![Edit context api study](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/context-api-study-6h1dr?fontsize=14&hidenavigation=1&theme=dark){:target="_blank"}   

# React.createContext()
- context 객체를 생성한다.
- 인자값에는 기본값이 들어간다.

```js
const MyThemeContext = React.createContext('light');
```

# Context.Provider
- context 의 value 값을 설정할 수 있다.
- value 값에는 상태값 뿐만 아니라 함수도 전달할 수 있다.

```jsx
<MyThemeContext.Provider value='dark'>
  {/* 특정 컴포넌트 */}
</MyThemeContext>
```

# Context.Consumer
- context 변화를 구독하는 React 컴포넌트
- 컴포넌트 안에서 context 의 value 값을 활용하여 렌더링을 할 수 있다.

```jsx
<MyThemeContext.Consumer>
  {value => value === 'light' ? <p>기본 모드!<p> : <p>다크 모드!<p>}
</MyThemeContext.Consumer>
```

# Context.displayName
- context 의 displayName 문자열 속성을 설정할 수 있다.
- 개발자 도구에서 설정한 값을 확인할 수 있다.

```jsx
const MyThemeContext = React.createContext('light');
MyThemeContext.displayName = 'MyThemeDisplayName';

<MyThemeContext.Provider> // "MyThemeDisplayName.Provider" in DevTools
<MyThemeContext.Consumer> // "MyThemeDisplayName.Consumer" in DevTools
```

---

### 참고

[https://ko.reactjs.org/docs/context.html](https://ko.reactjs.org/docs/context.html){:target="_blank"}   
[https://velopert.com/3606](https://velopert.com/3606){:target="_blank"}   
[https://react.vlpt.us/basic/22-context-dispatch.html](https://react.vlpt.us/basic/22-context-dispatch.html){:target="_blank"}   