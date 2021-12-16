---
layout: post
title:  "[JAVA] 5. 인터페이스와 추상클래스"
subtitle:   "인터페이스와 추상클래스"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-16 00:21:54
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 1. 인터페이스

***

인터페이스는 클래스와 비슷한 개념입니다. 그러나 직접 기능을 구현하지 않고, 껍데기만 만들어놓고 상속받아 기능을 채워놓는 방식입니다. <br>
예시로 보겠습니다.

## [interface InterfaceA]
```
public interface InterfaceA {

	// Interface에서는 선언 불가
	// 작업명세서(껍데기)만 만들고, Interface Class 에서 무엇을 할지 선언
	public void funA();
}
```
`InterfaceA`를 만들었습니다. (`class`대신 `interface`라고 적습니다) <br>
`funA()`처럼 함수를 만들기만 하고, 기능을 넣지는 않습니다. 

## [interface InterfaceB]
```
public interface InterfaceB {
	public void funB();
}
```
`InterfaceB`도 만들었습니다. <br><br>

## [class InterfaceClass implements InterfaceA, InterfaceB]
```
public class InterfaceClass implements InterfaceA, InterfaceB {

	public InterfaceClass() {
		System.out.println(" --Interfaceclass constructor --");
	}
	
	@Override
	public void funA() {
		System.out.println(" -- funA() -- ");
	}
	
	@Override
	public void funB() {
		System.out.println(" --funB()-- ");
	}
}
```

- `InterfaceClass` 클래스를 만들었습니다. 
  >상속받을 때 사용했던 `extends`와 달리, `implements`를 적어줍니다. <br>여기서는 복수의 인터페이스를 가져올 수 있습니다.
- `InterfaceA` `InterfaceB`에서 가져온 `funA` `funB` 를 Override하여 기능을 불어넣어 줍니다.
<br><br>


## [MainClass]
```
public class MainClass {
	public static void main(String[] args) {
		InterfaceA ia = new InterfaceClass();
		InterfaceB ib = new InterfaceClass();
		 
		ia.funA();
		ib.funB();
	}
}
```
- 메인클래스에서는 다음과 같이 생성하여 사용하시면 됩니다.


<br><br>

# 2. 인터페이스의 사용 예시

## [interface Toy]
```
public interface Toy {
	
	public void walk();
	public void run();
	public void alarm();
	public void light();
}
```
- `Toy` 인터페이스를 만듭니다. 기능은 없습니다.

## [class ToyAirplane implements Toy]
```
public class ToyAirplane implements Toy {

	@Override
	public void walk() {
		System.out.println("The airplane can not walk.");
	}

	@Override
	public void run() {
		System.out.println("The airplane can not run.");
	}

	@Override
	public void alarm() {
		System.out.println("The airplane has alarm function.");
	}

	@Override
	public void light() {
		System.out.println("The airplane has no light function.");	
	}
}
```
`ToyAirplane` 클래스를 만들어 `Toy` 의 기능을 불어넣어 줍니다.

## [class ToyRobot implements Toy]
```
public class ToyRobot implements Toy {

	@Override
	public void walk() {
		System.out.println("The airplane can walk.");
	}

	@Override
	public void run() {
		System.out.println("The airplane can run.");
	}

	@Override
	public void alarm() {
		System.out.println("The airplane has no alarm function.");
	}

	@Override
	public void light() {
		System.out.println("The airplane has light function.");
	}
}
```
- `ToyRobot` 클래스를 만들어 `Toy` 의 기능을 불어넣어 줍니다.
- `ToyAirplane`과 동일하게 가져왔지만, 다른 기능을 넣어줍니다.
- `Toy`라는 공통적인 인터페이스가 있고, 장난감마다 다른 기능을 불어준다고 이해하면 되겠습니다.
<br><br>


## [MainClass]
```
public class MainClass {

	public static void main(String[] args) {
		
		Toy robot = new ToyRobot();
		Toy airplane = new ToyAirplane();
		
		Toy toys[] = {robot, airplane};
		
		for (int i=0;i<toys.length;i++) {
			toys[i].walk();
			toys[i].run();
			toys[i].alarm();
			toys[i].light();
		}
	}
}
```
- `MainClass` 에서 사용

<br><br>


# 3. 추상클래스

## [abstract class Bank]
```
public abstract class Bank {
	
	String name;
	String account;
	int totalAcount;
	
	public Bank() {
		System.out.println("Bank constructor");
	}
	
	public Bank(String name, String account, int totalAcount) {
		System.out.println("Bank counstructor");
		
		this.name = name;
		this.account = account;
		this.totalAcount = totalAcount;
	}
	
	// 예금
	public void deposit() {
		System.out.println(" -- deposit() START --");
	}
	
	// 출금
	public void withdraw() {
		System.out.println(" --withdraw() START --");
	}
	
	// 적금
	public abstract void installmentSavings();
	
	// 해약
	public abstract void cancellation();
	
	// 정보출력
	public void getInfo() {
		System.out.printf("name: %s\n", name);
		System.out.printf("account: %s\n", account);
		System.out.printf("totalAcount: %s\n", totalAcount);
	}
}
```

- 클래스를 생성할 때 앞에 `abstract`를 붙여줍니다.
- Interface와 달리 껍데기만 만들어 놓은 것도 있고, 실제로 기능이 있는 것도 있습니다.
> String name; String account; int totalAccount; <br>
> 변수들을 값은 넣지 않고, 생성만 했습니다.<br>
> 추상클래스를 상속받아 다른 클래스에서 값을 넣어줄 것입니다. <br><br>
> 예금, 출금, 정보출력은 기능이 구현되어 있고, 적금과 해약은 기능이 없습니다. <br>
> 추상클래스를 상속받아 다른 클래스에서 기능을 구현할 것입니다.

<br><br>

## [class MyBank extends bank]
```
public class MyBank extends Bank {
	
	public MyBank(String name, String account, int totalAcount) {
		super(name, account, totalAcount);
	}
	
	@Override
	public void installmentSavings() {
		System.out.println(" -- installmentSavings() START -- ");
	}
	
	@Override
	public void cancellation() {
		System.out.println(" -- cancellation() START --");
	}
}
```
- `MyBank` 클래스를 만들어 추상클래스를 상속받았습니다.
- 기능이 구현되지 않았던 적금과 해약을 Override받아 기능을 만들어 줍니다.
<br><br>

## [MainClass]
```
public class MainClass {

	public static void main(String[] args) {
		
		Bank myBank = new MyBank("박찬호", "123-4567-8901", 10000);
		
		myBank.deposit();
		myBank.withdraw();
		myBank.installmentSavings();
		myBank.cancellation();

		myBank.getInfo();
	}
}
```
- `MainClass`에서 생성하여 기능을 사용해줍니다.