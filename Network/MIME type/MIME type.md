# MIME type

## MIME 이란?

Multipurpose Internet Mail Extensions의 약어이며, 다목적 인터넷 메일 확장이란 뜻으로 이메일의 데이터 형식을 정의한 표준 포멧이다.

## MIME의 등장 배경

이메일은 7비트 ASCII 코드를 사용하여 데이터를 전송하기 때문에 plain text 데이터만 전송이 가능했고 이미지, 동영상, 오디오 등의 Binary 데이터를 전송하기에는 제약이 있었다. 기존의 이메일 전송 시스템을 그대로 사용하면서 Binary 데이터를 전송하기 위해서는 Binary 데이터를 plain text 데이터로 변환하고 이를 다시 ASCII로 변환하여 전송해야 했다. 여기서 Binary 데이터를 plain text 데이터로 변환하는 것을 인코딩(Encoding)이라 하고, 그 반대를 디코딩(Decoding)이라고 한다. 이렇게 인코딩한 본문 및 Binary 데이터는 송신하는 측에서 디코딩할 때 참고할 수 있도록 포맷을 명시해야 하는데, 이 포맷을 MIME이라고 한다.

Postman 앱이나 Chrome DevTool로 Request Header를 뜯어보면 Content-Type 항목이 있는데, 이것이 MIME type이다. 즉, 본문(Body)의 원래 데이터 형식을 나타내는 것이다.

[https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbpmdGA%2FbtqCQ365O0w%2FvEgOvKGHzLGK0eBARuxYR0%2Fimg.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FbpmdGA%2FbtqCQ365O0w%2FvEgOvKGHzLGK0eBARuxYR0%2Fimg.png)

다음은 대략적인 MIME type 사용 예시이다.

[https://t1.daumcdn.net/cfile/tistory/997B2D395A7078321D](https://t1.daumcdn.net/cfile/tistory/997B2D395A7078321D)

## MIME type 문법

`type/subtype`

MIME type의 구조는 `/`로 구분된 두 개의 문자열인 type과 subtype으로 구성된다. type에는 개별타입과 multipart 타입이 있으며, 다음과 같다.

[Untitled](MIME%20type%20a1f57edce3d6481992727dd9ccbc366e/Untitled%20Database%207d00a28d9f674d40b4627e649b7a801b.csv)

각 타입에 대한 서브타입의 상세한 내용은 다음의 링크를 참조하면 된다.

[MDN Web Docs](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)