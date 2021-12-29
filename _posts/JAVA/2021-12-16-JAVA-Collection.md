---
layout: post
title:  "[JAVA] 8. ArrayList, HashMap"
subtitle:   "ArrayList, HashMap"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-16 00:22:40
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 1. ArrayList

ArrayList는 변수들을 저장하는 리스트입니다. <br>
각 변수마다 순서대로 index가 붙어있어 이를 기준으로 변수를 선택할 수 있습니다.

```
import java.util.ArrayList;

public class MainClass {

	public static void main(String[] args) {
		
		ArrayList<String> list = new ArrayList<String>();

		// 데이터 추가
		list.add("Hello");
		list.add("JAVA");
		list.add("World");
		System.out.println("list.size: " + list.size()); // 3

		System.out.println("list: " + list);
        // list: [Hello, JAVA, World]
		
		list.add(2, "Programming");
		System.out.println("list: " + list);
        // list: [Hello, JAVA, Programming, World]
		
		list.set(1, "C");
		System.out.println("list: " + list);
        // list: [Hello, C, Programming, World]

		// 데이터 제거		
		String str = list.remove(2);
		System.out.println("list.remove(2): " + str);
        // list.remove(2): Programming
		System.out.println("list: " +list);
        // list: [Hello, C, World]
		
		// 데이터 전체 제거
		list.clear();
		System.out.println("list: " + list);
        // list: []
		
		// 데이터 유무
		boolean b = list.isEmpty();
		System.out.println("list.isEmpty(): " + b);
        // true
    }
}
```
- `import java.util.ArrayList;`를 우선 가져옵니다.
- `list.size()` 리스트의 사이즈(길이)를 가져옵니다.
- `list.add(index, x)` x를 index 위치에 추가합니다.
- `list.set(index, x)` index 위치에 있는 것을 x로 바꿉니다.
- `list.remove(index)` index 위치에 있는 것을 제거합니다. 이는 변수로 저장할 수 있습니다.
- `list.clear()` 리스트를 완전히 비웁니다.
- `list.isEmpty()` 비어있다면 `true` 아니라면 `false`를 반환합니다.

<br><br>

# 2. HashMap

HashMap은 변수들의 집합인데, 각 변수마다 key(고유 숫자)와 value가 붙어있어, key로 value를 가리킵니다. <br>
애초에 저장할 때 부터 key(int)와 value(Stirng)를 함께 넣어줍니다.

```
import java.util.HashMap;

public class MainClass {

	public static void main(String[] args) {

		// HashMap 객체 생성
		HashMap<Integer, String> map = new HashMap<Integer, String>();
		
		// 데이터 추가
		map.put(5, "Hello");
		map.put(6, "Java");
		map.put(7, "World");
		System.out.println("map: " + map);
        // map: {5=Hello, 6=Java, 7=World}

		System.out.println("map.size: " + map.size());
        // map.size: 3
		
		map.put(8, "!!");
		System.out.println("map: " + map);
		
		// 데이터 교체
		map.put(6, "C");
		System.out.println("map: " + map);
		
		// 데이터 추출
		String str1 = map.get(5);
		System.out.println("map.get(5): " + str1);
        // map.get(5): Hello
		
		// 데이터 제거
		map.remove(8);
		System.out.println("map: " + map);
		
		// 특정 데이터 포함 유무
		boolean b1 = map.containsKey(7);
		System.out.println("map.containsKey(7): " + b1);
        // true
		
		b = map.containsValue("World");
		System.out.println("map.containsValue(\"World\"): " + b);
		
		// 데이터 전체 제거
		map.clear();
		System.out.println("map: " + map);
		
		// 데이터 유무
		b = map.isEmpty();
		System.out.println("map.isEmpty(): " +  b);
	}
}
```

- `import java.util.HashMap;`를 우선 가져옵니다.
- `map.put(5, "Hello");` value를 key와 함께 추가합니다. (만일 해당 key에 해당되는 변수가 이미 저장되어있다면, 이로 변환합니다.)
- `map.size()` 해쉬맵의 사이즈(길이)를 가져옵니다.
- `map.get(5)` 해당 key를 가진 변수를 가져옵니다.
- `map.remove(8);` 해당 key를 가진 변수를 제거합니다.
- `map.containsKey(7);` 해당 key를 가진 변수가 있는 지 boolean 형태로 가져옵니다.
- `map.containsValue("World");` 특정 value를 가진 변수가 있는 지 boolean 형태로 가져옵니다.
- `map.clear();` 해당 해쉬맵 안에 있는 데이터를 모두 지웁니다.
- `map.isEmpty();` 해쉬맵에 데이터가 있는지 없는지 boolean 형태로 반환합니다.

<br><br>

# 3. HashMap 에서 value값 key로 찾기, value로 찾기

***

```
@Test
public void test(){
    HashMap<Integer, String> map = new HashMap<Integer, String>();

    map.put(1, "one");
    map.put(2, "two");
    map.put(3, "three");
    map.put(4, "four");

    String answer1 = map.get(3);

    String answer2 = map.values().stream()
            .filter(number -> number.equals("three"))
            .findAny().get();
}
```
`map`에 <key, value> 4개를 넣었습니다.

1. key 값으로 찾기
> `map.get(3)`으로 key값이 3인 value를 반환합니다.

<br>

2. value 값으로 찾기
> `map.values()` value 값들 중에<br>
>  `.steam()` 돌면서<br>
>  `.filter(nember -> number.equals("three"))` 'three' 와 동일한 것을 걸러냅니다. (여기서 `number`는 아무 글자가 넣어도 괜찮습니다 반복문에서 임시로 넣는 변수같은 것입니다)<br>
> `.findAny()` 하나라도 필터링되면 그만합니다.

<br>

`answer1` `answer2` 두 개다 동일하게 `three`라는 문자가 저장됩니다.