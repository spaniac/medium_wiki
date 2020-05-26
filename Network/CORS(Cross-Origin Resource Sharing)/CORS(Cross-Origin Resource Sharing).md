# CORS(Cross-Origin Resource Sharing)

# CORS 개념

CORS는 Cross-Origin Resource Sharing의 약자로, Cross Domain이라고도 한다. 도메인 또는 포트가 다른 다른 서버의 자원을 요청하여 공유하는 기능을 말한다.

![CORS%20Cross%20Origin%20Resource%20Sharing%20ec90ad721d6b46e39fed3ab134c4001e/Untitled.png](CORS%20Cross%20Origin%20Resource%20Sharing%20ec90ad721d6b46e39fed3ab134c4001e/Untitled.png)

CORS 예시 1

쉽게 말해, www.a.com이라는 도메인을 가진 서버에서 [www.b.com](http://www.b.com) 등과 같은 다른 도메인을 가진 서버의 리소스를 요청하는 것을 말한다. 하지만 일반적으로 동일 출처 정책(Same-Origin Policy)에 의해  CORS 요청이 발생하면 보안 목적으로 차단한다.

> 동일 출처 정책(Same-Origin Policy)
불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 중요한 보안 방식입니다. 이것은 잠재적 악성 문서를 격리하여, 공격 경로를 줄이는데 도움이 됩니다.

— MDN Web Docs —

## 동일 출처 정책 기준

두 URL의 프로토콜, 포트(명시한 경우), 호스트가 모두 같아야 동일한 출처라고 판단한다.

[동일 출처 정책 기준](CORS%20Cross%20Origin%20Resource%20Sharing%20ec90ad721d6b46e39fed3ab134c4001e/Untitled%20879762a109444f3a8e1446bbe0cd7840.csv)

# CORS 요청 종류

HTTP 요청은 CORS를 위한 Cross-Site HTTP Requests 기능을 제공한다. HTTP를 이용한 CORS 요청에는 다음과 같은 종류가 있다.

- Simple / Preflight
- Credential / Non-Credential

브라우저가 요청 내용을 분석하여 3가지 방식 중 해당하는 방식으로 서버에 요청을 날리므로, 프로그래머가 목적에 맞는 방식을 선택하고 그 조건에 맞게 코딩해야 한다.

## Simple Request

아래의 3가지 조건을 모두 만족하면 Simple Request이다. 

- GET, HEAD, POST 중의 한 가지 방식을 사용해야 한다.
- POST 방식일 경우 Content-type이 아래 셋 중 하나여야 한다.
    - application/x-www-form-urlencoded
    - multipart/form-data
    - text/plain
- 커스텀 헤더를 전송하지 말아야 한다.

Simple Request는 서버에 1번 요청하고, 서버도 1번 회신하는 것으로 처리가 종료된다.

```yaml
GET /resources/public-data/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,\*/\*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,\*;q=0.7
Connection: keep-alive
Referer: http://foo.example/examples/access-control/simpleXSInvocation.html
Origin: http://foo.example

HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 00:23:53 GMT
Server: Apache/2.0.61
Access-Control-Allow-Origin: *
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
Transfer-Encoding: chunked
Content-Type: application/xml

[XML Data]
```

## Preflight Request

Simple Request 조건에 해당하지 않으면 브라우저는 Preflight Request 방식으로 요청한다. 조건은 다음과 같다.

- GET, HEAD, POST 외의 다른 방식으로도 요청 가능
- application/xml처럼 다른 Content-type으로 요청 가능
- 커스텀 헤더 사용 가능

Preflight Request는 예비 요청과 본 요청으로 나누어 전송한다.

먼저 서버에 예비 요청를 보내고(HTTP Method OPTION) 서버는 예비 요청에 대해 응답한다. 그 다음에 본 요청을 서버에 보내고 서버도 본 요청에 응답한다.

하지만, 예비 요청과 본 요청에 대한 서버 단의 응답을 서버 개발자가 서버 애플리케이션 내에서 구분하여 처리할 필요는 없다. 서버 개발자는 Response Header에 `Access-Control-` 계열의 데이터를 설정해주면 서버가 알아서 본 요청을 처리한다.

```yaml
OPTIONS /resources/post-here/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,\*/\*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,\*;q=0.7
Connection: keep-alive
Origin: http://foo.example
Access-Control-Request-Method: POST
Access-Control-Request-Headers: X-PINGOTHER

HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 01:15:39 GMT
Server: Apache/2.0.61 (Unix)
Access-Control-Allow-Origin: http://foo.example
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Allow-Headers: X-PINGOTHER
Access-Control-Max-Age: 1728000
Vary: Accept-Encoding
Content-Encoding: gzip
Content-Length: 0
Keep-Alive: timeout=2, max=100
Connection: Keep-Alive
Content-Type: text/plain

POST /resources/post-here/ HTTP/1.1
Host: bar.other
User-Agent: Mozilla/5.0 (Macintosh; U; Intel Mac OS X 10.5; en-US; rv:1.9.1b3pre) Gecko/20081130 Minefield/3.1b3pre
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,\*/\*;q=0.8
Accept-Language: en-us,en;q=0.5
Accept-Encoding: gzip,deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,\*;q=0.7
Connection: keep-alive
X-PINGOTHER: pingpong
Content-Type: text/xml; charset=UTF-8
Referer: http://foo.example/examples/preflightInvocation.html
Content-Length: 55
Origin: http://foo.example
Pragma: no-cache
Cache-Control: no-cache

<?xml version="1.0"?><person><name>Arun</name></person>

HTTP/1.1 200 OK
Date: Mon, 01 Dec 2008 01:15:40 GMT
Server: Apache/2.0.61 (Unix)
Access-Control-Allow-Origin: http://foo.example
Vary: Accept-Encoding
Content-Encoding: gzip
Content-Length: 235
Keep-Alive: timeout=2, max=99
Connection: Keep-Alive
Content-Type: text/plain

[Some GZIP'd payload]
```

## Request with Credential

HTTP Cookie와 HTTP Authentication 정보를 인식할 수 있게 해주는 요청. 클라이언트에서 Credential 옵션을 True로 지정하여 Credential 요청을 보낼 수 있다.

서버는 Response Header에 반드시 `Access-Control-Allow-Credentials: true`를 포함해야 하고, `Access-Control-Allow-Origin` 헤더의 값에는 `*`가 아닌 `[http://foo.origin](http://foo.origin과)`과 같은 구체적인 도메인을 명시해야 한다.

## Request without Credential

CORS 요청은 기본적으로 Non-Credential 요청이므로, 클라이언트에서 Credential 옵션을 별도로 지정하지 않으면 default로 Non-Credential 요청을 보낸다.

# CORS 관련 HTTP Headers

## Request Headers

클라이언트가 서버에서 CORS 요청을 보낼 때 사용하는 헤더로, 브라우저가 자동으로 지정하며, XMLHttpRequest를 사용하는 프론트엔드 개발자가 직접 지정할 필요는 없다.

### Origin

Cross-site 요청을 보내는 요청 도메인 URI을 나타내며, Access Control이 적용되는 모든 요청에 `Origin` 헤더는 반드시 포함된다.

```yaml
Origin: <origin>
```

`<origin>`은 서버 이름(포트 포함)만 포함되며, 경로 정보는 포함되지 않는다.

`<origin>`은 공백일 수도 있는데, 소스가 data URL일 경우에 유용하다.

### Access-Control-Request-Method

예비 요청을 보낼 때 포함되며, 본 요청에서 어떤 HTTP Method를 사용할 지 서버에게 알려준다.

```yaml
Access-Control-Request-Method: <method>
```

### Access-Control-Request-Headers

예비 요청을 보낼 때 포함되며, 본 요청에서 어떤 HTTP Header를 사용할 지 서버에게 알려준다.

```yaml
Access-Control-Request-Headers: <field-name>[, <field-name>]*
```

## Response Headers

서버에서 CORS 요청을 처리할 때 지정하는 헤더.

### Access-Control-Allow-Origin

Access-Control-Allow-Origin 헤더의 값으로 지정된 도메인으로부터의 요청에 대해서만 서버의 리소스에 접근을 허용한다.

```yaml
Access-Control-Allow-Origin: <origin> | *
```

### Access-Control-Expose-Headers

기본적으로 브라우저에게 노출이 되지 않지만, 브라우저 측에서 접근할 수 있게 허용해주는 헤더를 지정한다. 커스텀 헤더도 설정이 가능하다.

- Default로 브라우저에 노출되는 HTTP Response Header
    - Cache-Control
    - Content-Language
    - Content-Type
    - Expires
    - Last-Modified
    - Pragma

```yaml
Access-Control-Expose-Headers: Content-Length, X-My-Custom-Header, X-Another-Custom-Header
```

### Access-Control-Max-Age

Prefilght Request의 결과가 캐시에 유지할 시간을 설정한다.

```yaml
Access-Control-Max-Age: <delta-seconds>
```

### Access-Control-Allow-Credentials

Request with Credential 방식이 사용될 수 있는지를 지정한다.

```yaml
Access-Control-Allow-Credentials: true | false
```

### Access-Control-Allow-Methods

예비 요청에 대한 Response Header에 사용되며, 서버의 리소스에 접근할 수 있는 HTTP Method 방식을 지정한다.

```yaml
Access-Control-Allow-Methods: <method>[, <method>]*
```

### Access-Control-Allow-Headers

예비 요청에 대한 Response Header에 사용되며, 본 요청에서 사용할 수 있는 HTTP Header를 지정한다.

```yaml
Access-Control-Allow-Headers: <field-name>[, <field-name>]*
```

# 출처 및 참조

[교차 출처 리소스 공유 (CORS)](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)

[동일 출처 정책](https://developer.mozilla.org/ko/docs/Web/Security/Same-origin_policy)

[지긋지긋한 CORS 파헤쳐보자](https://velog.io/@jmkim87/%EC%A7%80%EA%B8%8B%EC%A7%80%EA%B8%8B%ED%95%9C-CORS-%ED%8C%8C%ED%97%A4%EC%B3%90%EB%B3%B4%EC%9E%90)

[CORS에 대한 간단한 고찰](https://velog.io/@wlsdud2194/cors)

[Cross Origin Resource Sharing - CORS](https://homoefficio.github.io/2015/07/21/Cross-Origin-Resource-Sharing/)