# REST API

---

# REST?

REST는 REpresentational State Transfer의 약자로 자원과 자원에 대한 행위를 표현하도록 설계하는 아키텍처다.

# REST의 구성

REST는 다음과 같이 구성된다.

- 자원(Resource) → URI(Uniformed Resource Identifier)
- 행위(Verb) → HTTP Method
- 자원과 행위를 표현(Representations)

---

# REST의 특징

1. Uniform: 획일화된 인터페이스
Uniform Interface는 URI로 지정한 리소스에 대한 조작을 통일되고 한정적인 인터페이스로 수행하는 아키텍처 스타일이다.
2. Stateless: 무상태성
REST는 작업을 위한 상태 정보를 따로 저장하고 관리하지 않는다. 서버 측의 세션 정보나 클라이언트 측의 쿠키 정보를 별도로 저장하고 관리하지 않기 때문에 API 서버는 요청에만 집중할 수 있다. 이로 인해 서비스의 자유도가 높아지고 서버에서 불필요한 정보를 관리하지 않음으로써 API 구현이 단순해진다.
3. Cacheable: 캐시 가능
REST의 가장 큰 장점 중 하나는 HTTP라는 기존 웹 표준을 그대로 사용하기 때문에 웹에서 사용하는 기존 HTTP 인프라를 그대로 활용할 수 있다. 그래서 HTTP가 제공하는 캐싱 기능을 적용할 수 있다. HTTP 프로토콜 표준에서 사용하는 Last-Modified 또는 E-Tag를 이용하면 캐싱을 구현할 수 있으며, HTTP Message Header에서 확인이 가능하다.
4. Self-descriptiveness: 자체 표현 구조
REST의 또 다른 큰 특징 중 하나는 REST API 메세지만 확인해도 쉽게 이해할 수 있는 자체 표현 구조로 되어 있다는 것이다.
5. Client - Server 구조
REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(상태 정보 → 세션, 로그인 정보) 등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로 간 의존성이 줄어든다.
6. Hierarchical: 계층형 구조
REST 서버는 다중 계층으로 구성될 수 있으며, 보안, 로드 밸런싱, 암호화 계층을 추가해 구조 상의 유연성을 둘 수 있고, Proxy, Gateway와 같은 네트워크 기반의 중간 매체를 사용할 수 있게 합니다.

---

# REST API 디자인 가이드

## REST API 디자인 핵심 규칙

1. URI는 정보의 자원을 표현해야 한다.

    URI에는 행위에 대한 단어를 사용하지 않는다. URI는 자원을 표현하는데 중점을 두어야 한다.

2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다.

```
# 잘못된 예시
GET /users/delete/1

# 올바르게 수정한 예시
DELETE /users/1
```

```
# 예시

# 유저의 정보를 가져오는 URI
GET /users/retrieve/1     (X)
GET /users/1              (O)

# 유저를 추가하는 URI
GET /users/create/2       (X)
POST /users/              (O)
```

## URI 설계 시 주의할 점

1. 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용

    ```
    http://restapi.example.com/houses/apartments
    http://restapi.example.com/animals/mammals/whales
    ```

2. URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며, URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다. REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.

    ```
    http://restapi.example.com/houses/apartments/ (X)
    http://restapi.example.com/houses/apartments  (0)
    ```

3. 하이픈(-)은 URI 가독성을 높이는데 사용한다.
URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높인다.
4. 밑줄(_)은 URI에 사용하지 않는다.
글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 한다. 이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하여 가독성을 높이는 것이 좋다.
5. URI 경로에는 소문자가 적합하다.
URI 경로에 대문자 사용은 피하는 것이 좋은데, 대소문자에 따라 다른 리소스로 인식하게 되기 때문이다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정한다.

    ```
    RFC 3986 is the URI (Unified Resource Identifier) Syntax document
    ```

6. 파일 확장자는 URI에 포함시키지 않는다.
REST API에서는 HTTP Message Body의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다. Accept header를 사용하는 것을 권장한다.

    ```
    http://restapi.example.com/members/soccer/345/photo.jpg (X)

    GET /members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
    ```

## 리소스 간의 관계를 표현하는 방법

REST 리소스 간에는 연관 관계가 있을 수 있고, 이런 경우 다음과 같은 표현 방법을 사용한다.

```
/리소스명/리소스 ID/관계가 있는 다른 리소스명

ex) GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
```

만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있다. 예를 들어 사용자가 ‘좋아하는’ 디바이스 목록을 표현해야 할 경우 다음과 같은 형태로 사용할 수 있다.

```
GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)
```

## 자원을 표현하는 Collection과 Document

Collection과 Document에 대해 알면 URI 설계가 한 층 더 쉬워진다. Document는 단순히 문서로 이해해도 되고, 한 객체라고 이해하셔도 될 것 같습니다. Collection은 문서들의 집합, 객체들의 집합이라고 생각하시면 이해하시는데 좀더 편하실 것 같습니다. Document와 Collection은 모두 자원으로서 표현할 수 있으며 URI에 표현이 가능하다.

```
http://restapi.example.com/sports/soccer
```

위 URI를 보시면 sports라는 컬렉션과 soccer라는 도큐먼트로 표현되고 있다고 생각하면 됩니다. 좀 더 예를 들어보자면

```
http://restapi.example.com/sports/soccer/players/13
```

sports, players 컬렉션과 soccer, 13(13번인 선수)를 의미하는 도큐먼트로 URI가 구성된다. 여기서 중요한 점은 Collection을 **복수**로 사용하고 있다는 점이다. 좀 더 직관적인 REST API를 위해서는 Collection과 Document를 사용할 때 단수/복수도 구분한다면 더 이해하기 쉬운 URI를 설계할 수 있다.

# 출처

[REST API 제대로 알고 사용하기 : TOAST Meetup](https://meetup.toast.com/posts/92)