---
layout: post
title:  "[styled components] 추가 style 적용 이슈"
categories: ['Debugging','React']
---

# 상황

기존의 컴포넌트를 가져온 다음, 추가적인 스타일을 적용하는 작업을 진행하던 중 스타일 적용이 되지 않는 이슈가 발생하였다.


# 해결

가져오려는 컴포넌트의 props 에 className 을 추가해주어야 한다.


```jsx
// atoms/Button.tsx (기존 컴포넌트)
function ButtonComp ({ className }){ 
  return (
    <button
      className={className} // className 적용 !
    >
    버튼
    </button>
  )
}


// Login.tsx (style 을 추가하려는 컴포넌트) 
import styled from 'styled-components';
import Button from 'atoms/button'

...

const LoginButton = styled(Button)`
  border: 1px solid #f00;
`
```

---

### 참고

[https://styled-components.com/docs/basics#styling-any-component](https://styled-components.com/docs/basics#styling-any-component){:target="_blank"}   
[https://stackoverflow.com/a/52542937](https://stackoverflow.com/a/52542937){:target="_blank"}   