---
layout: post
title:  "[Javascript] defer 와 async"
categories: ['Javascript']
---

브라우저는 HTML을 파싱하는 중 스크립트 태그 `<script>...</script>` 를 만나면 HTML 파싱을 중단하고 스크립트 다운과 실행을 한 뒤에 다시 HTML 파싱을 재개하는데
이런 동작은 **스크립트가 DOM 요소에 접근이 불가능**하고 스크립트의 용량이 큰 경우 스크립트를 다운 및 실행을 기다려야 하므로 **스크립트 이후의 페이지 확인이 불가능**한 이슈가 생긴다.

해당 이슈를 해결하기 위해서 스크립트를 페이지 하단에 위치시키는 방법이 있다.


```html
<body>
    ...컨텐츠...
    
    <script src=""></script>
</body>
```
하지만 만약 HTML의 파일의 크기가 큰 경우 HTML의 파일을 다운받은 뒤에 스크립트를 다운받기 때문에 다운로드 속도가 매우 느려질 것이다.
이 문제를 해결하기 위해 defer와 async를 사용한다.

# defer

```html
<body>
    ...컨텐츠...
    
    <script defer src=""></script>
</body>
```

* 스크립트를 백그라운드에서 다운 (HTML 파싱이 멈추지 않음)
* 페이지 구성이 끝날 때까지 지연된다. (페이지 우선)
* DOMContentLoaded 이벤트 전에 실행된다.
* HTML 추가 순으로 실행된다.
  - 다운로는 동시에 되지만 실행은 추가 순으로 실행된다.
* 외부 스크립트에서만 속성이 유효하다.
* DOM과 스크립트의 실행 순서가 중요한 경우 사용


# async

```html
<body>
    ...컨텐츠...
    
    <script async src=""></script>
</body>
```
* 스크립트를 백그라운드에서 다운 (HTML 파싱이 멈추지 않음)
* 실행 시에는 HTML 파싱이 멈춘다.
* 페이지와 완전히 **<mark>독립적</mark>**으로 동작한다.
  - DOMContentLoaded 이벤트, 다른 스크립트, async 스크립트는 서로를 기다려주지 않는다.
  - 다운로드가 끝난 뒤 바로 실행되기 때문에 추가 순의 의미가 없다. (load-first order)
* 방문자 수 카운트나 광고 관련 스크립트같이 다른 스크립트에 의존하지 않는 독립적인 스크립트나 실행 순서가 중요하지 않은 경우에 사용


# 동적 스크립트

자바스크립트를 사용하여 스크립트를 추가하는 것

```js
let script = document.createElement('script');
script.src = "/example.js";
document.body.append(script);
```

* 기본적으로 async 스크립트처럼 행동한다. **(독립적)**
* async 값을 false로 하면 순서가 HTML 추가 순으로 실행된다.

```js
let script = document.createElement('script');
script.src = "/example.js";
script.async = false; // (*)
document.body.append(script);
```

## 요약
* **script** : 페이지 다운 중 스크립트를 만나면 페이지 다운이 중단되고, 스크립트 다운과 실행이 완료되면 다시 페이지 다운 재개
* **defer** : 페이지와 스크립트를 동시에 다운받은 뒤 페이지 다운이 완료되면 스크립트 실행
* **async** : 페이지와 스크립트를 동시에 다운받는 중 스크립트가 실행되면 페이지 다운이 중단되고 실행이 완료되면 다시 페이지 다운 재개 **(독립적)**

[해당 링크](https://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html#script){:target="_blank"}의 이미지가 defer와 async를 한눈에 이해하기 쉬운 것 같다.

## 출처 

[https://ko.javascript.info/script-async-defer](https://ko.javascript.info/script-async-defer){:target="_blank"}

