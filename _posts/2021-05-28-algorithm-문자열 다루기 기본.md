---
layout: post 
title:  "[Algorithm] 문자열 다루기 기본"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12918){:target="_blank"}

---

# 문제 설명

문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.


# 제한 사항

- `s`는 길이 1 이상, 길이 8 이하인 문자열입니다.


# 입출력 예

| s      | return |
| ------ | ------ |
| "a234" | false  |
| "1234" | true   |

---

# 내가 푼 방식

```js
function solution(s) {
    return s*1 && !/[a-z]/g.test(s) && (s.length === 4 || s.length === 6) ? true : false
}
```

- 문자열s를 숫자형으로 변환한 값이 true이고 (`s*1`)
- 문자열s에 영문자가 들어가 있지 않고 (`!/[a-z]/g.test(s)`)
- 문자열s의 길이가 4이거나 6인 경우 true, 아니면 false


# 다른 답안

```js
function solution(s) {
    var regex = /^\d{6}$|^\d{4}$/;
    return regex.test(s);
}
```

- 문자열s에 4자리의 숫자가 있거나 6자리의 숫자가 있는 경우 true, 아니면 false를 반환한다.
