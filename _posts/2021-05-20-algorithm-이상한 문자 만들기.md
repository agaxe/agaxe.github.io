---
layout: post
title:  "[Algorithm] 이상한 문자 만들기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12930){:target="_blank"}

---

# 문제 설명

문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.


# 제한 사항

- 문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
- 첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.


# 입출력 예

| s                 | return            |
| ----------------- | ----------------- |
| "try hello world" | "TrY HeLlO WoRlD" |


# 입출력 예 설명

"try hello world"는 세 단어 "try", "hello", "world"로 구성되어 있습니다. 각 단어의 짝수번째 문자를 대문자로, 홀수번째 문자를 소문자로 바꾸면 "TrY", "HeLlO", "WoRlD"입니다. 따라서 "TrY HeLlO WoRlD" 를 리턴합니다.

---

# 내가 푼 방식

```js
function solution(s) {
    return s.split(' ').map((v, i) => ( // (1)
        v.split('').map((val, idx) => ( // (2)
            idx % 2 === 0 ? val.toUpperCase() : val.toLowerCase() // (3)
        )).join('') // (4)
    )).join(' ') // (5)
}
```

1. 매개변수로 받은 문자열 s를 `split()`를 사용해서 공백을 기준으로 배열로 만든 뒤 `map()`을 사용해서 반복문을 실행한다.
2. 해당 단어를 `split()`를 사용해서 배열로 만든 뒤 `map()`을 사용해서 반복문을 실행한다.
3. 만약 해당 인덱스가 짝수이면 대문자로(`toUpperCase()`), 홀수면 소문자로(`toLowerCase()`) 변경해준다.
4. 2번의 배열을 문자열로 만들어준다.
5. 1번의 배열을 문자열로 만들어준다.

```js
/*  
    ex) s = "try hello world"

    1. s.split(' ') = ["try", "hello", "world"]
    2. v.split('') = [ 
        ["t", "r", "y"], 
        ["h", "e", "l", "l", "o"],
        ["w", "o", "r", "l", "d"]
    ]
    3. [
        ["T", "r", "Y"],
        ["H", "e", "L", "l", "O"],
        ["W", "o", "R", "l", "D"]
    ]
    4. ["TrY", "HeLlO", "WoRlD"]
    5. "TrY HeLlO WoRlD"
*/
```

# 다른 답안

```js
function solution(s) {
    return s.toUpperCase().replace(/(\w)(\w)/g, function(a){return a[0].toUpperCase() + a[1].toLowerCase();})
}
```

1. 매개변수s를 모두 대문자로 변경해준다.
2. `replace()`에 정규표현식을 사용해서 s에서 연속으로 두 글자인 부분을 선택하고(`(\w)(\w)`)
3. 두 글자 중 짝수값(`a[0]`)을 대문자로 변경하고, 홀수값(`a[1]`)을 소문자로 변경해준다.

```js
/*
    ex) s = "try hello world"

    1. "TRY HELLO WORLD"
    2. "TRY HELLO WORLD".replace(/(\w)(\w)/g) = "(TR)Y (HE)(LL)O (WO)(RL)D" 
    3.  (TR)
            a[0] = T = T
            a[1] = R = r 
        (HE)
            a[0] = H = H
            a[1] = R = e 
        (LL)
            a[0] = L = L
            a[1] = L = l 
        (WO)
            a[0] = W = W
            a[1] = O = o 
        (RL)
            a[0] = R = R
            a[1] = L = l

    =>  "TrY HeLlO WoRlD"      
*/ 
```
