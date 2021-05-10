---
layout: post
title:  "[Algorithm] 소수 만들기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12977){:target="_blank"}

---

# 문제 설명

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

# 제한 사항

- nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
- nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.


# 입출력 예

| nums        | result |
| ----------- | ------ |
| [1,2,3,4]   | 1      |
| [1,2,7,6,4] | 4      |

# 입출력 예 설명

**입출력 예 #1**

- [1,2,4]를 이용해서 7을 만들 수 있습니다.

**입출력 예 #2**

- [1,2,4]를 이용해서 7을 만들 수 있습니다.
- [1,4,6]을 이용해서 11을 만들 수 있습니다.
- [2,4,7]을 이용해서 13을 만들 수 있습니다.
- [4,6,7]을 이용해서 17을 만들 수 있습니다.

---

# 답안

```js
function solution(nums) {
    var answer = 0;
    let sumList = [];
    
    // (3)
    function isPrime(sum){
        for(let i = 2; i <= Math.sqrt(sum); i++){
            if(sum % i === 0){
                return false;
            }
        }
        return true;
    }
    
    // (1)
    for(let i = 0; i < nums.length; i++){
        for(let j = i+1; j < nums.length; j++){
            for(let k = j+1; k < nums.length; k++){
                // (2)
                sumList.push(nums[i] + nums[j] + nums[k])
            }
        }
    }
    
    // (4)
    for(let i = 0; i < sumList.length; i++){
        // (5)
        if(isPrime(sumList[i])) answer++
    }
    
    return answer;
}
```

1. 매개변수로 받은 nums배열을 `for`반복문을 3번 사용한다.
2. nums[i]+nums[j]+nums[k]값을 합계 배열인 sumList에 추가한다.
3. 소수를 구하는 함수 isPrime를 만들어 준다.
  ```js
    function isPrime(sum){
        // (1)
        for(let i = 2; i <= Math.sqrt(sum); i++){
            // (2)
            if(sum % i === 0){
                return false;
            }
        }
        return true;
    }

    // 1. 매개변수로 받은 값의 제곱근만큼 반복문을 실행한다. 
    // 2. 반환한 제곱근의 i의 나머지 값이 0이면 false(소수x), 아니면 true(소수o)를 반환
  ```
4. 합계 배열인 sumList의 개수만큼 `for`반복문을 실행한다.
5. 3번에서 만든 isPrime() 함수에 sumList[i]를 인자로 보낸 뒤 해당 값이 true면 answer를 +1 해준다.
