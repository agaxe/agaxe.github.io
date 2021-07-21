---
layout: post
title:  "SOP & CORS"
categories: ['Server']
---

# SOP
- 동일 출처 정책 (same-origin policy)
- **어떤 출처에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 중요한 보안 방식**
- 동일한 출처끼리만 자원에 접근할 수 있는 보안 방식
- 여기서 출처는 Protocol(http://) 과 Host(localhost:8000) 이다.
- XMLHttpRequest 와 Fetch API 는 동일 출처 정책을 따른다.
- CORS 를 사용해 접근을 허용할 수 있다.

## 예제
```js
/**
http://localhost:8000 => http://localhost:8000  = same origin

http://localhost:8000 => http://localhost:2000  = cross origin  
http://localhost:8000 => http://weather.com     = cross origin 
**/
```


# CORS 
- 교차 출처 리소스 공유 (Cross-Origin Resource Sharing)
- **추가 HTTP 헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을 부여하도록 브라우저에 알려주는 체제**


# CORS 이슈 해결 방법

## 서버
1. 헤더에 Access-Control-Allow-Origin 설정

```js
app.use((req,res, next) => {
    res.header("Access-Control-Allow-Origin", "*");                     // 모든 도메인
    res.header("Access-Control-Allow-Origin", "https://foo.example");   // 특정 도메인
})
```

2. Node.js 의 [CORS 미들웨어](https://www.npmjs.com/package/cors){:target="_blank"} 사용 

```js
var express = require('express')
var cors = require('cors')
var app = express()

// 모든 도메인 접근 허용  
app.use(cors())

app.get('/products/:id', function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for all origins!'})
})


// 특정 도메인 접근 허용   
var corsOptions = {
  origin: 'https://foo.example',
  optionsSuccessStatus: 200
}
 
app.get('/products/:id', cors(corsOptions), function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for only example.com.'})
})
```


## 클라이언트 

### Proxy
- 클라이언트가 다른 네트워크에 간접적으로 접속할 수 있게 해주는 역할
- 간단하지만, 속도가 느리다는 단점이 있다.

1. cors-anywhere 
    ```js
    // 'https://cors-anywhere.herokuapp.com/https://foo.example/'
    ```

2. Webpack Dev Server (개발 환경)
    ```js
    // webpack.config.js
    module.exports = {
        devServer: {
            proxy: {
            '/api': 'http://localhost:8000'
            }
        }
    };
    ```

---

### 참고

[https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy){:target="_blank"}   
[https://developer.mozilla.org/ko/docs/Web/HTTP/CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS){:target="_blank"}   
[https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%EC%84%9C%EB%B2%84](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%EC%84%9C%EB%B2%84)
[https://velog.io/@yejinh/CORS-4tk536f0db](https://velog.io/@yejinh/CORS-4tk536f0db)
