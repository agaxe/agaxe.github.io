---
layout: post
title:  "[Javascript] 클로저 (Closure)"
categories: ['Javascript']
---

# 클로저의 정의

* <mark>함수와 그 함수가 선언됐을 때의 어휘적 환경(Lexical environment)과의 조합</mark>
* 내부함수가 외부함수의 변수(자유변수)를 참조할 수 있는 함수
* 어떤 함수에서 선언한 변수를 참조하는 내부함수에서만 발생하는 현상

```js
function outerFunc() {
    var x = 10;
    var innerFunc = function () { 
        console.log(x); 
    };
    return innerFunc;
}

var inner = outerFunc();
inner(); // 10
```

예제의 9번째줄을 보면 inner에 outerFunc()를 할당하면, 실행이 되어 내부함수인 innerFunc()가 return이 된다.
그 이후 inner()를 실행하면 innerFunc()가 실행이 되는데, outerFunc()가 실행이 완료(콜스택에서 제거)되어 소멸한 줄 알았던 변수 x의 값이 존재해 10이 출력된다.

* innerFunc() 는 클로저 함수이다.
* 변수 x 는 자유변수이다.

# 어휘적 환경 (Lexical environment)

<!-- <mark>함수 생성 시 함수의 범위에 있는 모든 변수로 구성된 환경</mark> -->
<mark>특정 함수나 코드 블록({..})안의 환경정보를 담고있는 객체</mark>


* 선언한 위치를 기준으로 환경이 결정된다.
* 정의에서의 환경정보는 변수 식별자, 함수 등이 있다.

# 어휘적 범위 지정 (Lexical scope)

* 함수가 <mark>선언된 위치를 기준</mark>으로 상위 스코프가 결정되는 것
* <mark>정적 스코프(Static scope)</mark> 라고도 한다.


# 클로저의 활용

## 은닉화
```js
function Counter() {
  // 카운트를 유지하기 위한 자유 변수
  var counter = 0;

  // 클로저
  this.increase = function () {
    return ++counter;
  };

  // 클로저
  this.decrease = function () {
    return --counter;
  };
}

const counter = new Counter();

console.log(counter.increase()); // 1
console.log(counter.decrease()); // 0
```

increase와 decrease를 사용해야지만 Counter 생성자의 자유 변수인 counter에 접근할 수 있다.

## 일반적인 실수

```js
var arr = [];

for (var i = 0; i < 5; i++) {
  arr[i] = function () {
    return i;
  };
}

for (var j = 0; j < arr.length; j++) {
  console.log(arr[j]());
}
```

반복문을 사용하여 arr 이란 배열에 숫자를 넣은 다음 배열의 숫자를 콘솔로 실행하려고 하는 경우
원하는 결과는 1,2,3,4,5 가 출력이 돼야 하는데 위의 코드는 5가 5번이 출력된다.

그 이유는 5번째 줄의 `return i;` 의 `i` 는 전역변수의 i를 참조하기 때문에 5가 된다.

원하는 결과를 얻기 위해서는 아래와 같이 수정을 해야 한다.

```js
var arr = [];

for (var i = 0; i < 5; i++){
  arr[i] = (function (id) {
    return function () {
      return id;
    };
  }(i));
}

for (var j = 0; j < arr.length; j++) {
  console.log(arr[j]());
}
```

콘솔을 실행하는 부분은 같지만 `arr[]` 배열에 값을 추가하는 코드에서 즉시 함수 호출을 사용하여 인자값으로 `i`를 전달해주고 그 값을 매개변수 `id`로 받아 `return id;` 를 하였다.   

이런 형식으로 하면 이전 코드처럼 전역변수의 `i`를 참조하는 것이 아니라 인자값으로 전달받은 `i`를 `id`로 받아 반복문을 실행할 때마다 새로운 `i` 값을 참조하기 때문에 원하는 결과가 나온다.

```js
const arr = [];

for (let i = 0; i < 5; i++) {
  arr[i] = function () {
    return i;
  };
}

for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]());
}
```

또한 위의 코드처럼 `let`을 사용하면 처음의 코드 형식을 사용하여 구현할 수도 있다.

# 메모리 관리

외부함수(outerFunc)의 변수(x)는 클로저가 참조하기 때문에 GC(가비지 컬렉터)의 수거 대상이 되지 않는다.
그로 인해 불필요하게 메모리가 소모되므로 클로저의 사용이 완료되면 nulll 이나 undefined를 할당하여 GC의 수거 대상으로 만들어 주는 것이 좋다.

```js
function outerFunc() {
    var x = 10;
    var innerFunc = function () { 
        console.log(x); 
    };
    return innerFunc;
}

var inner = outerFunc();
inner();
inner = null; // innerFunc() 의 참조를 제거
```

# 출처 

[https://poiemaweb.com/js-closure](https://poiemaweb.com/js-closure){:target="_blank"}
[https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures](https://developer.mozilla.org/ko/docs/Web/JavaScript/Closures){:target="_blank"}
[https://hyunseob.github.io/2016/08/30/javascript-closure/](https://hyunseob.github.io/2016/08/30/javascript-closure/){:target="_blank"}