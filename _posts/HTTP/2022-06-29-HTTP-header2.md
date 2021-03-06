---
layout: post
title:  "[HTTP] 8. HTTP 헤더2"
subtitle:   "HTTP 헤더2"
categories: HTTP
tags: HTTP
comments: true
date: 2022-06-29 00:22:18
---



# 1. 캐시 기본 동작


<hr> 

## 캐시가 없을 때
- 데이터가 변경되지 않아도 계속 네트워크를 통해 데이터를 다운로드 받아야 한다
- 느린 사용자 경험

## 캐시 적용
- 캐시 가능 시간 동안은 네트워크를 사용하지 않아도 된다
- 빠른 사용자 경험

## 캐시 시간 초과
- 캐시 유효 시간을 초과하면, 서버를 통해 데이터를 다시 조회하고, 캐시를 갱신한다
- 다시 네트워크 다운로드 발생

<br><br>


<h1>검증 헤더와 조건부 요청</h1>

<hr>

## 캐시 시간 초과
- 캐시 유효 시간이 초과해서 서버에 다시 요청한다면 두 가지 상황 중 하나가 나타난다
  - 1. 서버에서 기존 데이터를 변경함
  - 2. 서버에서 기존 데이터를 변경하지 않음

- 캐시 만료 후에도 서버에서 데이터를 변경하지 않았다면, 저장해 두었던 캐시를 재사용할 수 있다
- 단, 클라이언트의 데이터와 서버의 데이터가 같다는 사실을 확인할 수 있는 방법 필요
<br><br>

## 검증 헤더와 조건부 요청
- 캐시 유효 시간이 초과해도, 서버의 데이터가 갱신되지 않는다면 `304 Not Modified` + 헤더 메타 정보만 응답한다 (바디는 없음)
- 클라이언트는 서버가 보낸 응답 헤더 정보로 캐시의 메타 정보를 갱신 (아하 데이터 재활용해도 되네?)
- 클라이언트는 캐시에 저장되어 있는 데이터 재활용
- 결과적으로 네트워크 다운로드가 발생하기는 하지만 헤더 정보만 다운로드 하기에 용량이 적다!!!



<br><br>

<h1>3. 검증 헤더와 조건부 요청2</h1>

<hr>

### 검증 헤더
- 캐시 데이터와 서버 데이터가 같은지 검증하는 데이터
- Last-Modified: 서버에서 마지막으로 변경한 시간과 캐시 데이터의 시간이 동일하다면 캐시 데이터 사용
- ETag

### 조건부 요청 헤더
- 검증 헤더로 조건에 따른 분기
- If-Modified-Since: Last-Modifed 사용
- If-None-Match: ETag 사용
- 조건이 만족하면 200 OK (데이터가 변경됨)
- 조건이 만족하지 않으면 304 Not Modified -> 너의 캐시로 리다이렉션 해라 (데이터가 수정 되지 않음)

## Last-Modifed, If-Modified-Since 단점
- 1초 미만 단위로 캐시 조정이 불가능 (날짜 기반의 로직을 사용하기 때문)
- 데이터를 수정해서 날짜가 다르지만, 같은 데이터를 수정해서 데이터 결과가 같을 수도 있음 (새로 다운로드 받을 필요가 없다)
- 서버에서 별도의 캐시 로직을 관리하고 싶은 경우 (예: 주석처럼 크게 영향이 없는 변경에서는 캐시를 유지하고 싶음)

## ETag, If-None-Match
- ETag (Entity Tag)
- 캐시용 데이터에 임의의 고유한 버전 이름을 달아둠 (v1.0)
- 데이터가 변경된다면 이 이름을 변경한다 (Hash를 다시 생성) (v1.0 -> aaaaa)
- ETag만 보내서 같으면 캐시데이터 유지, 다르다면 다시 데이터 받기
- 캐시 제어 로직을 서버에서 완전히 관리한다
- 클라이언트는 단순히 이 값을 서버에 제공한다 (클라이언트는 캐시 메커니즘을 모름)




<br><br>

<h1>4. 캐시와 조건부 요청 헤더</h1>

<hr>

## 캐시 제어 Cahche-Control
### 캐시 지시어 (directives)
- `Cache-Control: max-age`: 캐시 유효 시간, 초 단위
- `Cache-Control: no-cache`: 데이터는 캐시해도 되지만, 항상 원(origin) 서버에 검증하고 사용
- `Cache-Control: no-sotre`: 데이터에 민감한 정보가 있으므로 저장하면 안된다 (메모리에서 사용하고 최대한 빨리 삭제)


## Pragma
- `Pragma: no-cache`
- HTTP 1.0 하위호환 -> 사용하지 않음

## Expires
- 캐시 만료일을 정확한 날짜로 지정
- HTTP 1.0 부터 사용
- `Cache-Control: max-age`의 하위호환임 -> 사용하지 않음
<br><br>

## 검증 헤더와 조건부 요청 헤더

### 검증 헤더
- ETag: "v1.0"
- Last-Modified: Thu, 04 Jun 2020 07:19:24 GMT

### 조건부 요청 헤더
- If-Match, If-None-Mate (ETag)
- If-Modified-Since, If-Unmodified-Since (Last-Modified)

<br><br>


<h1>5. 프록시 캐시</h1>

<hr>

미국에 있는 원(origin) 서버까지 도달하려면 거리가 멀기 때문에 응답 시간이 너무 오래걸린다<br>
-> 한국 어딘가에 <u>프록시 캐시 서버</u>를 만든다<br>
-> 한국에서 사용하는 웹 브라우저는 원 서버에 직접 연결하는 것이 아니라, 한국에 있는 프록시 캐시 서버를 통해 데이터를 응답받는다<br>
-> 시간이 짧게 걸린다
<br><br>
여기서 "프록시 캐시 서버"를 "public 캐시"라고 하고, 우리가 사용하는 "웹 브라우저" 캐시를 "private 캐시"라고 한다

## Cach-Control
- `Cache-Control: public`: 응답이 public 캐시에 저장되어도 됨
- `Cache-Control: private`: 응답이 해당 사용자만을 위한 것임, private 캐시에 저장해야 함 (기본값) -> 프록시 서버에는 저장되지 않음
- `Cache-Control: s-maxage`: 프록시 캐시에만 적용되는 max-age
- `Age:60`(HTTP 헤더): 오리진 서버에서 응답 후 프록시 캐시 내에 머문 시간

<br><br>

<h1>6. 캐시 무효화</h1>

<hr>

## Cache-Control
- `Cache-Control: no-cache` : 데이터는 캐시해도 되지만, 항상 원 서버에 검증하고 사용!
- `Cahce-Control: no-store`: 데이터에 민감한 정보다 있으므로 저장하면 안됨 (메모리에서 사용하고 최대한 빨리 삭제)
- `Cache-Control: must-revalidate`: 
  - 캐시 만료 후 최초 조회 시 원 서버에 검증해야 함
  - 원 서버 접근 실패시 반드시 오류가 발생해야 함(504 Gateway Timeout)
  - 캐시 유효 시간이라면 캐시를 사용한다 
- `Pragma: no-cache`: HTTP 1.0 하위호환 -> 과거 HTTP 요청이 있을 수도 있기 때문
<br><br>
<b>이것들을 전부 넣어주면 확실하게 캐시 무효화 응답할 수 있다</b>

## no-cache vs must-revalidate
- `no-cache`는 원서버와 네트워크 단절 시, 프록시 캐시에서 응답을 한다면 그냥 캐시를 사용할 수도 있다 (설정에 따라)
- `must-revalidate`는 원서버와 네트워크 단절 시, 무조건 504 Gateway Timeout 을 띄운다