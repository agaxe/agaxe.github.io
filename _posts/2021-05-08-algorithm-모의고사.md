---
layout: post
title:  "[Algorithm] 모의고사"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42840){:target="_blank"}

---

# 문제 설명

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.  

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...  
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...  
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...  

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.


# 제한 조건

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.


# 입출력 예

| answers     | return  |
| ----------- | ------- |
| [1,2,3,4,5] | [1]     |
| [1,3,2,4,2] | [1,2,3] |

# 입출력 예 설명

**입출력 예 #1**

- 수포자 1은 모든 문제를 맞혔습니다.
- 수포자 2는 모든 문제를 틀렸습니다.
- 수포자 3은 모든 문제를 틀렸습니다.

따라서 가장 문제를 많이 맞힌 사람은 수포자 1입니다.

**입출력 예 #2**

- 모든 사람이 2문제씩을 맞췄습니다.

---

# 내가 푼 방식

```js
function solution(answers) {
    var answer = [];

    // (1)
    let supo1 = [1, 2, 3, 4, 5]
    let supo2 = [2, 1, 2, 3, 2, 4, 2, 5]
    let supo3 = [3, 3, 1, 1, 2, 2, 4, 4, 5, 5];

    // (2)
    let cnt = [0,0,0];

    // (3)
    for(let i = 0; i < answers.length; i++){
        // (4)
        (supo1[i%supo1.length] === answers[i]) && cnt[0]++;
        (supo2[i%supo2.length] === answers[i]) && cnt[1]++;
        (supo3[i%supo3.length] === answers[i]) && cnt[2]++;
    }

    // (5)
    let max = Math.max(...cnt);

    // (6)
    for(let j = 0; j < cnt.length; j++){
        if(cnt[j] === max){
            answer.push(j+1)
        }
    }

    return answer;
}
```

1. 수포자1, 수포자2, 수포자3의 찍는 방식을 배열에 추가
2. 수포자1, 수포자2, 수포자3가 각각 맞춘 정답 수를 0으로 정의해준다.
3. 정답 수만큼 `for`반복문을 실행한다.
4. <mark>나머지 연산자(%)를 사용</mark>해서 수포자들의 찍는 방식을 반복처리 해주고 정답의 인덱스값과 같으면 정답 수의 해당 인덱스에 1을 추가해준다.
5. 정답 수 배열에서 가장 큰 값을 구한다.
6. 정답 수 배열을 `for`반복문으로 실행 후 해당 인덱스값이 가장 큰 값과 같으면 answer배열에 해당 인덱스의 +1값을 추가해준다.

# 다른 답안

```js
function solution(answers) {
    var answer = [];
    var a1 = [1, 2, 3, 4, 5];
    var a2 = [2, 1, 2, 3, 2, 4, 2, 5]
    var a3 = [ 3, 3, 1, 1, 2, 2, 4, 4, 5, 5];

    var a1c = answers.filter((a,i)=> a === a1[i%a1.length]).length;
    var a2c = answers.filter((a,i)=> a === a2[i%a2.length]).length;
    var a3c = answers.filter((a,i)=> a === a3[i%a3.length]).length;
    var max = Math.max(a1c,a2c,a3c);

    if (a1c === max) {answer.push(1)};
    if (a2c === max) {answer.push(2)};
    if (a3c === max) {answer.push(3)};

    return answer;
}
```

- `filter`를 사용해서 수포자들의 정답값을 구했다.

