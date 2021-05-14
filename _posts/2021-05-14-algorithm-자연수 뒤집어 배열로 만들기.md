---
layout: post
title:  "[Algorithm] 자연수 뒤집어 배열로 만들기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12932){:target="_blank"}

---

# 문제 설명

자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.


# 제한 조건

- n은 10,000,000,000이하인 자연수입니다.


# 입출력 예

| n     | return      |
| ----- | ----------- |
| 12345 | [5,4,3,2,1] |

---

# 답안

```js
function solution(n) {
    return [...String(n)].reverse().map(v => Number(v));
}
```

1. 매개변수로 받은 자연수n을 문자열로 바꾼 뒤 비구조화 할당을 사용해서 배열로 만들어 준다
2. `reverse()`를 사용해서 배열 값의 순서를 반전시켜 준다.
3. 순서를 반전시킨 배열의 값들을 숫자형으로 변경해준다.