---
layout: post 
title:  "[Algorithm] 문자열 내림차순으로 배치하기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12917){:target="_blank"}

---

# 문제 설명

문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.   
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.


# 제한 사항

- str은 길이 1 이상인 문자열입니다.


# 입출력 예

| s         | return    |
| --------- | --------- |
| "Zbcdefg" | "gfedcbZ" |


---

# 답안

```js
function solution(s){
    return s.split('').sort((a,b) => a < b ?  1 : -1).join('')
}
```

- 매개변수 s를 `split()`를 사용해서 배열로 변경하고, `sort()`를 사용해서 내림차순으로 정렬 후 `join()`을 사용해서 다시 문자열로 변경해준다.
