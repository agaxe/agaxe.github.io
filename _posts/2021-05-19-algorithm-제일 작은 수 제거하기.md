---
layout: post
title:  "[Algorithm] 제일 작은 수 제거하기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12935){:target="_blank"}

---

# 문제 설명

정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.


# 제한 조건

- arr은 길이 1 이상인 배열입니다.
- 인덱스 i, j에 대해 i ≠ j이면 arr[i] ≠ arr[j] 입니다.


# 입출력 예

| arr       | return  |
| --------- | ------- |
| [4,3,2,1] | [4,3,2] |
| [10]      | [-1]    |


---

# 내가 푼 방식

```js
function solution(arr) {
    return arr.length <= 1 ? [-1] : arr.filter(v => v !== Math.min(...arr));
}
```

- 매개변수로 받은 arr의 길이가 1 이하면 [-1]을, 아니면 `Math.min()`과 `전개 연산자(...)`를 사용해서 arr에서 제일 작은 값을 구하고 그 값을 `filter()`를 사용해서 제일 작은 값을 제외한 배열을 반환해준다.


# 다른 답안

```js
function solution(arr) {
    arr.splice(arr.indexOf(Math.min(...arr)), 1); // (1), (2)
    if(arr.length < 1) return [-1]; // (3)
    
    return arr;
}
```

1. `Math.min()`로 arr배열에서 제일 작은 수를 구하고, `indexOf()`를 사용해서 방금 구한 제일 작은수의 인덱스값을 구한다.
2. `splice()`의 첫 번째 인자에 제일 작은 수의 인덱스를 넣어서 제일 작은 수의 값을 빼준다.
3. 만약 arr의 길이가 1보다 작으면 [-1]를 반환해준다.

