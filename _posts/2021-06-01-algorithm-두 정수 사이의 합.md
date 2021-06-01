---
layout: post 
title:  "[Algorithm] 두 정수 사이의 합"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12912){:target="_blank"}

---

# 문제 설명

두 정수 a, b가 주어졌을 때 a와 b 사이에 속한 모든 정수의 합을 리턴하는 함수, solution을 완성하세요.   
예를 들어 a = 3, b = 5인 경우, 3 + 4 + 5 = 12이므로 12를 리턴합니다.


# 제한 조건

- a와 b가 같은 경우는 둘 중 아무 수나 리턴하세요.
- a와 b는 -10,000,000 이상 10,000,000 이하인 정수입니다.
- a와 b의 대소관계는 정해져있지 않습니다.


# 입출력 예

| a    | b    | return |
| ---- | ---- | ------ |
| 3    | 5    | 12     |
| 3    | 3    | 3      |
| 5    | 3    | 12     |


---

# 내가 푼 방식

```js
function solution(a, b) {
    let sum = 0; // (1)
    
    if(a < b){ // (2)
        for(let i = a; i <= b; i++){
            sum += i
        }
    }else if(a > b){ // (3)
       for(let i = b; i <= a; i++){
            sum += i
       } 
    }else{ // (4)
        sum = a;
    }
    
    return sum;
}
```

1. 합계를 담을 sum 변수를 선언해준다.
2. 만약 매개변수 b가 a보다 큰 경우, `for()`를 사용해서 a ~ b까지의 합계를 sum변수에 할당해준다.
3. 만약 매개변수 a가 b보다 큰 경우, `for()`를 사용해서 b ~ a까지의 합계를 sum변수에 할당해준다.
4. a와 b가 같을 경우, a를 sum변수에 할당해준다.


# 다른 답안

```js
function solution(a, b) {
    return (a + b) * (Math.abs(b - a) + 1) / 2;
}
```

- a와 b를 더한 값과 a와 b의 절대값에 1을 더한 값을 곱해준 뒤, 2로 나누어준다.

```js
// ex) a = 3, b = 7

/*
    (a + b)                 = 10
    (Math.abs(b - a) + 1)   = 5 (4+1)
    10 * 5 / 2              = 25
*/
```