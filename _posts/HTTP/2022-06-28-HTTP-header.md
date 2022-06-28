---
layout: post
title:  "[HTTP] 7. HTTP 헤더1"
subtitle:   "HTTP 헤더"
categories: HTTP
tags: HTTP
comments: true
date: 2022-06-28 00:22:20
---



# 1. HTTP 헤더


<hr> 

```
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
```

- HTTP 전송에 필요한 모든 부가정보
- 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언틑, 서버 정보, 캐시 관리 정보 등
- 표준 헤더가 너무 많고, 필요시 임의의 헤더 추가 가능


<br><br>


<h1>2. HTTP BODY</h1>

<hr>

```
// 표현 헤더
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

// 표현 데이터
<html>
  <body>...</body>
</html>
```

- 메시지 본문을 통해 표현 데이터 전달
- 메시지 본문 = 페이로드(payload)
- 표현은 요청이나 응답에서 전달할 실제 데이터
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공 (데이터 유형 html, json, 데이터 길이, 압축 정보 등)


<br><br>

<h1>3. 표현</h1>

<hr>

- Content-Type: 표현 데이터의 형식
- Content-Encoding: 표현 데이터의 압축 방식
- Content-Language: 표현 데이터의 자연 언어
- Content-Length:표현 데이터의 길이

<b>표현 헤더는 전송, 응답 둘다 사용</b>

## 3-1. Content-Type
- 표현 데이터의 형식 설명
- 미디어 타입, 문자 인코딩
- 예) `text/html; charset=utf-8` `application/json` `image/png`
  
## 3-2. Content-Encoding
- 표현 데이터를 압출하기 위해 사용
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- 예) `gzip` `deflate` `identity`

## 3-3. Content-language
- 표현 데이터의 자연 언어를 표현
- 예) `ko` `en` `en-US`

## 3-4. Content-Length
- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용한다면 Content-Length를 사용하면 안됨 (이미 들어있음)


<br><br>

<h1>4. 협상 Content negotiation</h1>

<hr>

### 클라이언트가 선호하는 표현 요청
- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어

<b>협상 헤더는 요청시에만 사용!</b><br>
안될 수도 있지만 가능한 한 요청하는 것임!
<br><br>

## 협상과 우선순위1

```
GET /event
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
```

- Quality Values(q) 값 사용
- 0~1, 클수록 높은 우선순위
- 생략하면 1 (위의 예시에서 ko-KR은 q가 생략되어 있기에 1을 나타내고 있음)
- `ko-KR` > `ko` > `en-US` > `en`

## 협상과 우선순위2

```
GET /event
Accept: text/*, text/plain, text/plain;format=flowed, */*
```

- 구체적인 것이 우선한다
- `text/plain;format=flowed` > `text/plain` > `text/*` > `*/*`


<br><br>

<h1>5. 전송 방식</h1>

<hr>

- 단순 전송: Content-Length로 받아서 길이만큼 HTTP BODY에서 전송한다
- 압축 전송: 압축하여 전송한다 (Content-Encoding으로 어떤 형식으로 압축되었는지 알려주어야 한다)
- 분할 전송: `Transfer-Encoding: chunked` 을 붙여준다. 크기(바이트)를 설정하여 HTTP BODY를 해당 크기만큼 잘라서 바로바로 보낸다. (한꺼번에 보내지는 것이 아니다)
- 범위 전송: 범위를 설정하여 보낸다 `Content-Range: bytes 1001-2000 / 2000`

<br><br>

<h1>6. 일반 정보</h1>

<hr>

## 6-1. From
- 유저 에이전트의 이메일 정보
- 일반적으로는 잘 사용되지 않음
- 검색 엔진 같은 곳에서 주로 사용
- 요청에서 사용

## 6-2. Referer
- 현재 요청된 페이지의 이전 웹 페이지 주소
- A -> B로 이동하는 경우 B를 요청할 때 Referer: A를 포함해서 요청
- 유입 경로 분석 가능
- 요청에서 사용

## 6-3. User-Agent

```
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.193 Safari/537.36
```

- 유저 에이전트 애플리케이션 정보
- 클라이언트의 애플리케이션 정보 (웹 브라우저 정보 등)
- 통계 정보 뽑기 좋다
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- 요청에서 사용

## 6-4. Server
- 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
- `Server: Apache/2.2.22 (Debian)`
- `server: nginx`
- 응답에서 사용

## 6-5. Date
- 메시지가 발생한 날짜와 시간
- `Date: Tue, 15 Nov 1994 08:12:31 GMT`
- 응답에서 사용


<br><br>

<h1>7. 특별한 정보</h1>

<hr>

## 7-1. Host
- 요청한 호스트 정보(도메인)
- 요청에서 사용
- 필수!!!
- 하나의 서버가 여러 도메인을 처리해야 할 때
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때 호스트(도메인)를 구분한다

## 7-2. Location
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동 (리다이렉트)
- 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI를 나타낸다

## 7-3. Allow
- 허용 가능한 HTTP 메서드
- 405 (Method Not Allowed) 에서 응답에 포함해야 함
- `Allow: GET, HEAD, PUT`

## 7-4. Retry-After
- 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
- `Retry-After: Fri, 31 Dec 1999 23:59:59 GMT` (날짜 표기)
- `Retry-After: 120` (초단위 표기)

<br><br>

<h1>8. 인증</h1>

<hr>

### Authorization
- 클라이언트 인증 정보를 서버에 전달

### WWW-Authenticate
- 리소스 접근 시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용
- `WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple"`

<br><br>

<h1>9. 쿠키</h1>

<hr>

- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

만일 쿠키가 없다면, 모든 요청에 사용자 정보가 포함되도록 개발해야 함

쿠키는 모든 요청에 쿠키 정보 자동으로 포함한다

## 쿠키

```
set-cookie: sessionId=abcde 1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domian=.goolge.com; Secure
```
- 사용처
  - 사용자 로그인 세션 관리 
  - 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
  - 네트워크 트래픽 추가 유발
  - 최소한의 정보만 사용 (세션 id, 인증 토큰)
  - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지 참고
- 주의!
  - 보안에 민감한 데이터는 저장하면 안됨 (주민번호, 신용카드 번호 등)


## 9-1. 쿠키 - 생명주기
- `Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT`
  - 만료일이 되면 쿠키 삭제
- `Set-Cookie: max-age=3600` (3600초)
  - 0이나 음수를 지정하면 쿠키 삭제
- 세션 쿠키: 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속 쿠키: 만료 날짜를 입력하면 해당 날짜까지 유지

## 9-2. 쿠키 - 도메인

`domain=example.org`

- 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
  - `domain=example.org`를 지정해서 쿠키 생성 (`example.org` 와 함께 `dev.example.org`도 쿠키 접근)
- 생략: 현재 문서 기준 도메인만 적용
  - `example.org` 에서 쿠키를 생성하고 domain 지정을 생략 (`example.org` 에서만 쿠키 접근, `dev.example.org` 는 쿠키 미접근)

## 9-3. 쿠키 - 경로

`path=/home`
- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 `path=/` 루트로 지정
  
## 9-4. 쿠키 - 보안
- Secure
  - 쿠키는 http, https를 원래는 구분하지 않는데, Secure를 적용한다면 https인 경우에만 전송한다
- HttpOnly
  - XSS 공격 방지
  - 자바스크립트에서 접근 불가
  - HTTP 전송에만 사용
- SameSite
  - XSRF 공격 방지
  - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우에만 쿠키 전송






