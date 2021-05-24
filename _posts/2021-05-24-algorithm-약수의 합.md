---
layout: post
title:  "[Algorithm] 약수의 합"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12928){:target="_blank"}

---

# 문제 설명

정수 n을 입력받아 n의 약수를 모두 더한 값을 리턴하는 함수, solution을 완성해주세요. 

# 제한 사항

- `n`은 0 이상 3000이하인 정수입니다.


# 입출력 예

| n    | return |
| ---- | ------ |
| 12   | 28     |
| 5    | 6      |


# 입출력 예 설명

**입출력 예 #1**

- 12의 약수는 1, 2, 3, 4, 6, 12입니다. 이를 모두 더하면 28입니다.

**입출력 예 #2**

- 5의 약수는 1, 5입니다. 이를 모두 더하면 6입니다.

---

# 내가 푼 방식

```js
function solution(n) { 
    return [...Array(n)]
        .map((v, i) => i + 1)
        .reduce((acc, curr) => n % curr === 0 ? acc + curr : acc, 0)
}
```

1. `map()`을 사용해서 [0 ~ n]의 값을 가진 배열을 만들고
2. `reduce()`를 사용해서 n을 curr로 나눈 나머지 값이 0이면 합계에 현재값을 더해주며 반복문을 실행한다. 


# 다른 답안

```js
function solution(n) {
    let sum = 0; // (1)

    // (2)
    for (let i = 1; i <= n; i++) {
        if (n % i === 0) sum += i;
    }

    return sum
}
```

1. 합계를 나타내는 변수 sum을 선언해준다.
2. 매개변수 n만큼 `for()`반복문을 실행해주고, n을 i로 나눈 나머지값이 0이면 sum에 i를 더해준다.