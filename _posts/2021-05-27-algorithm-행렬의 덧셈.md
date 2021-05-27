---
layout: post 
title:  "[Algorithm] 행렬의 덧셈"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12950){:target="_blank"}

---

# 문제 설명

행렬의 덧셈은 행과 열의 크기가 같은 두 행렬의 같은 행, 같은 열의 값을 서로 더한 결과가 됩니다. 2개의 행렬 arr1과 arr2를 입력받아, 행렬 덧셈의 결과를 반환하는 함수, solution을 완성해주세요.


# 제한 조건

- 행렬 arr1, arr2의 행과 열의 길이는 500을 넘지 않습니다.


# 입출력 예

| arr1          | arr2          | return        |
| ------------- | ------------- | ------------- |
| [[1,2],[2,3]] | [[3,4],[5,6]] | [[4,6],[7,9]] |
| [[1],[2]]     | [[3],[4]]     | [[4],[6]]     |

---

# 내가 푼 방식

```js
function solution(arr1, arr2) {
    return arr1.map((v,i) => v.map((val,idx) => val + arr2[i][idx]))
}
```

1. `map()`을 사용해서 arr1배열의 항목(2차원 배열)에 접근한다.
2. arr1배열의 항목(2차원 배열)에 `map()`을 사용하여 arr1[i][j]값(val) 과 arr2[i][j] 값을 더한 뒤 배열을 반환해준다.


# 다른 답안

```js
function solution(arr1, arr2) {
    var answer = Array();
    
    for(var i = 0; i < arr1.length; i++){
        answer[i] = []; 
        for(var j = 0; j < arr1[i].length; j++){
            answer[i][j] = arr1[i][j] + arr2[i][j];             
        }
    }
    return answer;
}
```

1. answer라는 빈 배열을 만든다.
2. arr1.length만큼 `for()` 반복문을 실행하고
3. answer안의 해당 인덱스의 빈 배열을 만들어준다. (answer[i] = [])
4. arr1[i].length만큼 `for()` 반복문을 실행하고
5. arr1[i][j]값과 arr2[i][j]값을 더한 값을 answer[i][j]에 할당해준다.