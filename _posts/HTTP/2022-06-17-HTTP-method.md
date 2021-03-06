---
layout: post
title:  "[HTTP] 4. HTTP 메서드"
subtitle:   "HTTP 메서드"
categories: HTTP
tags: HTTP
comments: true
date: 2022-06-17 00:17:25
---



# 1. HTTP API

<hr> 

## API URI 고민
<b>가장 중요한 것은 리소스 식별!</b> <br>
리소스와 행위는 구분해야 한다! <br>

[예시]<br>
- <b>회원</b> 목록 조회 /members<br>
- <b>회원</b> 조회 /members/{id}<br>
- <b>회원</b> 등록 /members/{id}<br>
- <b>회원</b> 수정 /members/{id}<br>
- <b>회원</b> 삭제 /members/{id}<br>

리소스: 회원 / 행위: 조회, 등록, 삭제, 변경 <br>
리소스는 명사, 행위는 동사 <br>
행위 = 메서드


<br><br>


<h1>2. HTTP 메서드 - GET, POST, PUT, PATCH, DELETE</h1>


<hr>


[주요 메서드]<br>
- GET: 리소스 조회<br>
- POST: 요청 데이터 처리, 주로 등록에 사용<br>
- PUT: 리소스를 대체, 해당 리소스가 없으면 생성<br>
- PATCH: 리소스 부분 변경<br>
- DELETE: 리소스 제거<br>
<br>

[기타 메서드]
- HEAD: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환<br>
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명<br>

<br><br>

<h2>2-1. GET</h2>

```
GET /search?q=hello&hl=ko HTTP/1.1
```

- <b>리소스 조회</b>
- 서버에 전달하고 싶은 데이터는 query를 통해서 전달<br>
- 메시지 바디를 사용하여 데이터를 전달할 수 있지만, 지원하지 않는 곳이 많아서 권장하지는 않음<br>

<br>

<h2>2-2. POST</h2>

```
POST /members HTTP/1.1
```

- 요청 데이터 처리<br>
- <b>메시지 바디를 통해 서버로 요청 데이터 전달</b><br>
- 서버는 요청 데이터를 처리<br>
  - 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다<br>
- 주로 전달된 데이터로 신규 리소스 등록, 프로세스 처리에 사용<br>
- 해당 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지 리소스마다 따로 정해야 한다 (메시지 게시, 새 리소스 생성, 기존 자원에 데이터 추가 등) -> 정해진 것이 없다!<br>

[정리]<br>
1. 새 리소스 생성(등록)<br>
2. 요청 데이터 처리: 데이터를 생성하거나 변경하는 것을 넘어 프로세스를 처리해야 하는 경우 (배달시작 -> 배달완료)<br>
3. 다른 메서드로 처리하기 애매한 경우(사실 POST는 모든 기능을 수행할 수 있다. 그러나 각자에 맞는 역할을 수행하는 것이 유리하다.)<br>

<br>

<h2>2-3. PUT</h2>

```
PUT /members/100 HTTP/1.1
```

- 기존 리소스를 완전히 대체 (없으면 생성 [덮어쓰기])<br>
- 클라이언트가 리소스를 식별: 클라이언트가 리소스 위치를 알고 URI 지정 (POST와의 차이점임)
<br><br>

<h2>2-4. PATCH</h2>

```
PATCH /members/100 HTTP/1.1
```

- 리소스 부분 변경
  
<br><br>

<h2>2-5. DELETE</h2>

```
DELETE /members/100 HTTP/1.1
```

- 리소스 제거

<br><br>

<h1>3. HTTP 메서드의 속성</h1>

<hr>

<h2>3-1. 안전 (Safe)</h2>
- 호출해도 리소스를 변경하지 않는다<br>
- 안전 메서드: GET<br>
<br><br>

<h2>3-2. 멱등 (Idempotent)</h2>
- f(f(x)) = f(x)<br>
- 한 번 호출하든 두 번 호출하든 100번 호출하든 결과가 똑같다<br>
- 멱등 메서드: GET, PUT, DELETE<br>
- POST, PATCH는 멱등 메서드가 아니다! (PATCH는 `age += 1` 와 같은 개념임)<br>
- 활용: 자동 복구 메커니즘 -> 서버가 TIMEOUT 등으로 정상 응답을 못주었을 때, 클라이언트가 같은 요청을 다시 해도 되는가? 판단 근거
<br><br>

<h2>3-3. 캐시가능 (Cacheable)</h2>
- 응답 결과 리소스를 캐시해서 사용해도 되는가?<br>
- 캐시가능 메서드: GET, HEAD, POST, PATCH<br>
- 실제로는 GET, HEAD 정도만 캐시로 이용 (POST, PATCH는 본문 내용까지 캐시 키로 고려해야 하는데, 구현이 쉽지 않음)
