---
layout: post
title:  "프로토타입 (Prototype)"
categories: ['Javascript']
---

# Prototype

* 자신을 생성하기 위해 사용된 객체의 원형
* 클래스라는 개념이 없던 ES6 이전의 자바스크립트에서 객체지향 프로그래밍을 하기 위해 사용되었음
* 부모객체의 속성이나 메소드를 **상속**받아 프로그래밍 하는 것을 **프로토타입 프로그래밍(Prototype-based programming)** 이라고 한다.
* **Prototype Object** 와 **Prototype Link** 2가지로 표현된다.

## Prototype Object

* 자신을 원형으로 만들어질 다른 객체가 참조할 프로토타입 객체
* 함수를 정의하면 프로토타입 객체가 생성된다.
* [function].prototype 으로 접근할 수 있다.
* constructor 와 \__proto__ 를 가지고 있다.

```js
function Guitar(){}

console.log(Guitar.prototype); // Prototype Object
/*
    constructor: ƒ Guitar()
    __proto__: Object
*/
```
### Constructor

* 선언한 생성자 함수 자체를 가리킨다.
* constructor 가 있어야 new 를 사용하여 인스턴스를 생성할 수 있다.
* new 를 사용하여 인스턴스 생성 시 constructor 함수를 실행하고 객체를 생성시킨다.

```js
function Guitar(){}
const electric = new Guitar();

console.log(electric.constructor === Guitar) // true
```

### \__proto__

* Prototype Link
* 모든 객체가 가지고 있는 속성
* 선언한 생성자의 Prototype Object 을 가리킨다.

```js
function Guitar(){}
const electric = new Guitar();

console.log(electric.__proto__ === Guitar.prototype) // true
```

# Prototype Link

* 상위(부모) 객체와의 참조를 이어주는 링크
* 자바스크립트에서 상속을 구현하고자 하는 경우 사용

## Prototype Chain

* 객체에서 메소드나 프로퍼티에 접근하려고 하는 경우 접근하고자 하는 메소드나 프로퍼티가 없으면 \__proto__ 가 가리키는 링크를 따라가 상위(부모)의 메소드나 프로퍼티를 참조(상속) 할 수 있는 것

```js
function Guitar(){
  this.head = true;
  this.string = 6;
} 

Guitar.prototype.playing = function(){
  return '딩가 딩가';
}

var electric = new Guitar();
console.log(electric.playing()) // "딩가 딩가"
/*
  electric.__proto__ === Guitar.prototype
  Guitar.prototype 을 검색하여 playing() 을 가져옴
*/
```

# Prototype 정리

```js
function Guitar(){}

Guitar.prototype.head = true; 
Guitar.prototype.string = 6;

var electric = new Guitar();

console.log(electric.prototype === Guitar()) // true
console.log(electric.constructor === Guitar) // true
console.log(electric.__proto__ === Guitar.prototype) // true
console.log(electric.string === Guitar.prototype.string) // true
```

# 요약

![프로토타입 과정](/img/posts/javascript/prototype/prototype.png)
<small>출처 : https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67</small>

* **Prototype** : 자신을 만들어낸 객체의 원형
* **Prototype Object** : 자신을 원형으로 만들어질 다른 객체가 참조할 프로토타입 객체
* **Consturctor** : 선언한 생성자 함수 자체를 가리키는 객체
* **__proto__** : 선언한 생성자의 Prototype Object 를 가리키는 객체
* **Prototype Link** : 상위(부모) 객체와의 참조를 이어주는 링크
* **Prototype Chain** : 특정 메소드를 찾는 경우 \__proto__ 를 링크로 삼아서 상위 Prototype 까지 검색을 하여 값을 찾아내는 것

---

### 참고

[https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67](https://medium.com/@bluesh55/javascript-prototype-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-f8e67c286b67){:target="_blank"}   
