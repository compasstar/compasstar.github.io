---
layout: post
title:  "[JAVA] 4. 익명 클래스"
subtitle:   "익명 클래스"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-16 00:21:48
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 익명 클래스

***

클래스 하나를 만들어주겠습니다.

```
public class AnonymousClass {
	
	public AnonymousClass() {
		System.out.println("AnonymousClass Constructor");
	}

	public void method() {
		System.out.println("-- AnonymousClass's method START --");
	}
}
```

해당 클래스를 사용하기 위해서는 `Main Class`에서 아래 코드와 같이 생성을 해야 합니다.

```
AnonymousClass anonymous = new AnonymousClass();
anonymous.method();
```
그러나 일회성으로만 함수를 사용하고 싶다면, 생성하는 과정을 거치지 않고, 바로 사용할 수 있습니다.

```
new AnonymousClass() {
	@Override
	public void method() {
		System.out.println("-- AnonymousClass's Override method START --");
	};
}.method();
```

- `new AnonymousClass` 로 생성 후, 변수에 저장하지 않습니다.<br> 바로 상속받아 (`@Override`) 함수를 사용합니다.<br>
- 보통 일회성으로 override해서 사용하는데 쓰입니다.
