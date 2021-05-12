---
layout: post
title:  "[Algorithm] 자릿수 더하기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12931){:target="_blank"}

---

# 문제 설명

자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.   
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.


# 제한 사항

- N의 범위 : 100,000,000 이하의 자연수


# 입출력 예

| N    | answer |
| ---- | ------ |
| 123  | 6      |
| 987  | 24     |

# 입출력 예 설명

**입출력 예 #1**

문제의 예시와 같습니다.

**입출력 예 #2**

9 + 8 + 7 = 24이므로 24를 return 하면 됩니다.

---

# 내가 푼 방식

```js
function solution(n){
    let sum = 0; // 총합

    // (1)
    const number = n.toString();

    // (2)
    for(let i = 0; i < number.length; i++){
        sum += Number(number[i]) // (3)
    }
    return sum;
}
```

1. 매개변수로 받은 자연수 n을 문자형으로 타입 변환을 해준다.
2. 변환한 문자열의 길이만큼 `for`반복문을 실행한다.
3. 변환한 문자열의 해당 인덱스값을 숫자형으로 변경 후 sum값에 더해준다.


# 다른 답안

```js
function solution(n){
    return (n+"").split("").reduce((acc, curr) => acc + parseInt(curr), 0)
    // return [...(n + "")].reduce((a, b) => a + b * 1, 0)
}
```

1. 매개변수로 받은 자연수 n을 암묵적으로 숫자형에서 문자열로 타입을 변환한다.
2. 문자열로 변환한 값을 `split()`를 사용해서 각각의 항목들을 담은 배열을 변환한다.
3. 각각의 항목들을 담은 배열을 `reduce()`를 사용해서 합계를 반환한다. 