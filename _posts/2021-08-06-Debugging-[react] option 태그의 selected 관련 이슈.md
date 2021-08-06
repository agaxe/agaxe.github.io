---
layout: post
title:  "[react] option 태그의 selected 관련 이슈"
categories: ['Debugging','React']
---

# 상황

- select 태그의 option 을 반복문을 통해 렌더링하려는 상황
- 새로 고침 시 특정 값(ex. query string) 의 option 에 selected 를 적용하려고 하던 중 에러 발생

<em style="color:red">
  Warning: Use the defaultValue or value props on \<select> instead of setting selected on \<option>.
</em>

# 해결

option 태그의 selected 를 제거하고 select 태그에 defaultValue 를 추가했다.


```jsx
// before

const viewCount = 5;
const viewCountList = [5, 10, 20, 50].map((v) => ({ value: v, text: `${v}개씩 보기` }));

...
return (
  <Select {...props}>
    {viewCountList.length &&
      viewCountList.map((v, i) => (
        <option selected={v.value === viewCount} key={i} value={v.value}>
          {v.text}
        </option>
      ))}
  </Select>
);
...
```

```jsx
// after

const viewCount = 5;
const viewCountList = [5, 10, 20, 50].map((v) => ({ value: v, text: `${v}개씩 보기` }));
const initSelect = viewCountList[0].value; // 5

...
return (
  <Select {...props} defaultValue={initSelect}> {/** defaultValue 추가 */}
    {viewCountList.length &&
      viewCountList.map((v, i) => (
        <option key={i} value={v.value}>
          {v.text}
        </option>
      ))}
  </Select>
);
...
```

---

### 참고

[https://stackoverflow.com/a/44787318](https://stackoverflow.com/a/44787318){:target="_blank"}   