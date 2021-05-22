---
layout: post
title:  "[Algorithm] 내적"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/70128){:target="_blank"}

---

# 문제 설명

길이가 같은 두 1차원 정수 배열 a, b가 매개변수로 주어집니다. a와 b의 내적을 return 하도록 solution 함수를 완성해주세요.   

이때, a와 b의 내적은 `a[0]*b[0] + a[1]*b[1] + ... + a[n-1]*b[n-1]` 입니다. (n은 a, b의 길이)


# 제한사항

- a, b의 길이는 1 이상 1,000 이하입니다.
- a, b의 모든 수는 -1,000 이상 1,000 이하입니다.


# 입출력 예

| a           | b             | result |
| ----------- | ------------- | ------ |
| [1,2,3,4] | [-3,-1,0,2] | 3      |
| [-1,0,1]  | [1,0,-1]    | -2     |


# 입출력 예 설명

**입출력 예 #1**

- a와 b의 내적은 `1*(-3) + 2*(-1) + 3*0 + 4*2 = 3` 입니다.

**입출력 예 #2**

- a와 b의 내적은 `(-1)*1 + 0*0 + 1*(-1) = -2` 입니다.

---

# 내가 푼 방식

```js
function solution(a, b) {
    return a.reduce((acc,curr,i) => acc += curr * b[i],0)
}
```

- 매개변수로 받은 a배열에 `reduce()`를 사용해서 현재값과 매개변수 b배열의 해당 인덱스값을 곱한 뒤, acc에 더해 주었다.


# 다른 답안

```js
function solution(a, b) {
    var sum = 0;

    for(var i = 0; i < a.length; i++){
        sum += a[i] * b[i];
    }

    return sum;
}
```

- `for()`를 사용해서 a배열의 해당 인덱스와 b배열의 해당 인덱스를 곱한 값을 sum변수에 더해주었다.