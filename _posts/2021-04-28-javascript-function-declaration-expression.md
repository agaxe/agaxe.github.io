---
layout: post
title:  "[Javascript] 함수 선언식과 함수 표현식"
categories: ['Javascript']
---

# 함수 선언식

* <mark>Function Declaration</mark>
* 함수를 <mark>함수명과 함께 선언</mark>하는 것
* 일반적인 함수 정의 방법

```js
function func(){
    console.log('func 실행!')
}
func(); // func 실행!
```

# 함수 표현식

* <mark>Function Expression</mark>
* 함수를 <mark>별도의 변수에 할당</mark>하는 것
* <mark>함수명을 정의하지 않은</mark> 함수 표현식은 <mark>익명 함수 표현식</mark>
* <mark>함수명을 정의</mark>한 함수 표현식은 <mark>기명 함수 표현식</mark>

```js
// 익명 함수 표현식
var func1 = function(){
    console.log('func1 실행!')
}
func1(); // func1 실행!


// 기명 함수 표현식
var func2 = function func3 (){
  console.log('func2 실행!')
}
func2(); // func2 실행!
func3(); // ReferenceError : func3 is not defined
```

# 차이점

## 1. 선언 방식

* 변수에 함수를 할당하는지의 차이가 있다.

## 2. 호이스팅

* <mark>함수 선언식</mark>은 <mark>함수 전체를 호이스팅</mark> 한다.
* <mark>함수 표현식</mark>은 함수를 할당한 <mark>변수 선언부만 호이스팅</mark> 한다.

```js
func1(); // 함수1 실행!
func2(); // TypeError : func2 is not a function

function func1(){
  console.log('함수1 실행!')
}

var func2 = function(){
  console.log('함수2 실행!')
}
```

---

### 참고

[코어 자바스크립트 (정재남 저)](https://wikibook.co.kr/corejs/){:target="_blank"}   
[https://ko.javascript.info/function-expressions](https://ko.javascript.info/function-expressions){:target="_blank"}