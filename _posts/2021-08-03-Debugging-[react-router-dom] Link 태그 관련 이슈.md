---
layout: post
title:  "[react-router-dom] Link 태그 관련 이슈"
categories: ['Debugging','React']
---

# 상황

특정 데이터의 리스트를 만들기 위해 리스트에 react-router-dom 의 Link 태그를 적용하고 그 안에 있는 수정 버튼에도  Link 태그를 적용하는 상황에서 해당 에러가 발생하였다.

<em style="color:red">
  Warning: validateDOMNesting(...): \<a> cannot appear as a descendant of \<a>
</em>

# 해결

구글링으로 찾아보니 Link 태그 안에 Link 태그를 추가적으로 사용해서 발생한 이슈인 것 같아 자식 Link 를 제거하고 useHistory() 를 사용하여 처리하였다.

```jsx
// before
...
return(
  <Link to="/POST_KEY">
    <Link to="/POST_KEY/write">news<Link>
  </Link>
)

```

```jsx
// after
...
const history = useHistory();

function movePage(pathname){
  history.push(pathname)
}

return(
  <Link to="/POST_KEY">
    <button onClick={() => movePage('/POST_KEY/write')}>news<button>
  </Link>
)

```

---

### 참고

[https://stackoverflow.com/a/66410125](https://stackoverflow.com/a/66410125){:target="_blank"}   