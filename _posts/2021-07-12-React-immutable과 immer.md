---
layout: post
title:  "immutable과 immer"
categories: ['React', 'Javascript']
---

# immutable와 immer

- 자바스크립트의 불변성을 유지할 때 간편하게 사용할 수 있는 라이브러리

## immutable

- [immutable 공식 문서](https://immutable-js.com/){:target="_blank"}
- Map, List, set, get, update, setIn, getIn, updateIn, toJS, Record 등을 사용한다.
- 일반 자바스크립트로 변환할 경우 `toJS()`를 사용한다
- 길이값은 length 대신 `size`를 사용한다.
- `isEmpty()`로 빈 값 여부를 boolean으로 확인할 수 있다. 

### 설치

```bash
npm i immutable
```

### Map

- 객체를 사용하는 경우 사용한다.
- 객체가 복잡한 경우 `fromJS()`를 사용해서 처리할 수도 있다.

```js
import { Map, fromJS } from 'immutable';

const obj1 = Map({
  foo: 1,
  inner: Map({
    bar: 10
  })
});

const obj2 = fromJS({
  foo: 1,
  inner: { // Map을 사용하지 않았음
    bar: 10
  }
});

console.log(obj1); // Map {foo: 1, inner: Map, constructor: Object}
console.log(obj2); // Map {foo: 1, inner: Map, constructor: Object}
console.log(obj1.toJS()) // {foo: 1, inner: Object}
console.log(obj.size) // 2
console.log(obj.isEmpty()) // false
```

### List

- 배열을 사용하는 경우 사용한다.

```js
import { List } from 'immutable';

const arr = List([
  Map({ foo: 1 }),
  Map({ bar: 2 }),
]);


console.log(arr); // List {size: 2, _origin: 0, _capacity: 2, _level: 5, _root: null…}
console.log(arr.toJS()); // [Object, Object]
console.log(arr.size) // 2
console.log(arr.isEmpty()) // false
```

### set

- 값을 설정하는 경우 사용한다.

```js
import { Map, List } from 'immutable';

const obj = Map({
  foo: 1,
  inner: Map({
    bar: 10
  })
});

const arr = List([
  Map({ foo: 1 }),
  Map({ bar: 2 }),
]);


const newObj = obj.set('foo',5)
const newArr = arr.set(0, 5)
console.log(newObj.toJS());  // {foo: 5, inner: Object}
console.log(newArr.toJS()); // [5, Object]
```

### get

- 값을 읽을 경우 사용한다.

```js
import { Map, List } from 'immutable';

const obj = Map({
  foo: 1,
  inner: Map({
    bar: 10
  })
});

const arr = List([
  Map({ foo: 1 }),
  Map({ bar: 2 }),
]);


console.log(obj.get('foo')); // 1
console.log(arr.get(1).toJS()); // { bar: 2 }
```

### update

- 값을 읽은 뒤 설정할 때 사용한다.

```js
import { Map, List } from 'immutable';

const obj = Map({
  foo: 1,
  inner: Map({
    bar: 10
  })
});

const arr = List([
  Map({ foo: 1 }),
  Map({ bar: 2 }),
]);


const newObj = obj.update('foo', value => value + 10 )
console.log(newObj.toJS()) // {foo: 11, inner: Object}
```

## setIn, getIn, updateIn

- 내부에 있는 값을 set, get, update하는 경우 사용한다.

```js
import { Map, List } from 'immutable';

const obj = Map({
  foo: 1,
  inner: Map({
    bar: 10
  })
});

const arr = List([
  Map({ foo: 1 }),
  Map({ bar: 2 }),
]);


const newObj = obj.setIn(['inner', 'bar'], 20)
console.log(newObj.toJS()) // {foo: 1, inner: { bar : 20 }}
console.log(newObj.getIn(['inner', 'bar'])) // 20
console.log(newObj.updateIn(["inner", "bar"], value => value + 5).toJS()) // {foo: 1, inner: { bar : 25 }}

const newArr = arr.setIn([0, 'foo'], 30)
console.log(newArr.toJS()) // [{foo : 30}, {bar: 2}]
console.log(newArr.getIn([0, 'foo'])) // 30
console.log(newArr.updateIn([0, "foo"], value => value + 10).toJS()); // [{foo : 40}, {bar: 2}]
```

### delete

- key값을 제거하는 경우 사용한다.

```js
import { Map, List } from 'immutable';

const obj = Map({
  foo: 1,
  inner: Map({
    bar: 10
  })
});

const arr = List([
  Map({ foo: 1 }),
  Map({ bar: 2 }),
]);


const newObj = obj.delete('foo');
console.log('newObj',newObj.toJS()) // {inner: Object}

const newArr = arr.delete(0) 
console.log('newArr',newArr.toJS()) // [{bar: 2}]
```

### Record

- get이나 getIn을 사용하지 않고 값을 읽을 수 있다.
- 일반 객체의 값을 가져오는 방식으로 값을 가져올 수 있다. (obj.name)

```js
import { Record } from 'immutable';

const Person = Record({
  name: '홍길동',
  age: 1
});

let person = Person();

// (1)
console.log(person.name) // 홍길동

// (2)
person = person.set('age', 5)
console.log(person.age) // 5
// person.name = '철수' (Error : Cannot set on an immutable record)

// (3)
person = Person({
  name: '영희',
  age: 10,
});
const { name, age } = person;
console.log(name, age) // 영희 10

// (4)
const dog = Record({
  name: '멍멍이',
  age: 1,
  foo: Record({
    bar: true
  })() // (*)
})() // (*)
console.log(dog.name) // 멍멍이
console.log(dog.foo.bar) // true
```

## immer.js

- [immer 공식 문서](https://immerjs.github.io/immer/){:target="_blank"}
- immutable.js보다 더욱 간편하게 사용할 수 있다.
- 자바스크립트의 [Proxy](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Proxy){:target="_blank"}기능을 사용한다. 

### 설치

```bash
npm i immer
```

### produce

- immer를 사용하기 위해서 보통 produce라는 이름으로 불러온다.
- produce함수의 첫 번째 인자에는 기존의 객체를, 두 번째 인자에는 업데이트를 실행하는 함수가 들어간다.

```js
import produce from "immer";

const memo = [
  { idx: 1, title: "제목 1", isTrash: false },
  { idx: 2, title: "제목 2", isTrash: true }
];

// 읽기
console.log(memo[0].idx); // 1

// 추가
const addMemo = produce(memo, (draft) => {
  draft.push({
    idx: 3,
    title: "제목 3",
    isTrash: true
  });
});
console.log(addMemo[2]); // {idx: 3, title: "제목 3", isTrash: true}

// 수정
const updateMemo = produce(memo, (draft) => {
  draft[1].title = "제목 변경!";
});
console.log(updateMemo[1].title); // 제목 변경!

// 삭제
const deleteMemo = produce(memo, (draft) => {
  draft.pop();
});
console.log(deleteMemo); // [{idx: 1, title: "제목 1", isTrash: false}]
```


### 기타

- 자바스크립트, 특히 리액트에서는 불변성이 매우 중요하기 때문에 유지해주어야 한다. 
- 간단한 불변성 처리라면 ES6기능으로 처리하는 것이 좋다.

---

### 참고

[https://immutable-js.com/](https://immutable-js.com/){:target="_blank"}   
[https://immerjs.github.io/immer/](https://immerjs.github.io/immer/){:target="_blank"}   
[https://velopert.com/3486](https://velopert.com/3486){:target="_blank"}   
[https://react.vlpt.us/basic/23-immer.html](https://react.vlpt.us/basic/23-immer.html){:target="_blank"}