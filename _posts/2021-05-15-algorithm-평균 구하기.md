---
layout: post
title:  "[Algorithm] 평균 구하기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12944){:target="_blank"}

---

# 문제 설명

정수를 담고 있는 배열 arr의 평균값을 return하는 함수, solution을 완성해보세요.


# 제한사항

- arr은 길이 1 이상, 100 이하인 배열입니다.
- arr의 원소는 -10,000 이상 10,000 이하인 정수입니다.


# 입출력 예

| arr       | return |
| --------- | :----: |
| [1,2,3,4] |  2.5   |
| [5,5]     |   5    |

---

# 답안

```js
function solution(arr) {
    return arr.reduce((acc,cur) => acc + cur, 0) / arr.length;
}
```

- 매개변수로 받은 arr배열에 `reduce()`를 사용해서 합계를 구한 뒤 arr의 길이만큼 나눠준다.