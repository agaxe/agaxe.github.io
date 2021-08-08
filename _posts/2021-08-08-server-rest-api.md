---
layout: post
title:  "REST API"
categories: ['Server']
---

# REST 정의

Representational State Transfer 의 약자로 <mark>자원을 이름으로 구분하여 해당 자원의 상태를 주고받는 모든 것</mark>을 의미한다.

# REST 구성

* <mark>자원 (RESOURCE)</mark> - URI
* <mark>행위 (Verb)</mark> - HTTP Method
* <mark>표현 (Representations)</mark>

# REST 특징

<p/>
### 1. Uniform Interface (유니폼 인터페이스)
- URI 에서 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.

## 2. Stateless (무상태성)
- 세션 정보나 쿠키 정보에 대한 상태정보가 없다.

## 3. Cacheable (캐시 가능)
- HTTP 프로토콜을 따르기 때문에 HTTP 프로토콜의 캐시기능을 사용할 수 있다. (Last-Modified, E-Tag)

## 4. Self-descriptiveness (자체 표현 구조)
- REST API 메시지만 보고 바로 이해 할 수 있는 자체 표현 구조이다.

## 5. Server - Client 구조
- Server 는 API,  Client 는 사용자 인증이나 컨텍스트를 관리하여 서로 간의 의존성이 줄어든다.

## 6. Layered System (계층형 구조)
- 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 한다.

# REST 장점

1. HTTP 프로토콜의 인프라를 따르기 때문에 REST API 를 사용하기 위해 별도의 인프라를 구축할 필요가 없다.
2. HTTP 프로토콜을 따르는 여러 가지 플랫폼에서 사용할 수 있다.
3. 의도하는 메시지가 명확하다.
4. 서버와 클라이언트의 역할이 명확하게 분리된다.


# REST 단점 

1. 표준이 없다.
2. HTTP Method 의 개수가 제한적이다.
3. 구형 브라우저에서 원활하게 동작하지 않는 경우가 있다.


# REST API

<mark>REST 를 기반으로 서비스 API 를 구현한 것</mark>

* API : Application Programming Interface 의 약자로 데이터와 기능의 집합을 제공하여 컴퓨터 프로그램간 상호작용을 촉진하며, 서로 정보를 교환 가능 하도록 하는 것

# RESTful API?

REST API 를 제공하는 웹 서비스를 지칭하는 용어


## REST API 디자인 가이드

1. URI는 정보의 자원을 표현해야 한다.
2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE) 를 사용하여 표현한다.

```bash
GET /members/delete/1 (x)
DELETE /members/1 (o)
```
* URI 에 정보의 자원이 아닌 행위가 들어있기 때문에 1번에 부적절하다.
* HTTP Method 표현하고자 하는 행위와 맞지 않기 때문에 2번에 부적절하다.

# HTTP Method 의 종류

* GET : 리소스를 <mark>조회</mark>하는 경우 사용
* POST : 새로운 리소스를 <mark>추가</mark>하는 경우 사용
* PUT : 리소스를 <mark>모두 수정</mark>하는 경우 사용
* PATCH : 리소스를 <mark>일부 수정</mark>하는 경우 사용
* DELETE : 리소스를 <mark>삭제</mark>하는 경우 사용

## URI 설계 시 주의사항

1. 슬래시(/) 구분자는 계층 관계를 나타내는 경우에만 사용한다.
2. 마지막은 슬래시(/)를 포함하지 않는다.
3. 하이픈(-)은 가독성을 높이는 경우 사용한다.
4. 언더바(-)는 사용하지 않는다.
5. URI 경로에 대문자는 적합하지 않다.
6. 파일 확장자는 URI 에 포함하지 않는다.

## Colllection과 Document

* 컬렉션 (Colllection) : 문서들의 집합, 객체들의 집합
* 도큐먼트 (Document) : 문서, 한 객체

```bash
http://restapi.example.com/sports/soccer
```
* sports 은 컬렉션이다. (컬렉션은 복수 명사를 사용)
* soccer 는 도큐먼트이다.


# HTTP 응답 코드

## 2xx
* 200 : 클라이언트의 요청을 <mark>정상적으로 수행</mark>한 경우
* 201 : 클라이언트가 리소스 생성을 요청하여 <mark>생성을 정상적으로 수행</mark>한 경우

## 4xx
* 400 : 클라이언트의 <mark>요청이 부적절</mark>한 경우
* 401 : 클라이언트가 <mark>인증되지 않는 상태에서 요청</mark>한 경우
* 403 : <mark>응답하고 싶지 않는 리소스를 요청</mark>하는 경우
* 405 : <mark>요청한 리소스의 Method 가 리소스에서</mark> 사용이 불가능한 경우

## 3xx
* 301 :  <mark>요청한 리소스에 대한 URI가 변경</mark>되었을 때 사용하는

## 5xx
* 500 :  <mark>서버에 문제가 생긴 경우</mark> 사용


## 출처

* [https://meetup.toast.com/posts/92](https://meetup.toast.com/posts/92){:target="_blank"}
* [https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html){:target="_blank"}



