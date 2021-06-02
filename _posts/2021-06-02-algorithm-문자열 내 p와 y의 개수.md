---
layout: post 
title:  "[Algorithm] 문자열 내 p와 y의 개수"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12916){:target="_blank"}

---

# 문제 설명

대문자와 소문자가 섞여있는 문자열 s가 주어집니다. s에 'p'의 개수와 'y'의 개수를 비교해 같으면 True, 다르면 False를 return 하는 solution를 완성하세요. 'p', 'y' 모두 하나도 없는 경우는 항상 True를 리턴합니다. 단, 개수를 비교할 때 대문자와 소문자는 구별하지 않습니다.

예를 들어 s가 "pPoooyY"면 true를 return하고 "Pyy"라면 false를 return합니다.


# 제한 조건

- 문자열 s의 길이 : 50 이하의 자연수
- 문자열 s는 알파벳으로만 이루어져 있습니다.


# 입출력 예

| s         | answer |
| --------- | ------ |
| "pPoooyY" | true   |
| "Pyy"     | false  |

# 입출력 예 설명

**입출력 예#1**

'p'의 개수 2개, 'y'의 개수 2개로 같으므로 true를 return 합니다.

**입출력 예#2**

'p'의 개수 1개, 'y'의 개수 2개로 다르므로 false를 return 합니다.


---

# 내가 푼 방식

```js
function solution(s){
    // (1)
    let pLength = 0;
    let yLength = 0; 
    const S = s.toUpperCase(); // (2)
    
    // (3)
    for(let i = 0; i < s.length; i++){
        if(S[i] === 'P'){ // (4)
            pLength++
        }
        if(S[i] === 'Y'){ // (5)
            yLength++
        }
    }
    
    return pLength === yLength; // (6)
}
```

1. 매개변수s에서 'P'의 개수를 담을 pLength 변수와 'Y'의 개수를 담을 yLength 변수를 생성한다.
2. 매개변수s를 대문자로 변경한 값을 S변수에 할당한다.
3. `for()`를 사용하여 매개변수s의 길이만큼 반복문을 실행해준다.
4. 만약 해당 인덱스의 값이 'P'일 경우 pLength++를 해준다.
5. 만약 해당 인덱스의 값이 'Y'일 경우 yLength++를 해준다.
6. pLength와 yLength가 같다면 true, 아니면 false를 반환해준다.    
    (둘 다 없는 경우 1번에서 0을 할당하였기 때문에 true를 반환한다)


# 다른 답안

```js
function solution(s){
    return s.toUpperCase().split("P").length === s.toUpperCase().split("Y").length;
}
```

- 매개변수s를 대문자로 변경한 값을 'P'를 기준으로 생성한 배열의 길이와 'Y'를 기준으로 생성한 배열의 길이가 같을 경우 true, 아닐 경우 false를 반환한다.

```js
/*
    ex) s = "pPoooyY"

    s.toUpperCase().split("P") = ["","","OOOYY"] (3)
    s.toUpperCase().split("Y") = ["PPOOO","",""] (3)
    return true


    ex) s = "Pyy"

    s.toUpperCase().split("P") = ["","YY"] (2)
    s.toUpperCase().split("Y") = ["P","",""] (3)
    return false
*/
```