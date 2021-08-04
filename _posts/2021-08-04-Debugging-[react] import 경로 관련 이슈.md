---
layout: post
title:  "[react] import 경로 관련 이슈"
categories: ['Debugging','React']
---

# 상황

컴포넌트를 나누는 작업을 진행 중 vscode 와 브라우저의 콘솔창에 해당 이슈가 발생했다.

<em style="color:red">
  There are multiple modules with names that only differ in casing.
</em>

# 해결

import 의 경로를 대소문자를 구분하여 작성하였다.


---

### 참고

[https://stackoverflow.com/a/54183343](https://stackoverflow.com/a/54183343){:target="_blank"}   