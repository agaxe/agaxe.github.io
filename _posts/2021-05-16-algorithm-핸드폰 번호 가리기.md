---
layout: post
title:  "[Algorithm] 핸드폰 번호 가리기"
categories: ['Algorithm']
---

[프로그래머스 문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12948){:target="_blank"}

---

# 문제 설명

프로그래머스 모바일은 개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.   
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 `*`으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.


# 제한사항

- s는 길이 4 이상, 20이하인 문자열입니다.


# 입출력 예

| phone_number  | return        |
| ------------- | ------------- |
| "01033334444" | "\*\*\*\*\*\*\*4444" |
| "027778888"   | "\*\*\*\*\*8888"   |

---

# 내가 푼 방식

```js
function solution(phone_number) {
    const length = phone_number.length - 4; // (1)
    let star = '';
    
     // (2)
    for(let i = 0; i < length; i++){
        star += '*'
    }
    return phone_number.replace(phone_number.substr(0,length),star) // (3)
}
```

1. 매개변수로 받은 휴대폰 번호의 길이에서 뒷 4자리를 뺀 길이값을 구한다.
2. 뒷 4자리를 뺀 휴대폰번호의 길이만큼 `for` 반복문을 실행하여 star변수에 *을 추가시켜준다.
3. 휴대폰 번호에 `replace()`를 사용하여 첫번째 인자에는 `substr()`를 사용해서 뒷 4자리를 뺀 번호를 구한 값을,두번째 인자에는 2번에서 추가한 *를 넣어준다. 


# 다른 답안

```js
function solution(phone_number) {
  const regex = /\d(?=\d{4})/g;
  return phone_number.replace(regex, "*");
  
  //return phone_number.replace(/\d(?=\d{4})/g, "*");
}
```

- 정규표현식을 사용하여 뒷 4자리를 제외한 값을 *로 변경해주었다.