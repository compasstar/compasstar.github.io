---
layout: post
title:  "[JAVA] 9. 예외처리"
subtitle:   "예외처리"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-17 00:22:34
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 1. try, catch, finally

***

```
Scanner scanner = new Scanner(System.in);
int i, j;
ArrayList<String> list = null;
		
int[] iArr = {0, 1, 2, 3, 4};
	
try {
	System.out.println("input i: ");
	i = scanner.nextInt();
	System.out.println("input j: ");
	j = scanner.nextInt();
			
	System.out.println("i / j = " + (i / j));
			
	for (int k=0;k < 5;k++) {
		System.out.println("iArr[" + k + "]: " + iArr[k]);
	}

	System.out.println("list.size(): " + list.size());

} catch (InputMismatchException e) {
	e.printStackTrace();
} catch (ArrayIndexOutOfBoundsException e) {
	e.printStackTrace();
} catch (Exception e) {
	e.printStackTrace();
} finally {
	System.out.println("예외 발생 여부와 상관없이 언제나 실행 됩니다");
}
```

- 우선 기본적으로 `try`를 실행합니다
- 예외(error)가 발생한다면 `catch`를 실행합니다.
- `catch()` 괄호 안의 내용은 에러의 종류입니다 (`Exception`은 모든 오류)
- `e.printStackTrace()`는 에러내용을 출력합니다
- `finally`는 에러 발생 여부와 상관없이 언제나 실행합니다

<br><br>

# 2. throws

***

## [MainClass004]
```
public class MainClass004 {
	
	public void firstMethod() throws Exception {
		secondMethod();
	}
	
	public void secondMethod() throws Exception {
		thirdMethod();
	}
	
	public void thirdMethod() throws Exception {
		System.out.println("10 / 0 = " + (10 / 0));
	}
}
```

## [MainClass]
```
MainClass004 mainClass004 = new MainClass004();
		
try {
	mainClass004.firstMethod();
} catch (Exception e) {
	// 에러 발생 목록 보여준다
	e.printStackTrace();
	System.out.println("error!");
}
```
- `throws`는 에러가 발생한다면 자신을 호출한 곳으로 되돌아갑니다<br><br>
- `MainClass`에서 `MainClass004`의 `firstMethod()`를 불러옵니다
- `firsthMethod()` -> `secondMethod()` -> `thirdMethod()` 순서로 차례로 불러오게 됩니다.
- 이때 `thirdMethod()`에서 (10 / 0) 으로 인해 에러가 발생합니다.<br><br>
- `throws`로 인해 `secondMethod()`로 되돌아갑니다
- `secondMethod()`에서 오류가 났으므로 `firstMethod()`로 `throws`합니다
- `firstMethod()`는 다시 `MainClass`로 되돌아 갑니다<br><br>
- `try`에서 오류가 났으므로 `catch`를 실행합니다.

<br>

## [실행콘솔]

```
java.lang.ArithmeticException: / by zero
	at exception.MainClass004.thirdMethod(MainClass004.java:14)
	at exception.MainClass004.secondMethod(MainClass004.java:10)
	at exception.MainClass004.firstMethod(MainClass004.java:6)
	at exception.MainClass.main(MainClass.java:71)
error!
```
- `e.printStackTrace()`가 발생한 에러 목록을 보여줍니다
- `error!`를 출력합니다
