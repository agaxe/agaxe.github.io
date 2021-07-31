---
layout: post
title:  "Guard Clause"
categories: ['etc','Javascript']
---

# Guard Clause
- if...else 의 중첩으로 인해 가독성과 유지보수가 어려워지는 단점을 보완하는 것
- 보통 예외 처리를 먼저 한다.

```js
// ex) 로그인 시 아이디와 비밀번호의 길이를 체크하는 경우


// if...else 
function loginValidation(info){
  if(info.id.length > 3){
    if(info.pw.length > 8){
      console.log('로그인!', info)
      return true;
    }else{
      return false;
    }
  }else{
    return false;
  }
}


// Guard Clause
function loginValidation(info){
  if(info.id.length < 3) return false;
  if(info.pw.length < 8) return false;

  console.log('로그인!', info)
  return true;
}
```

- 이런 식으로도 가능하다.

```js
function isIdValidation(info){
  return (info.id.length > 3)
}

function isPwValidation(info){
  return (info.pw.length > 8)
}
```

---

### 참고

[https://learningactors.com/javascript-guard-clauses-how-you-can-refactor-conditional-logic/](https://learningactors.com/javascript-guard-clauses-how-you-can-refactor-conditional-logic/){:target="_blank"}     
