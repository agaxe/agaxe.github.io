---
layout: post
title:  "[Algorithm] K번째수"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42748?language=javascript#){:target="_blank"}

---

# 문제 설명

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.

예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면

1. array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.
2. 1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다.
3. 2에서 나온 배열의 3번째 숫자는 5입니다.
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

# 제한사항

* array의 길이는 1 이상 100 이하입니다.
* array의 각 원소는 1 이상 100 이하입니다.
* commands의 길이는 1 이상 50 이하입니다.
* commands의 각 원소는 길이가 3입니다.

# 입출력 예

| array                 | commands                          | return    |
|-----------------------|-----------------------------------|-----------|
| [1, 5, 2, 6, 3, 7, 4] | [[2, 5, 3], [4, 4, 1], [1, 7, 3]] | [5, 6, 3] |

# 입출력 예 설명

* [1, 5, 2, 6, 3, 7, 4]를 2번째부터 5번째까지 자른 후 정렬합니다. [2, 3, 5, 6]의 세 번째 숫자는 5입니다.
* [1, 5, 2, 6, 3, 7, 4]를 4번째부터 4번째까지 자른 후 정렬합니다. [6]의 첫 번째 숫자는 6입니다.
* [1, 5, 2, 6, 3, 7, 4]를 1번째부터 7번째까지 자릅니다. [1, 2, 3, 4, 5, 6, 7]의 세 번째 숫자는 3입니다.

---

# 내가 푼 방식

```js
function solution(array, commands) {
    var answer = [];
    let result;

    for(let n = 0; n < commands.length; n++){
        const currArray = commands[n];
        
        const i = currArray[0];
        const j = currArray[1];
        const k = currArray[2];
        
        result = array.slice(i-1,j).sort((a,b) => a - b);
        result = result[k-1];

        answer.push(result);
    }
    return answer;
}
```

* commands의 길이값만큼 반목문 실행
* 각각의 i, j, k 변수에 **시작 인덱스**, **종료 인덱스**, **출력할 인덱스**를 할당
* array에 `slice()`를 사용하여 **시작 인덱스**와 **종료 인덱스**를 기준으로 자른 뒤 `sort()`로 오름차순 정렬 후 result 변수에 할당
* 정렬한 배열에서 **출력할 인덱스**에 해당하는 값을 result에 재할당 후 answer에 `push()`

# 다른 답안

```js
function solution(array, commands) {
  var answer = [];
  
  answer = commands.map(command => {
    const [start, end, idx] = command; // (*)
    const newArray = array
      .filter((value,index) => index >= start -1 && index <= end - 1) // (*)
      .sort((a,b) => a - b);
    return newArray[idx - 1];
  }) 
 
  return answer;
}
```

* 비구조화 할당과 `filter()`를 사용해서 코드를 더욱 간결하게 작성하였다.
