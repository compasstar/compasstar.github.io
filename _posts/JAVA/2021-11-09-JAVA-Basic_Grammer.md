---
layout: post
title:  "[JAVA] 1. 자바 기본문법"
subtitle:   "자바 기본문법"
categories: JAVA
tags: JAVA
comments: true
date: 2021-11-09 00:18:15
---

# 자바 기본 문법

인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 1. 기본 자료형
<br>

```
package BasicGrammer;

public class MainClass {
	
	public static void main(String[] args) {

	}
}
```
자바의 기본적인 구조입니다. <br>
package > class > main(함수) 순서로 들어있어서 간단하게는 main 함수 안에서 작업합니다. <br>
코드가 복잡해지면 여러 함수를 사용하고, 외부에서 클래스를 가져와서 사용할 수도 있습니다. <br><br>
앞으로 나오는 코드들은 main 함수 안에 적었습니다.

<br><br>

```
int i = 10;
		
float f = 10.123f;

double d = 10.123;

char c = 'c';
		
String s = "Hello Java World!!!!";

boolean b = false;	
```

`byte`, `short`, `int`, `long`
> 정수를 담는 자료형으로 위 순서대로 더 큰 수를 담을 수 있습니다. <br>
> 주로 `int`를 사용합니다.

`float`, `double` 
> 실수를 저장하는 자료형입니다.  <br>
> `float`는 숫자 뒤에 `f`를 붙인다는 특징이 있습니다.

`char`, `String`
> 문자를 저장하는 자료형입니다. <br>
> `char`는 단일문자, `String`은 ''안의 모든 문자를 저장합니다.

`boolean`
> `true` `false` 참 거짓을 저장하는 자료형입니다.

<br><br>

# 2. 특수문자와 서식문자

## [특수문자]

```
// 주석입니다

/*
길게 주석을 달고 싶으면 위아래 /* */ 표시를 해줍니다
*/
```

```
System.out.println("Good\tMorning~");
System.out.println("Good\n\nMorning~");
System.out.println("Good\'Morning~\'");
System.out.println("Good\"Morning~\"");
```

```
/*
Good	Morning~
Good

Morning~
Good'Morning~'
Good"Morning~"
*/
```


- `\t` -> Tab
- `\n` -> 줄바꿈
- `\'` -> 작은따옴표
- `\"` -> 큰따옴표

<br>

## [서식문자]

```
System.out.printf("오늘의 날씨는 %d도 입니다.\n", 8);
// 오늘의 날씨는 8도 입니다.

System.out.printf("소문자 \'%c\'의 대문자는 \'%c\'입니다.\n", 'a', 'A');
// 소문자 'a'의 대문자는 'A'입니다.

double d = 1.123456d;
System.out.printf("d = %f\n", d);
// d = 1.123456

// 정수만큼 오른쪽으로 간격을 띈다
System.out.printf("%5d \n", 123);
//    123
		
// 소수점제한
System.out.printf("%.2f \n", 1.22222);
// 1.22
```

- `%d` 정수, `%c` 단일문자, `%s` 문자열, `%f` 실수로 대체해서 사용할 수 있습니다. <br>
- `System.out.printf` 로 사용합니다.<br>
- 중간에 숫자를 넣어서 표시를 조절할 수 있습니다.

<br><br>

# 3. 연산자

산술 연산자
> `+`(덧셈), `-`(뺄셈), `*`(곱셈), `/`(나눗셈), `%`(나머지)

복합대입 연산자
> `x = x + 10` 을 `x += 10` 으로 줄여쓸 수 있습니다.<br>
> 다른 연산자들도 동일합니다. 

관계 연산자
> `>`, `<`, `>=`, `<=`, `==`(같다) `!=`(다르다)

증감 연산자
> `x++` 코드를 실행한 후, x에 1을 더합니다.<br>
> `++x` x에 1을 더한 후, 코드를 실행합니다.

논리 연산자
> `&&` (and), `||` (or), `!` (not)

삼항(조건) 연산자
> `c = (x > y) ? 'c1' : 'c2'` <br>
> 조건이 참이면 변수에 c1을 저장하고, 거짓이면 c2를 저장합니다.

<br><br>

# 4. 배열

```
int[] arr1 = new int[5];
arr1[0] = 100;

int[] arr2 = {10, 20, 30};
```
배열을 생성해주고, 인덱스를 통해 값을 넣어줍니다. <br>
혹은 처음부터 `{}`를 이용하여 배열을 만들 수 있습니다.

```
// 배열 길이 출력
System.out.println("arrAtt1.length: " + arrAtt1.length);
		
// 배열 요소 출력
System.out.println("arrAtt1: " + Arrays.toString(arrAtt1));
		
// 배열 요소 복사
arrAtt3 = Arrays.copyOf(arrAtt1, arrAtt1.length);
System.out.println("arrAtt3: " + Arrays.toString(arrAtt3));
		
// 배열 레퍼런스
arrAtt2 = arrAtt1;
System.out.println("arrAtt1: " + arrAtt1); // [I@123a439b
// 아예 주소값이 같다
System.out.println("arrAtt2: " + arrAtt2); // [I@123a439b
// copy 했기 때문에 주소값이 다르다
System.out.println("arrAtt3: " + arrAtt3); // [I@7de26db8
```

<b>주소값</b>
>`arrAtt2 = arrAtt1`과 같이 배열을 같다고 지정한다면, `arrAtt2`는 `arrAtt1`의 주소를 갖습니다. <br>
그 뜻은, `arrAtt1`을 수정한다면, `arrAtt2` 또한 함께 바뀐다는 뜻입니다. <br><br>
그렇기에 데이터만 복사해와 새로운 배열을 만들고 싶다면 `Arrays.copyOf(배열, 배열길이)` 를 사용해야 합니다. <br>
여기서 배열길이는 카피하고자 하는 배열의 길이와 동일할 필요는 없습니다. 더 길게 만들어서 새로운 데이터를 집어넣어도 괜찮습니다.

<br>

```
int[][] arrMul = new int[3][2];
		arrMul[0][0] = 10;
		arrMul[0][1] = 100;
```
다차원으로도 만들 수 있습니다.

<br><br>

# 5. 조건문

## [if문]

```
if(num1 < num2) {
			System.out.println("num1은 num2보다 작다");
} else if(num1 > num2) {
	System.out.println("num1은 num2보다 크다");
} else {
	System.out.println("num1과 num2는 같다");
}
```

## [switch문]

```
switch(score) {
case 100:
case 90:
	System.out.println("수");
	break;
		
case 80:
	System.out.println("우");
	break;
			
case 70:
	System.out.println("미");
	break;
			
default:
	System.out.println("try again!");
	break;
}
```
- `score`에 따라 실행이 달라집니다. <br>
- 어느 `case`에도 해당되지 않는다면 `default`를 실행합니다.
- `break`를 사용하지 않으면, 코드가 내려가면서 이미 조건이 실행되어도 또 다른 조건을 실행하게 됩니다.
- `case 100` `case 90`의 예시처럼, 두개의 case에 하나의 실행을 넣을 수도 있습니다. 100 또는 90 일때 '수'가 출력됩니다.

<br><br>


# 6. 반복문

## [for문]

```
for(int i=1 ; i<10 ; i++) {
	System.out.printf("%d * %d = %d", 3, i, (3*i));
}
// 3 6 9 12 15 18 21 24 27
```
구구단의 3단을 출력하는 반복문입니다. <br>
`for(변수초기화 ; 조건 ; 반복할때마다 변수의 조정)`<br>
`for(int i=1; i<10 ; i++)` <br>
i가 1부터 1씩 커지며 10미만일 때까지 반복합니다.
<br>

## [while문]

```
int i = 1;
while (i < 10) {
	System.out.printf("%d * %d = %d", 3, i, (3*i));
	i++;
}
```
`for` 코드와 마찬가지로, 구구단 3단을 출력합니다. <br>
`while(조건)`형태로 사용하며, 주로 `while`문 안에 `i++`와 같이 반복을 통해 조건을 거짓으로 만드는 코드를 적어넣습니다. <br>
조건을 `false`로 만들어 끝내지 않는다면, 무한루프에 빠져서 코드가 제대로 실행이 되지 않을 것입니다. <br>
<br>

## [do while문]

```
int i=1;
do {
	System.out.println("무조건 1번은 실행합니다.");
} while (i > 100);
```
`while`과 동일한 역할을 하는데, 단, 무조건 1번은 실행합니다.<br>
따라서 위 코드는 한 번 실행합니다.
