---
layout: post
title:  "[JAVA] 2. 자바 객체"
subtitle:   "자바 객체"
categories: JAVA
tags: JAVA
comments: true
date: 2021-11-18 00:15:56
---

# 자바 객체

인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 1. 자바의 구조

***

<br>

<img width="300" src="https://user-images.githubusercontent.com/55419868/142367537-27347e2b-6388-464a-b395-cdf277657aa1.JPG">

<img width="300" src="https://user-images.githubusercontent.com/55419868/142367544-8675e69d-41dd-4db2-b68c-1048d890a0ba.JPG">

패키지(objectedOrientedProgramming) <br>
-> 클래스 (MainClass.java) <br>
-> 함수 (main) <br>

순서로 담겨있습니다. 함수는 하나하나의 기능이라고 할 수 있고, 클래스는 하나의 객체, 패키지는 객체들을 모아놓은 것이라고 할 수 있겠습니다. <br><br>
자전거를 예로 들면, 자전거 하나는 <b>클래스</b>에 해당합니다. 자전거가 앞으로 나아간다거나, 속력을 줄인다거나 하는 것은 <b>함수</b>에 해당됩니다. <br>
객체는 자전거 외에도 여러가지가 있을 것입니다. 자동차나, 자판기, 혹은 키보드가 있을 수도 있습니다. 이렇게 객체들을 모아놓은 것을 <b>패키지</b>라고 할 수 있겠습니다.


이 중에서 메인클래스와 메인함수를 주목해야 합니다. <br>
메인은 프로그램을 실행시키면 제일 먼저 자동으로 실행됩니다. <br> 그러므로, 다른 클래스들을 만들어 객체를 생성한 후, 메인클래스와 메인함수에서 그들을 이용하여 프로그램을 작동시키면 됩니다.

<br><br>


# 2. 클래스와 생성자

***


```
package objectedOrientedProgramming;

public class Bicycle {
	
	public String color;
	public int price;
	
	public Bicycle(String c, int p) {
		System.out.println("Bycyle constructor - II ");
		color = c;
		price = p;
	}
	
	public void info() {
		System.out.println("-- info() -- ");
		System.out.println("color: " + color);
		System.out.println("price: " + price);
	}

}
```
자전거 class를 만들었습니다. 자전거의 속성으로 `color`, `price`를 만들어줍니다. 그리고, 함수를 만듭니다. `info()`는 자전거의 `color`, `price`를 출력합니다. <br>

`public Bicycle(String c, int p)`를 주목해봅시다. `class`의 이름과 함수의 이름이 같습니다. 이를 생성자라고 합니다. 생성자는 메인함수에서 해당 클래스를 불러올 때, 자동으로 실행되는 함수입니다. 위의 생성자는 `color`, `price`를 설정하는 역할을 합니다. 메인 클래스를 보겠습니다.

```
package objectedOrientedProgramming;

public class MainClass {
	
	public static void main(String[] args) {

		Bicycle myBicycle = new Bicycle("red", 100);
		myBicycle.info();
	}
}
```
메인함수에서 `Bicycle` 클래스를 불러옵니다. `Bicycle("red", 100)`과 생성자를 함께 주목해주세요. <br> 생성자에서 첫번째 변수는 `color`를 설정하고, 두번째 변수는 `price`를 설정하고 있었습니다. <br>그러므로 `info()`함수를 불러보면, 아래의 결과를 출력하실 수 있습니다.

```
Bycyle constructor - II 
-- info() -- 
color: yellow
price: 100
```

<br><br>

# 3. public, private, static

***

변수, 함수, 클래스를 만들 때 앞에 이를 공유하는 범위를 설정하는 명령어가 들어갑니다. `public`, `private`, `static` 입니다. <br>
`public`은 자유롭게 다른 클래스에서도 접근할 수 있습니다. <br>
`private`는 다른 클래스에서 접근할 수 없습니다. <br>

```
EmployeeBank parkBank = new EmployeeBank("박찬호");
parkBank.money = 10000;
```
예를들어, 위처럼 `money`를 정의하는 코드는 `money`가 `public`이라면 가능하지만, `private`에서는 가능하지 않습니다.<br>
다음은 `static` 을 알아보겠습니다.
<br><br>

```
package objectedOrientedProgramming;

public class EmployeeBank {
	
	String name;
	static int amount = 0;
	
	public EmployeeBank(String name) {
		this.name = name;
	}
	
	public void saveMoney(int money) {
		amount += money;
		System.out.println("amount: "+ amount);
	}
	
	public void spendMoney(int money) {
		amount -= money;
		System.out.println("amount: "+ amount);
	}
	
	public void getBankInfo() {
		System.out.println("Employ name: "+ this.name);
		System.out.println("amount: " + amount);
	}

}
```
은행 클래스를 만들고, 입금과 출금 기능을 만들었습니다. 그리고 남은 금액을 확인할 수 있습니다. 여기서 `amount` 변수가 `static` 범위라는 것을 기억해주세요.


```
EmployeeBank parkBank = new EmployeeBank("박찬호");
		parkBank.saveMoney(100);
		
		EmployeeBank leeBank = new EmployeeBank("이승엽");
		leeBank.saveMoney(300);
		
		leeBank.getBankInfo(); // amount: 400
		
		parkBank.spendMoney(400);
		
		leeBank.getBankInfo(); // amount: 0
```
`parkBank`, `leeBank`로 각각 클래스를 생성했습니다. 그리고 `parkBank`에 100, `leeBank`에 300 만큼 입금했습니다. <br><br> `leeBank`에서 `getBankInfo()` 를 통해 남은 금액을 확인했더니, 400이라는 결과가 나왔습니다. 분명 `leeBank`에서는 300만 입금했는데, 숫자가 다릅니다. <br><br>
`static` 은 클래스를 여러개 생성해도, 값을 공유합니다. <br>`leeBank`에서 `amount`를 조절하든, `parkBank`에서 조절하든 동일한 `amount`가 조절됩니다. 그러므로 마지막에 `parkBank`에서 400을 사용했는데, `leeBank`에서 0이 남게 된 것입니다. 
<br><br>

# 4. getter, setter

```
private String name;
private int score;
```
`private`로 변수를 만들었습니다. 이는 외부에서 접근할 수 없습니다. 그러나, 이를 우회해서 외부에서 접근하기 위해 `getter, setter`를 사용합니다. <br>이클립스의 코드를 적는 곳에서 우클릭 후, Source -> Generate Getters and Setters 를 클릭합니다.


![getter](https://user-images.githubusercontent.com/55419868/142635288-e4542973-0f70-4ae7-b2b6-948751ca5faf.JPG)

```
package objectedOrientedProgramming;

public class Student {
	
	private String name;
	private int score;
	
	public Student(String n, int s) {
		this.name = n;
		this.score = s;
	}
	
	public void getInfo() {
		System.out.println(" -- getInfo() -- ");
		System.out.println(" name: " + name);
		System.out.println(" socore: " + score);
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getScore() {
		return score;
	}

	public void setScore(int score) {
		this.score = score;
	}
}
```
아래 4개의 함수가 생성됩니다. `getName()`, `setName()`, `getScore()`, `setScore()` <br>
(`Student()`, `getInfo()`는 직접 타이핑한 것입니다)

```
Student student1 = new Student("홍길동",  90);
student1.getInfo(); // name: 홍길동 score: 90
		
student1.setScore(100);
student1.getInfo(); // name: 홍길동 score: 100
```
이제 메인클래스에서 `get` 과 `set` 을 통해 접근할 수 있습니다.