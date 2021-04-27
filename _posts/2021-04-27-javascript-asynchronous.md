---
layout: post
title:  "[Javascript] 비동기 처리"
categories: ['Javascript']
---

# 비동기 처리란?

* <mark>비동기(Asynchronous)</mark>
* 동기(Synchronous)의 반대개념 
* 특정 코드의 실행이 완료되기 전에 다음 코드를 실행하는 것   
* 특정 코드를 기다리지 않고 다음 코드가 실행되는 것

## 비동기 처리 예제

```js
console.log(1)
setTimeout(() => console.log(2),1000)
console.log(3)

// 1
// 3
// (1초 뒤) 2
```

해당 코드는 비동기 처리로 인해 코드의 순서인 1, 2, 3이 아니라 1, 3이 먼저 실행이 되고 1초 뒤에 2가 실행된다.


# 콜백

콜백 함수를 사용하면 원하는 순서인 1, 2, 3을 구현할 수 있다.

```js
function num2(callbackFunc){
  setTimeout(() => {
    console.log(2);
    callbackFunc();
  },1000)
}

console.log(1);
num2(function(){
  console.log(3)
})


// 1
// (1초 뒤) 2
// 3
```

## 콜백 지옥

위의 예제처럼 콜백함수를 사용해서 비동기를 처리할 수 있지만 처리해야 하는 코드가 많아지면 들여쓰기가 깊어져 가독성도 떨어지고 수정도 어려워지는 콜백 지옥 현상(*)이 일어난다.
```js
function num2(callbackFunc){
  setTimeout(() => {
    console.log(2)
    callbackFunc();
  },1000)
}
function num3(callbackFunc){
  setTimeout(() => {
    console.log(3)
    callbackFunc();
  },1000)
}
function num4(callbackFunc){
  setTimeout(() => {
    console.log(4)
    callbackFunc();
  },1000)
}

console.log(1)
num2(function(){ // (*)
  num3(function(){
    num4(function(){
      console.log('end')
    })
  })
})

// 1
// (1초 뒤) 2
// (1초 뒤) 3
// (1초 뒤) 4
// end
```
이를 해결하기 위해서는 함수를 분리해주면 해결된다.

```js
function num2(){
  setTimeout(() => {
    console.log(2)
    num3();
  },1000)
}
function num3(){
  setTimeout(() => {
    console.log(3)
    num4();
  },1000)
}
function num4(){
  setTimeout(() => {
    console.log(4)
    console.log('end')
  },1000)
}

console.log(1)
num2()

// 1
// (1초 뒤) 2
// (1초 뒤) 3
// (1초 뒤) 4
// end
```
이런 식으로 함수를 분리하면 콜백지옥 현상이 일어나지 않지만, 코드를 해석할 때 함수명을 계속 추적해야 한다는 단점이 있다.
그래서 ES6에서는 Promise와 Generator 등이 도입되었고, ES2017에서는 async/await가 도입되었다.


# Promise

* 자바스크립트 비동기 처리에 사용되는 객체
* Promise는 <mark>대기(pending)</mark>, <mark>이행(fulfilled)</mark>, <mark>거부(rejected)</mark> 총 3가지의 상태를 가진다.
* Promise 객체는 <mark>state와 result</mark>, 2개의 프로퍼티를 가지고 있다.
* Promise 객체의 <mark>초기값은 state는 "pending", result는 undefined</mark>를 가진다.
* 인수로 넘겨준 콜백 중 <mark>하나를 반드시 호출</mark>해야 한다. (resolve, reject)
* resolve와 reject중 <mark>먼저 호출된 함수가 호출</mark>된다.

```js
let promise = new Promise(function(resolve, reject){
  // resolve나 reject를 반드시 호출
})

console.log(promise);
// Promise 객체의 초기값
/*
{
  state : "pending"
  result: undefined
}
*/
```

## resolve

* <mark>일이 성공적으로 완료</mark>된 경우 결과와 함께 호출
* Promise 객체의 <mark>state는 "fulfilled"</mark>, <mark>result는 해당 결과값</mark>으로 변한다.

```js
let promise = new Promise(function(resolve, reject){
  resolve('성공!');
})

console.log(promise);
// resolve 호출 시의 Promise 객체
/*
{
  state : "fulfilled"
  result: "성공!"
}
*/
```

## reject

* <mark>에러 발생 시</mark> 에러 객체인 error와 함께 호출
* Promise 객체의 <mark>state는 "rejected"</mark>, <mark>result는 해당 에러값</mark>으로 변한다.

```js
let promise = new Promise(function(resolve, reject){
  reject(new Error('에러 발생!'));
})

console.log(promise);
// reject 호출 시의 Promise 객체
/*
{
  state : "rejected"
  result: "에러 발생!"
}
Error: 에러 발생!
*/
```

## then

* 첫 번째 인수는 이행(성공)됐을 경우 실행, 두 번째 인수는 거부(에러)됐을 경우 실행
  ```js
  promise.then(
    function(result){/* result를 다룸 */},
    function(error){/* error를 다룸 */}
  )
  ```
* 이행(성공)된 경우
  ```js
  let promise = new Promise(function(resolve, reject) {
    resolve("성공!")
  });

  promise.then(
    result => console.log(result), // "성공"
    error => console.log(error) // 실행되지 않음
  );
  ```
* 거부(에러)된 경우
  ```js
  let promise = new Promise(function(resolve, reject) {
    reject(new Error('에러 발생!'));
  });

  promise.then(
    result => console.log(result), // 실행되지 않음
    error => console.log(error) // Error: 에러 발생!
  );
  ```

## catch

* 에러가 발생한 경우만 다룰 경우 사용 
* then의 두 번째 인수와 동일
  ```js
  let promise = new Promise(function(resolve, reject) {
    reject(new Error('에러 발생!'));
  });

  promise.catch(
    error => console.log(error) // Error: 에러 발생!
  );
  ```

## finally

* 이행이나 거부 관계없이 항상 실행됨

```js
// 이행(성공)된 경우

let promise = new Promise(function(resolve, reject) {
  resolve('성공!');
});

promise
.finally(() => console.log('실행!'))
.then(
  result => console.log(result),
  error => console.log(error) // 실행되지 않음
);

// 실행!
// 성공!
```

```js
// 거부(에러)된 경우

let promise = new Promise(function(resolve, reject) {
  reject(new Error('에러 발생!'));
});

promise
.finally(() => console.log('실행!'))
.then(
  result => console.log(result), // 실행되지 않음
  error => console.log(error)
);

// 실행!
// Error: 에러 발생!
```

## Promise 체이닝

* Promise의 결과값이 then 핸들러의 체인(사슬)을 통해 전달되는 것
  ```js
  new Promise(function(resolve, reject) {
    resolve(1);
  }).then(function(result){
    console.log(result); // 1
    return result * 2;
  }).then(function(result){
    console.log(result); // 2
    return result * 2;
  }).then(function(result){
    console.log(result); // 4
    return result * 2;
  });
  ```
* fetch를 사용하는 경우 자주 사용된다.
  ```js
  fetch('https://ko.javascript.info/article/promise-chaining/user.json')
  .then(function(res){
    return res.json() // JSON으로 파싱
  })
  .then(function(user){
    console.log(user.name) // iliakan
  })
  ```


# Promise 메서드

## Promise.all

* 요소 전체가 Promise인 배열을 받아 새로운 Promise를 반환하는 메서드
* <mark>모든 Promise가 이행될 때까지 기다렸다가 결과값을 반환</mark>한다.
* Promise.all에 전달되는 값이 하나라도 거부되면 반환하는 값은 에러와 함께 거부되고 나머지 결과는 무시된다.

```js
let urls = [
  'https://api.github.com/users/iliakan',
  'https://api.github.com/users/remy',
  'https://api.github.com/users/jeresig'
];

let requests = urls.map(url => fetch(url));

console.log('requests',requests); // [Promise, Promise, Promise]

Promise.all(requests)
.then(responses => responses.forEach(
  response => console.log(`${response.url}: ${response.status}`)
));

// https://api.github.com/users/iliakan: 200
// https://api.github.com/users/remy: 200
// https://api.github.com/users/jeresig: 200
```

## Promise.race

* all과 비슷하지만 <mark>먼저 처리</mark>되는 Promise의 값 또는 에러를 반환한다.
* race = 경주

```js
Promise.race([
  new Promise((resolve, reject) => setTimeout(() => resolve(1), 1000)),
  new Promise((resolve, reject) => setTimeout(() => reject(new Error("에러 발생!")), 2000)),
  new Promise((resolve, reject) => setTimeout(() => resolve(3), 3000))
]).then(console.log); // 1
```


# async/await

* async/await를 사용하면 Promise를 더욱 편리하게 사용할 수 있다.

## async

* <mark>함수 앞에 위치</mark>한다.
* async를 추가한 함수는 await를 사용할 수 있다.
* async를 추가한 함수는 <mark>항상 Promise를 반환</mark>한다.

```js
async function func(){
  return '반환값!';
}

console.log(func()); // Promise {...}
func().then(res => console.log(res)) // '반환값!'
```

## await

* <mark>async 함수 안에서만 동작</mark>한다.
* Promise가 처리될 때까지 기다린 뒤 결과를 반환한다. (await = 기다리다)

```js
// 이행(성공)된 경우

async function func() {
  try {
    let response = await fetch('https://ko.javascript.info/article/promise-chaining/user.json');
    let user = await response.json();
    console.log(user) // {name: "iliakan", isAdmin: true}
  } catch(err) {
    console.log(err); // 실행되지 않음
  }
}
func();
```
```js
// 거부(에러)된 경우

async function func() {
  try {
    let response = await fetch('http://유효하지-않은-url');
    let user = await response.json();
    console.log(user) // 실행되지 않음
  } catch(err) {
    console.log(err); // TypeError: Failed to fetch
  }
}
func();
```

---

### 참고 

[https://ko.javascript.info/async](https://ko.javascript.info/async){:target="_blank"}