---
layout: post
title:  "[Algorithm] 두 개 뽑아서 더하기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/68644){:target="_blank"}

---

# 문제 설명

정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

# 제한사항

- numbers의 길이는 2 이상 100 이하입니다.
  - numbers의 모든 수는 0 이상 100 이하입니다.

# 입출력 예

| numbers       | result          |
| ------------- | --------------- |
| [2,1,3,4,1] | [2,3,4,5,6,7] |
| [5,0,2,7]   | [2,5,7,9,12]  |


# 입출력 예 설명

**입출력 예 #1**

- 2 = 1 + 1 입니다. (1이 numbers에 두 개 있습니다.)
- 3 = 2 + 1 입니다.
- 4 = 1 + 3 입니다.
- 5 = 1 + 4 = 2 + 3 입니다.
- 6 = 2 + 4 입니다.
- 7 = 3 + 4 입니다.
- 따라서 `[2,3,4,5,6,7]` 을 return 해야 합니다.

**입출력 예 #2**

- 2 = 0 + 2 입니다.
- 5 = 5 + 0 입니다.
- 7 = 0 + 7 = 5 + 2 입니다.
- 9 = 2 + 7 입니다.
- 12 = 5 + 7 입니다.
- 따라서 `[2,5,7,9,12]` 를 return 해야 합니다.

# 내가 푼 방식

```js
function solution(numbers) {

    var answer = [];

    for(let i = 0; i < numbers.length; i++) {
        for(let j = i+1; j < numbers.length; j++) {

            const sum = numbers[i] + numbers[j];

            if(answer.indexOf(sum) === -1) { 
                answer.push(sum);
            }
        }
    }
    return answer.sort((a,b) => a - b);
}
```
1. numbers를 `for` 반복문으로 2번 실행한다. (i는 numbers의 첫번째 값이고 j는 그다음 값이 된다.)
2. `indexOf()`를 사용해서 중복되지 않는 값들을 answer배열에 `push()`한다.
3. answer배열을 `sort()`를 사용해서 오름차순으로 정렬한다.

# 다른 답안

```js
function solution(numbers) {
    const temp = []

    for (let i = 0; i < numbers.length; i++) {
        for (let j = i + 1; j < numbers.length; j++) {
            temp.push(numbers[i] + numbers[j])
        }
    }

    const answer = [...new Set(temp)]

    return answer.sort((a, b) => a - b);
}
```

* `sort()`를 사용해서 오름차순, 내림차순으로 정렬 할 수 있다.
    ```js
    answer.sort((a,b) => a - b); // 오름차순
    answer.sort((a,b) => b - a); // 내림차순
    ```

* `new Set()`을 사용해서 중복되지 않는 값을 사용할 수 있다.
    ```js
    const answer = [...new Set(temp)]
    ```




