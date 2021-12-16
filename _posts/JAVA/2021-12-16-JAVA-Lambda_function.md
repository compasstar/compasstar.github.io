---
layout: post
title:  "[JAVA] 6. 람다함수"
subtitle:   "람다함수"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-16 00:22:25
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 람다함수

우선 인터페이스들을 만들어주겠습니다.

```
public interface LambdaInterface1 {
	public void method(String s1, String s2, String s3);
}
```

```
public interface LambdaInterface2 {
	public int method(int x, int y);
}
```

```
public interface LambdaInterface3 {
	public void method();
}
```

```
public class MainClass {

	public static void main(String[] args) {

		LambdaInterface1 li1 = (String s1, String s2, String s3) -> { System.out.println(s1 + " " + s2 + " " + s3); };
		li1.method("Hello", "Java", "World"); 
		
		LambdaInterface2 li2 = (x, y) -> {
			int result = x + y;
			return result;
		};
		System.out.printf("%d", li2.method(2, 3)); // 5
		
		// 매개변수가 없을 때 ()만 작성한다
		LambdaInterface3 li3 = () -> {System.out.println("내용 없음");};
		li3.method();	
	}
}
```
- 람다함수는 매개변수와 실행문 만으로 작성합니다. `() -> {}`
