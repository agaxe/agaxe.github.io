---
layout: post
title:  "[Algorithm] 가운데 글자 가져오기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12903){:target="_blank"}

---

# 문제 설명

단어 s의 가운데 글자를 반환하는 함수, solution을 만들어 보세요. 단어의 길이가 짝수라면 가운데 두 글자를 반환하면 됩니다.

# 제한사항

- s는 길이가 1 이상, 100이하인 스트링입니다.


# 입출력 예

| s       | return |
| ------- | ------ |
| "abcde" | "c"    |
| "qwer"  | "we"   |


---

# 내가 푼 방식

```js
function solution(s) {
    var answer = 0;

    // (1)
    if(s.length % 2 === 0){
        // (2)
        answer = s[s.length / 2 - 1] + s[s.length / 2]
    }
    // (3)
    else{
        // (4)
        answer = s[s.length / 2 - 0.5]
    }

    return answer;
}
```

1. 매개변수로 받은 글자(s)의 수가 <mark>짝수</mark>인 경우
2. s[s.length / 2 - 1] + s[s.length / 2]
    ```js
    // ex) qwer
    // s[4 / 2 - 1] = w
    // s[4 / 2] = e
    ```
3. 매개변수로 받은 글자(s)의 수가 <mark>홀수</mark>인 경우
4. s[s.length / 2 - 0.5]
    ```js
    // ex) abcde
    // s[5 / 2 - 0.5] = c
    ```

# 다른 답안

```js
function solution(s) {
    return s.substr(Math.ceil(s.length / 2) -1,s.length % 2 === 0 ? 2 : 1)
}
```

1. `substr()`의 첫 번째 인자에는 s.length / 2를 `Math.ceil()`를 사용해서 소수점 이하를 올림 한 뒤 -1을 한 값을 추가한다.
2. `substr()`의 두 번째 인자에는 짝수일 경우 2를 추가, 홀수일 경우 1을 추가한다.  
3. 짝수일 경우
    ```js
    // ex) qwer
    // s.substr(1, 2) = we
    ```
4. 홀수일 경우
    ```js
    // ex) abcde
    // s.substr(2, 1) = c
    ```


