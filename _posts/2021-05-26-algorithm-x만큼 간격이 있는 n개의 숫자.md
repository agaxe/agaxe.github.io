---
layout: post 
title:  "[Algorithm] x만큼 간격이 있는 n개의 숫자"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12954){:target="_blank"}

---

# 문제 설명

함수 solution은 정수 x와 자연수 n을 입력 받아, x부터 시작해 x씩 증가하는 숫자를 n개 지니는 리스트를 리턴해야 합니다. 다음 제한 조건을 보고, 조건을 만족하는 함수, solution을 완성해주세요.


# 제한 사항

- x는 -10000000 이상, 10000000 이하인 정수입니다.
- n은 1000 이하인 자연수입니다.


# 입출력 예

| x    | n    | answer       |
| ---- | ---- | ------------ |
| 2    | 5    | [2,4,6,8,10] |
| 4    | 3    | [4,8,12]     |
| -4   | 2    | [-4, -8]     |

---

# 내가 푼 방식

```js
function solution(x, n) {
    let answer = [];
    
    for(let i = 0; i < n; i++){
        answer.push(x * (i + 1))
    }
    
    return answer
}
```

- `for()`를 사용해 반복문을 실행히고 n번동안 answer배열에 `x * (i + 1)` 값을 추가해준다.


# 다른 답안

```js
function solution(x, n) {
    return Array(n).fill(x).map((v, i) => v * (i + 1))
}
```

1. `Array()`로 n개의 길이를 가진 배열을 만들고 `fill()`로 배열의 모든 항목을 x로 변경해준다.
2. `map()`을 사용해서 `v * (i + 1)`의 값을 가진 배열을 반환해준다.