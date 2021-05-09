---
layout: post
title:  "[Algorithm] 음양 더하기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/76501){:target="_blank"}

---

# 문제 설명

어떤 정수들이 있습니다. 이 정수들의 절댓값을 차례대로 담은 정수 배열 absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 signs가 매개변수로 주어집니다. 실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.


# 제한 사항

- absolutes의 길이는 1 이상 1,000 이하입니다.
  - absolutes의 모든 수는 각각 1 이상 1,000 이하입니다.
- signs의 길이는 absolutes의 길이와 같습니다.
  - `signs[i]` 가 참이면 `absolutes[i]` 의 실제 정수가 양수임을, 그렇지 않으면 음수임을 의미합니다.


# 입출력 예

| absolutes  | signs                | result |
| ---------- | -------------------- | ------ |
| [4,7,12] | [true,false,true]  | 9      |
| [1,2,3]  | [false,false,true] | 0      |

# 입출력 예 설명

**입출력 예 #1**

- signs가 `[true,false,true]` 이므로, 실제 수들의 값은 각각 4, -7, 12입니다.
- 따라서 세 수의 합인 9를 return 해야 합니다.

따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

**입출력 예 #2**

- signs가 `[false,false,true]` 이므로, 실제 수들의 값은 각각 -1, -2, 3입니다.
- 따라서 세 수의 합인 0을 return 해야 합니다.

---

# 내가 푼 방식

```js
function solution(answers) {
    const number = absolutes.map((v,i) => signs[i] ? v : -v); // (1)
    return number.reduce((acc,curr) => acc + curr, 0); // (2)
}
```

1. number변수에 `map()`을 사용해서 absolutes배열의 값에 부호를 추가한 값을 할당해준다.
2. 부호를 추가한 배열을 `reduce()`를 사용해서 총합을 구한다.

# 다른 답안

```js
   function solution(absolutes, signs) {
    return absolutes.reduce((acc, v, i) => acc += v * (signs[i] ? 1 : -1), 0)
}
```

- `reduce()`를 사용해서 signs배열의 현재 인덱스값이 true면 1, false면 -1인 값을 absolutes배열의 현재 값에 곱하고 총합에 더해준다.

