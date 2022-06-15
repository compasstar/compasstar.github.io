---
layout: post
title:  "[HTTP] 3.HTTP 메시지"
subtitle:   "HTTP 메시지"
categories: HTTP
tags: HTTP
comments: true
date: 2022-06-15 00:20:48
---

# HTTP

---

<b>HTTP (HyperText Transfer Protocol)</b>

- HTML, TEXT, Image, 영상, 파일 등 거의 모든 형태의 데이터를 전송할 수 있습니다
- HTTP/1.1 버전을 가장 많이 사용합니다
- HTTP/2, HTTP/3 버전도 사용하지만, 성능 개선 차원의 버전일 뿐이지 HTTP/1.1과 기능상으로는 거의 동일합니다
- HTTP/1.1과 HTTP/2는 TCP를, HTTP/3은 UDP를 사용합니다

<br><br>

# 1. 클라이언트 서버 구조

--- 

- 클라이언트는 서버에 요청을 하고 응답을 대기합니다
- 서버가 요청에 대한 결과를 만들어서 응답합니다

<br><br>

# 2. Stateless (무상태)

---

## Stateful (상태유지)
- 서버가 클라이언트의 정보를 저장합니다
- 클라이언트는 요청을 할 때, 모든 정보를 요청할 필요 없습니다. 그때 그때 추가되는 정보만 요청하면 됩니다
- 단점으로, 해당 클라이언트를 대할 때는 해당 서버가 기억을 하고 있기에 그 서버만 응답을 할 수 있습니다

## Stateless (무상태)
- 서버가 클라이언트의 상태를 보존하지 않습니다
- 클라이언트가 요청을 할 때마다 모든 정보를 전부 요청해야 합니다
- 클라이언트가 모든 정보를 요청하기 때문에, 특정 서버만 응답할 수 있는 것이 아니라 모든 서버가 응답할 수 있습니다. -> 클라이언트 요청이 많을 때 서버를 대거 투입할 수 있습니다
- <b>모든 것을 무상태로 설계할 수 있는 것은 아니지만, 상태 유지는 최소한만 사용하고 가능한 한 무상태로 설계해야 합니다</b>

<br><br>

# 3. 비연결성 (connectionless)

---

- HTTP는 기본이 연결을 유지하지 않는 모델입니다
- 서버는 클라이언트에게 응답을 하면 연결을 끊어버립니다
- 계속해서 연결을 유지한다면 서버 입장에서 처리가 어렵습니다.

### [한계와 극복]
- 연결을 계속해서 새로하기에 TCP/IP 연결을 새로 맺어야 합니다. -> 3 way handshake 시간이 많이 듭니다
- 웹 브라우저로 사이트를 요청하면 HTML, 자바스크립트, css, 추가 이미지 등 수많은 리소스들이 함께 다운로드 됩니다

### 극복
- 초기: <연결 -> HTML요청,응답 -> 종료> <연결 -> 자바스크립트요청,응답 -> 종료> <연결, 추가이미지요청,응답 -> 종료>
- 헌재: <연결 -> HTML요청,응답 / 자바스크립트요청,응답 / 추가이미지요청,응답 -> 종료>
- HTTP/2, HTTP/3 에서 더욱 최적화 되었습니다

<br><br>

# 4. HTTP 메시지

## 요청메시지

```
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

### 시작라인
```
GET /search?q=hello&hl=ko HTTP/1.1
```
- `method SP request-target SP HTTP-version CRLF` (SP = 공백, CRLF = 엔터)
- `method`(HTTP 메서드): GET, POST, PUT, DELETE ... -> 서버가 수행해야 할 동작 지정
- `request-target`(요청대상): absolute-path (절대경로)
<br><br>

### HTTP 헤더
```
Host: www.google.com
```
- `field-name":" OWS field-value OWS` (OWS = 띄어쓰기 허용)
- `field-name`은 대소문자 구분 없습니다 

<br><br>

## 응답메시지

```
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
  <body>...</body>
</html>
```
<br>

### 시작라인
```
HTTP/1.1 200 OK
```
- `HTTP-version SP status-code SP reason-phrase CRLF`
- `status-code`(HTTP 상태코드): 200 성공 / 400 클라이언트 요청 오류 / 500 서버 내부 오류
- `reason-phrase`(이유문구): 사람이 이해할 수 있도록 짧은 상태코드 설명 (200에 대한 설명 -> OK)
<br><br>

### HTTP 헤더
```
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
```
- HTTP 전송에 필요한 모든 부가정보
- 표준 헤더가 너무 많고, 필요시 임의의 헤더 추가 가능
<br><br>

### HTTP 메시지 바디
```
<html>
  <body>...</body>
</html>
```
- 실제 전송할 데이터
- HTML 문서, 이미지, 영상 등 byte로 표현할 수 있는 모든 데이터 전송 가능