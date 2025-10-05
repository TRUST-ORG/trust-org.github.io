---
title: HTTP Requests
published: 2025-10-02
author: Lanzarote
description: 'HTTP 요청에 대해서 알아봅시다'
image: './img/HTTP_logo.svg'
tags: ['Web', 'Network']
category: 'Web'
draft: false
---

# What is HTTP?

HTTP는 HTML과 같은 Hypermedia documents를 전송하기 위한 [Application-layer protocol](https://en.wikipedia.org/wiki/OSI_model)이다. 
웹 브라우저와 웹 서버 간의 통신과 API 등 다양한 용도로 사용된다.
이 게시글에는 간단하게 HTTP 요청에 대해서 알아본다.

# Structure of an HTTP Request

HTTP 요청은 다음과 같은 구조로 이루어져 있다.

```
POST /users HTTP/1.1
Host: example.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 49

name=FirstName+LastName&email=bsmth%40example.com
```
HTTP의 줄바꿈은 무조건 `CRLF`(`\r\n`)를 사용해야 한다. 
이유로는 각 운영체제마다 줄바꿈 문자가 다르기 때문이다. 
예를 들어, Unix 계열 운영체제는 `LF`(`\n`)를 사용하고, Windows는 `CRLF`(`\r\n`)를 사용한다.
HTTP 프로토콜은 이러한 차이를 없애기 위해 표준으로 `CRLF`를 채택했다.

가장 위에 있는 줄은 **Request Line**이라고 불리며, 세 부분으로 나뉜다.
```
<method> <request-target> <protocol>
```
- **Method**: 요청의 종류를 나타낸다. 예를 들어, `GET`, `POST`, `PUT`, `DELETE` 등이 있다.
- **Request Target**: 요청하는 리소스의 경로를 나타낸다.
- **Protocol**: 사용되는 프로토콜과 버전을 나타낸다. 

그 다음 줄들은 **Headers**라고 불리며, 요청에 대한 추가 정보를 제공한다. 각 헤더는 `Key: Value` 형식으로 작성된다. 한 헤더는 무조건 한 줄에 작성되어야 한다. 헤더는 대소문자 구분을 하지 않는다.

일반적인 헤더는 다음과 같다.
- `Host`: 요청하는 서버의 도메인 이름을 나타낸다.
- `Content-Type`: 요청 본문의 데이터 형식을 나타낸다.
- `Content-Length`: 요청 본문의 길이를 바이트 단위로 나타낸다.

마지막으로, 빈 줄 다음에는 **Body**가 있다. Body는 `PATCH`, `POST`, `PUT`의 Method만 사용할 수 있으며, 요청에 포함될 데이터를 담고 있다.

# Request Line

## Request Methods
Request Methods는 요청의 목적과 요청이 성공했을 때 어떤 값을 예상하는지 나타내기 위해 HTTP에서 정의한 일련의 메서드이다.

- **GET**: 서버에서 리소스를 가져온다. 요청 본문이 없어야 하며, 데이터 조회에 사용된다.
- **HEAD**: GET과 동일하지만, 응답 본문이 없다. 리소스의 메타데이터를 확인하는 데 사용된다.
- **POST**: 서버에 데이터를 제출한다. 요청 본문에 데이터를 포함하며, 리소스 생성이나 데이터 처리에 사용된다.
- **PUT**: 지정된 리소스를 요청 본문의 데이터로 대체한다.
- **DELETE**: 지정된 리소스를 삭제한다.
- **CONNECT**: 대상 리소스에 대한 터널을 설정한다.
- **OPTIONS**: 대상 리소스에 대한 통신 옵션을 설명한다.
- **TRACE**: 대상 리소스까지의 경로를 따라 메시지 루프백 테스트를 수행한다.
- **PATCH**: 리소스에 대한 부분적인 수정을 적용한다.

이 Method를 전부 다 알 필요는 없고, 주로 사용하는 `GET`, `POST`, `PUT`, `DELETE` 정도만 알아도 충분하다.

| Method   | Safe | Idempotent | Cacheable   | Body |
|----------|------|------------|-------------|------|
| GET      | Yes  | Yes        | Yes         | No   |
| POST     | No   | No         | Conditional | Yes  |
| PUT      | No   | Yes        | No          | Yes  |
| DELETE   | No   | Yes        | No          | No   |

- Safe: 서버의 상태를 변경하지 않는 메서드인지 여부
- Idempotent: 같은 요청을 여러 번 수행해도 결과가 동일한지 여부
- Cacheable: 응답이 캐시될 수 있는지 여부
- Body: 요청 본문에 데이터를 포함할 수 있는지 여부

## Request Target
Request Target은 다음과 같은 형태로 나타낼 수 있다.
- **Origin-form**: 가장 일반적인 형태로, 경로와 Query string으로 구성된다. `/path/resource?query=string`
- **Absolute-form**: 전체 URL을 포함한다. 주로 프록시 서버에 요청할 때 사용된다. `http://example.com/path/resource`
- **Authority-form**: 주로 CONNECT 메서드에서 사용되며, 호스트와 포트만 포함한다. `example.com:443`
- **Asterisk-form**: 서버 전체를 대상으로 하는 요청에 사용된다. `*`

# Header

## Content-Type
`Content-Type` 헤더는 request/response 본문의 데이터 형식을 나타낸다. 
이 헤더를 통해 서버는 클라이언트가 전송하는 데이터의 형식을 이해하고, 적절한 방식으로 처리할 수 있다.
또한 이 헤더로 클라이언트도 서버가 응답하는 데이터의 형식을 이해할 수 있게 된다.
```
Content-Type: <media-type>
```
media-type은 다음과 같은 형식을 가진다.
```
type/subtype; parameter=value
```
자주 쓰이는 media-type은 다음과 같다.
- `text/plain`: 일반 텍스트 데이터를 나타낸다.
- `text/html`: HTML 형식의 데이터를 나타낸다.
- `text/javascript`: JavaScript 형식의 데이터를 나타낸다.
- `application/json`: JSON 형식의 데이터를 나타낸다.
- `image/png`: PNG 이미지 데이터를 나타낸다.
- `image/jpeg`: JPEG 이미지 데이터를 나타낸다.
- `image/webp`: WebP 이미지 데이터를 나타낸다.
- `multipart/form-data`: 파일 업로드와 같은 복잡한 폼 데이터를 나타낸다.
- `multipart/byteranges`: 여러 부분으로 나뉜 데이터를 나타낸다.
- `application/x-www-form-urlencoded`: HTML 폼 데이터를 URL 인코딩 형식으로 나타낸다.

자세한 내용은 [Media types (MIME types) - HTTP | MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/MIME_types)에서 확인할 수 있다.

> 출처
>
> https://developer.mozilla.org/en-US/docs/Web/HTTP
