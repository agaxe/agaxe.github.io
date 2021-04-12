---
layout: post
title: '[JavaScript] var, let, const 차이점'
categories: ['Javascript']
bgColor: '#F7DF1E'
---

자바스크립트에는 `var`, `let`, `const` 3가지의 변수 선언 방식이 있다.

간단하게는 알고 있지만, 구체적으로 어떤 차이점이 있는지 정리해보려고 한다.

---

차이점을

##### 1. 재선언과 재할당

##### 2. 레벨 스코프

##### 3. 호이스팅

이 3가지로 분류해서 정리하려고 한다.

## 1. 재선언과 재할당

-   `var` 의 경우 재선언과 재할당 모두 가능하다.

```js
var age = 20;
console.log(age); // 20

var age = 30;
console.log(age); // 30
```

-   `let` 의 경우 재선언은 불가능하고 재할당은 가능하다.

```js
// 재선언은 불가능

let age = 20;
console.log(age); // 20

let age = 30; // Uncaught SyntaxError: Identifier 'age' has already been declared
```

```js
// 재할당은 가능

let age = 20;
console.log(age); // 20

age = 30;
console.log(age); // 30
```

-   `const` 의 경우 재선언과 재할당 모두 불가능하다.

```js
// 재선언 불가능

const age = 20;
console.log(age); // 20

const age = 30; // Uncaught SyntaxError: Identifier 'age' has already been declared
```

```js
// 재할당도 불가능

const age = 20;
console.log(age); // 20

age = 30; // Uncaught SyntaxError: Identifier 'age' has already been declared
```

## 2. 레벨 스코프

-   `var` 는 <mark>함수 레벨 스코프 (function-level scope)</mark> 를 따른다.
-   `const` 와 `let` 은 <mark>블록 레벨 스코프 (block-level scope)</mark> 를 따른다.
-   스코프에 관련된 정보는 [해당 포스팅](/javascript/2021/03/16/javascript-scope.html)에서 확인할 수 있다.

## 3. 호이스팅

호이스팅이란 함수 안에 있는 선언을 최상단으로 끌어 올리는 (Hoisting) 것을 의미한다.

-   `var` 의 경우

기존 코드

```js
var a = 10;

console.log(a); // 10
```

호이스팅 결과

```js
var a; // 선언이 최상단으로 끌어올려짐

a = 10; // 할당

console.log(a); // 결과 : 10
```

-   `let`, `const` 의 경우

`var` 랑 다르게 ReferenceError 가 발생한다.

```js
console.log(a); // undefined
console.log(b); // ReferenceError
console.log(c); // ReferenceError

var a = 'a';
let b = 'b';
const c = 'c';
```

이는 TDZ (Temporal Dead Zone) 에서 에러가 나타나기 때문이다.

#### TDZ (Temporal Dead Zone)

변수의 선언에는 총 3단계가 있다.

1. 선언 단계 (Declaration phase)
2. 초기화 단계 (Initialization phase)
3. 할당 단계 (Assignment phase)

-   `var` 는 선언 단계와 초기화 단계가 동시에 진행된다.
-   `let` 은 각각 따로 진행된다.
-   `const` 는 3단계가 동시에 진행된다.

<mark>TDZ (Temporal Dead Zone)</mark> 는 스코프의 시작점부터 초기화 단계까지의 구간을 의미한다.

![js-in-tdz-img](/img/posts/javascript/var-let-const/temporal-dead-zone-in-javascript.png)
<small>이미지 출처 : https://dmitripavlutin.com/javascript-variables-and-temporal-dead-zone/</small>

TDZ 로 인해 `let` 과 `const` 가 호이스팅이 되어 변수가 선언되었지만 초기화 단계가 진행되지않아 ReferenceError 가 생기는 것이다.

ReferenceError 가 발생해서 `let` 과 `const` 가 호이스팅이 되지 않는 것이라고 생각할 수도 있지만, 호이스팅이 된다.

```js
let age = 35;

(function () {
    // (*)
    console.log(age);
    let age = '27'; // ReferenceError: Cannot access 'age' before initialization
})();

// 6번 줄의 변수가 함수의 최상단(*)으로 호이스팅 되어 ReferenceError 가 발생한다.
```

## 요약

-   `var` 는 <mark>재선언과 재할당 모두 가능</mark>하다. <mark>함수 레벨 스코프 (function-level scope)</mark> 를 따른다.
-   `let` 은 <mark>재선언은 불가능하고 재할당은 가능</mark>하다. <mark>블록 레벨 스코프(block-level scope)</mark> 를 따른다.
-   `const` 는 <mark>재선언과 재할당 모두 불가능</mark>하다. <mark>블록 레벨 스코프(block-level scope)</mark> 를 따른다.
-   `let` 과 `const` 는 <mark>ES6 부터 추가</mark>되었다.
-   `let` 과 `const` 는 <mark>불변성의 차이</mark>가 있다.
-   <mark>변수의 선언 단계는 선언, 초기화, 할당</mark> 총 3가지의 단계가 있다.
-   `let` 과 `const` 는 <mark>호이스팅이 되지만 TDZ 로 인해 되지 않는 것처럼 보인다.</mark>

## 마무리

간단하게 var 는 좋지 않고 let 은 값을 바꿀 수 있고 const 값을 바꿀 수 없다! 라고만 생각했었는데 이번 기회에 더욱더 명확하게 차이점을 알 수 있었다.
