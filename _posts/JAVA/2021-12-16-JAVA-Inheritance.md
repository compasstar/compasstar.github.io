---
layout: post
title:  "[JAVA] 3. 자바 상속"
subtitle:   "자바 상속"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-16 00:21:39
---

인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 상속

***

```
public class ParentClass {
	
	int openYear = 1995;
	
	public ParentClass() {
		System.out.println("ParentClass constuctor");
	}
	
	public void parentFun() {
		System.out.println("parentFun()");
	}
	
	// 만일 접근자를 private으로 한다면, childClass에서 사용불가
	private void privateFun() {
		System.out.println("privateFun()");
	}
	
	public void makeJJajang() {
		System.out.println("-- makeJJajang() --");
	}

}
```

부모 클래스를 만들었습니다. 이제 `Child Class`를 만들어 상속받을 것입니다.

<br>

```
public class ChildClass extends ParentClass {
	
	// 하나의 클래스에 하나만 상속 가능
	
	int openYear = 2000;
	
	public ChildClass() {
		System.out.println("ChildClass constructor");
	}

	public void childFun() {
		System.out.println("childFun()");
	}
	
	@Override
	public void makeJJajang() {
		System.out.println("-- more makeJJajang() --");
	}
	
	public void getOpenYear() {
		System.out.println("ChildClass's Open year: " + this.openYear);
		System.out.println("ParentClass's Open year: " + super.openYear);
	}
}
```

- 상속 받는 클래스에는 `extends` + `상속받는 클래스 이름`을 적어줍니다. (한번에 하나만 상속 받을 수 있습니다)
- 상속을 받은 함수 위에는 `@Override`를 적어줍니다.
- `super`는 부모를 지칭합니다. <br>
>  `this.openYear` 는 `ChildClass` 에서 찾으므로 2000을 가리키고, `super.openYear` 는 `ParentClass`에서 찾으므로 1995를 가리킵니다.
- 변수에 커서를 가리키고 `Ctrl + T`를 누르면 상속관계를 확인할 수 있습니다.

<br><br>
