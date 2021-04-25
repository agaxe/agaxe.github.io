---
layout: post
title:  "[Javascript] 스코프 (Scope)"
categories: ['Javascript']
---

# 스코프의 정의

<mark>변수, 함수 등에 접근할 수 있는 범위 (Scope)</mark>

# 스코프의 구분

### 전역 스코프 (Global scope)

* 코드 어디서든 참조할 수 있다.

```js
var global = '전역';

function foo() {
    console.log(global); // '전역'
}
foo();

console.log(global); // '전역'
```

### 지역 스코프 (Local scope or Function-level scope)

* 함수 자신의 스코프나 하위 스코프에서만 참조할 수 있다.

```js
var global = '전역';

function foo() {
    var local = '지역'
    console.log(global); // '전역'
    console.log(local); // '지역'
}
foo();

console.log(global); // '전역'
console.log(local); // Uncaught ReferenceError: local is not defined
```


## 변수의 스코프

<mark>변수는 선언한 위치(전역 또는 지역)에 따라 스코프가 결정된다.</mark>

* ### 전역 변수 (Global variable)

    * 전역에서 변수의 참조가 가능하다.
    * `var` 를 사용한 전역변수는 전역객체인 `window` 의 프로퍼티이다.
    * <mark>전역변수는 변수의 이름이 중복될 가능성이 크고 의도치 않는 재할당으로 인해 코드를 예측하기가 어렵다.</mark>

* ### 지역 변수 (Local variable)

    * 선언된 지역과 그 하위 지역 내에서만 참조가 가능하다.


# 자바스크립트 스코프의 특징

* 대부분의 언어는 블록 레벨 스코프(block-level scope)이지만 <mark>자바스크립트는 함수 레벨 스코프(function-level scope)를 따른다.</mark>
* ES6부터 지원되는 `const` 이나 `let` 을 사용하면 블록 레벨 스코프를 사용할 수 있다.


# 함수 레벨 스코프 (Function-level scope)

함수 내에서 선언된 변수는 해당 함수 외부에서는 유효하지 않은 스코프이다.

> 함수가 유효범위이다!

```js
function foo(){
    if(true){
        var bar = 'bar'
    }
    console.log(bar)
}

foo(); // bar
console.log(bar) // // Uncaught ReferenceError: bar is not defined
```
함수 레벨 스코프는 유연하지만, 그로 인해 버그 발생, 메모리 누수, 디버깅의 어려움 등의 문제가 발생하기 때문에 블록 레벨 스코프를 사용하는 것이 좋다고 한다.

# 블록 레벨 스코프 (Block-level scope)

블록({…}) 내에서만 유효한 스코프이다.

> 블록이 유효범위이다!

```js
function foo(){
    if(true){
        let a = 'kim'
        const b = 'lee'
    }

    console.log(a) //Uncaught ReferenceError: a is not defined
    console.log(b) // Uncaught ReferenceError: b is not defined
}
foo();
```

# 렉시컬 스코프 (Lexical scope)

함수를 어디서 호출하는지가 아니라 <mark>어디에 선언하였는지에 따라 스코프를 결정하는 것</mark>을 렉시컬 스코프 또는 정적 스코프라고 한다.

```js
var x = 1;

function foo() {
  var x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo(); // 1
bar(); // 1
```

해당 코드의 3번째 줄의 `foo()` 에서 `bar()` 를 호출하면, 호출한 `foo()` 스코프의 `x` (4번째 줄) 가 아닌 `bar()` 를 <mark>선언한 위치</mark>인 
전역 스코프의 `x`(1번째 줄) 를 참조하기 때문에 두 함수의 결과는 1이 된다.


## 출처 

[https://poiemaweb.com/js-scope](https://poiemaweb.com/js-scope){:target="_blank"}





