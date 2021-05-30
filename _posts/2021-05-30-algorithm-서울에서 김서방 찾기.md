---
layout: post 
title:  "[Algorithm] 서울에서 김서방 찾기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12919){:target="_blank"}

---

# 문제 설명

String형 배열 seoul의 element중 "Kim"의 위치 x를 찾아, "김서방은 x에 있다"는 String을 반환하는 함수, solution을 완성하세요. seoul에 "Kim"은 오직 한 번만 나타나며 잘못된 값이 입력되는 경우는 없습니다.


# 제한 사항

- seoul은 길이 1 이상, 1000 이하인 배열입니다.
- seoul의 원소는 길이 1 이상, 20 이하인 문자열입니다.
- "Kim"은 반드시 seoul 안에 포함되어 있습니다.


# 입출력 예

| seoul           | return              |
| --------------- | ------------------- |
| ["Jane", "Kim"] | "김서방은 1에 있다" |

---

# 내가 푼 방식

```js
function solution(seoul) {
    return `김서방은 ${seoul.findIndex(v => v === 'Kim')}에 있다`;
}
```

- `findIndex()`를 사용해서 seoul배열에서 Kim의 인덱스값을 반환해준다.


# 다른 답안

```js
function solution(seoul) {
    var idx = seoul.indexOf('Kim');
    return "김서방은 " + idx + "에 있다";
}
```

- `indexOf()`를 사용해서 seoul배열에서 Kim의 인덱스값을 반환해준다.