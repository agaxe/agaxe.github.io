---
layout: post 
title:  "[Algorithm] 시저 암호"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12926){:target="_blank"}

---

# 문제 설명

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.


# 제한 조건

- 공백은 아무리 밀어도 공백입니다.
- s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
- s의 길이는 8000이하입니다.
- n은 1 이상, 25이하인 자연수입니다.


# 입출력 예

| s       | n    | result  |
| ------- | ---- | ------- |
| "AB"    | 1    | "BC"    |
| "z"     | 1    | "a"     |
| "a B z" | 4    | "e F d" |

---

# 답안

```js
function solution(s, n) {
    return [...s].map(v => { // (1)
        if(v === ' ') return v; // (2)
        return v.toUpperCase().charCodeAt() + n > 90 // (3)
        ? String.fromCharCode(v.charCodeAt() + n - 26) // (4)
        : String.fromCharCode(v.charCodeAt() + n)  // (5)
    }).join('') // (6)
}
```

1. 매개변수로 받은 문자열s를 배열로 만든 뒤 `map()`을 사용해준다.
2. 반복문에서 해당 항목이 공백일 경우 공백을 반환해준다.
3. 해당 항목을 대문자로 변경하고(`toUpperCase()`) 그 값의 ASCII 코드값(`charCodeAt()`) + n 값이 90보다 클 경우
    - 해당 항목이 "Z" 거나 "z"일 경우
4. 해당 항목의 ASCII 코드값에 n을 더하고 26을 빼준 값을 반환해주고
    - 26은 Z - A, z - a 값에 +1한 값임
5. 아닐 경우 해당 항목의 ASCII 코드값에 n을 더해준 값을 반환해준다.
6. `map()`이 완료된 뒤 배열을 문자열로 다시 변경해준다.

```js
// ex)  s= "z", n = 1

// (3) v.toUpperCase().charCodeAt() + n > 90 ===> 90 + 1 > 90
// (4) String.fromCharCode(v.charCodeAt() + n - 26) ===> String.fromCharCode(123 - 26)
```