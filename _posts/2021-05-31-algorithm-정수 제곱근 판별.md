---
layout: post 
title:  "[Algorithm] 정수 제곱근 판별"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12934){:target="_blank"}

---

# 문제 설명

임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.


# 제한 사항

- n은 1이상, 50000000000000 이하인 양의 정수입니다.


# 입출력 예

| n    | return |
| ---- | :----: |
| 121  |  144   |
| 3    |   -1   |

# 입출력 예 설명

**입출력 예#1**

121은 양의 정수 11의 제곱이므로, (11+1)를 제곱한 144를 리턴합니다.

**입출력 예#2**

3은 양의 정수의 제곱이 아니므로, -1을 리턴합니다.

---

# 내가 푼 방식

```js
function solution(n) {
    const number = Math.sqrt(n) + 1
    return Number.isInteger(number) ? Math.pow(number, 2) : -1
}
```

1. number변수에 매개변수로 받은 n의 루트값을 `Math.sqrt()`를 사용해서 구하고 +1을 한 값을 할당한다.
2. 만약 number변수가 정수일 경우 `Math.pow()`를 사용해서 number의 제곱을 리턴하고, 아닐 경우 -1을 반환해준다.


# 다른 답안

```js
function solution(n) {
    // (1)
    var result = 0;
    var x = 0;

    while (x * x < n){ // (2)
        x++;
    }
    if (x * x == n){  // (3)
        x++;
        result = x * x; 
    }else{  // (4)
        result = -1;
    }

    return result;
}
```

1. 0의 값을 가진 result와 x변수를 생성한다.
2. `while()`을 사용해서 x의 제곱이 n보다 클 때까지 x++을 해준다.
3. x의 제곱이 n과 같을 경우, x++를 해주고 result에 x의 제곱을 할당해준다.
4. x의 제곱이 n과 같지 않을 경우 result에 -1을 할당해준다.