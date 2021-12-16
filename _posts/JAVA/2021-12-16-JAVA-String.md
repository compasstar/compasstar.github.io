---
layout: post
title:  "[JAVA] 7. 문자열 클래스 String"
subtitle:   "문자열 클래스 String"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-16 00:22:32
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 1. String

```
String str = new String("JAVA");
String str2 = "JAVA";
```
`String`은 원래 `new String()`을 통해 생성해 주어야 합니다.<br> 그러나 편의상 `String str = "JAVA"` 와 같이 생략해서 사용할 수 있습니다.

<br><br>

# 2. StringBuffer

```
StringBuffer sf = new StringBuffer("JAVA");

sf.append(" World");
System.out.println("sf: " + sf);
// sf: JAVA World

System.out.println("sf.length():" +sf.length());
// sf.length():10


sf.insert(sf.length(), "-----"); // 끝에 추가하겠다
System.out.println("sf: " + sf);
// sf: JAVA World-----
		
sf.delete(4, 8);
System.out.println("sf: " + sf);
// sf: JAVAld-----
```
- `StringBuffer`를 통해 문자열 클래스를 만들 수 있습니다.
- `.append(문자)` 문자를 문자열 끝에 추가합니다.
- `.length()` 문자열 길이
- `.insert(index, 문자)` 문자를 index 위치에 추가합니다.
- `.delete(4, 8)` 인덱스 4~8 사이를 지웁니다. 

<br><br>

# 3. StringBuilder

```
StringBuilder sb = new StringBuilder("JAVA World!!");
```
- `StringBuilder` 도 `StringBuffer`와 동일한 기능을 합니다.
- `StringBuilder`는 상대적으로 조금 더 빠르고, `StringBuffer`는 상대적으로 조금 더 안정적입니다.