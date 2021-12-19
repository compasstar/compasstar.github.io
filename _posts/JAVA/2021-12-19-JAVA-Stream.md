---
layout: post
title:  "[JAVA] 10. 스트림 Stream (Input / Output)"
subtitle:   "스트림 Stream"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-19 00:12:08
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다
<br><br>
여러가지 Stream 방법을 사용하여 파일을 복사해보겠습니다.

<br><br>

# 1. InputStream / OutputStream

***

```
// InputStream / OutputStream 생성
InputStream inputStream = null;
OutputStream outputStream = null;

try {
	// Hello Java2.txt 를 읽는다
	inputStream = new FileInputStream("C:/Projects/Java_lecture/Hello Java2.txt");
	// Hello Java2 copy.txt 파일을 만든다
	outputStream = new FileOutputStream("C:/Projects/Java_lecture/Hello Java2 copy.txt");
			
	byte arr[] = new byte[3];
			
	while(true) {
		
		// arr 에 Hello Java2.txt에서 read한 것 저장
		int len = inputStream.read(arr);

		System.out.println("len: " + len);
		if(len == -1) break;

		// arr를 Hello Java2 copy 에 write한다
		outputStream.write(arr, 0, len);
	}
} catch (IOException e) {
	e.printStackTrace();
} finally {
	try {
		// 종료
		if(outputStream != null) outputStream.close();
		if(inputStream != null) inputStream.close();
	} catch (IOException e) {
		e.printStackTrace();
	}
}
```
- `InputStream` 을 통해 파일을 `read`하고, `OutputStream`을 이용해 새로운 파일에 `write`하는 방식입니다
- `byte arr[]`
  > byte 형태로 만들어서 문자열을 `read`, `write` 할 것입니다<br>(InputStream OutputStream 은 byte 단위로만 작업이 가능합니다)

- `int len = inputStream.read(arr);` 
> 읽어온 것을 `arr`에 아스키형태로 저장하고, 읽어온 문자열의 길이를 반환합니다.<br> `arr`의 크기가 3이므로, 3을 반환할 것입니다.<br> 단, 문자가 없다면 -1을 반환합니다.  <br>(문자열의 끝에 가면 3이 아닐 수도 있음 <br>-> 예시: 'JAVA' 3반환, 1반환)
- `outputStream.write(arr, 0, len);` 
>`arr`의 0번 인덱스부터 `len`만큼의 문자를 가져와서 입력합니다

<br><br>

# 2. DataInputStream / DataOutputStream

***

```
OutputStream outputStreamZero = null;
DataOutputStream dataOutputStreamZero = null;
InputStream inputStream = null;
DataInputStream dataInputStream = null;
OutputStream outputStream = null;
DataOutputStream dataOutputStream = null;
		
try {

	// Hello Java3.txt 파일 만들고 'Hello Java3' write한다		
	outputStreamZero = new FileOutputStream("C:/Projects/Java_lecture/Hello Java3.txt");
	dataOutputStreamZero = new DataOutputStream(outputStreamZero);
	String strZero = "Hello Java3";
	dataOutputStreamZero.writeUTF(strZero);
			
	// Hello Java3.txt 를 읽는다
	inputStream = new FileInputStream("C:/Projects/Java_lecture/Hello Java3.txt");
	dataInputStream = new DataInputStream(inputStream);
			
	String str = dataInputStream.readUTF();
			
	// Hello Java3 copy.txt 만들고 입력한다
	outputStream = new FileOutputStream("C:/Projects/Java_lecture/Hello Java3 copy.txt");
	dataOutputStream = new DataOutputStream(outputStream);
			
	dataOutputStream.writeUTF(str);
			
} catch (Exception e) {
	e.printStackTrace();
} finally {
	try {
		// 종료
		if(outputStreamZero != null) outputStreamZero.close();
		if(dataOutputStreamZero != null) outputStreamZero.close();
		if(inputStream != null) inputStream.close();
		if(dataInputStream != null) dataInputStream.close();
		if(outputStream != null) outputStream.close();
		if(dataOutputStream != null) dataOutputStream.close();
	} catch (IOException e) {
		e.printStackTrace();
	}
}
```

- `DataInputStream` / `DataOutputStream` 도 과정은 같습니다
- `InputStream` / `OutputStream`에서 생성한 것을 `DataInputStream` / `DataOutputStream`에 넣어주기만 하면 똑같습니다
- 차이점은 byte단위로 하지 않아도 된다는 것입니다. 문자를 그대로 사용할 수 있습니다.
- `readUTF()` / `writeUTF(str)` 를 사용합니다
- 단, 애초에 읽어올 때, `writeUTF()` 형태로 입력한 것이 아니면, 에러가 발생합니다. 그러므로 자유롭게 사용하기 어렵습니다.
- 메모장 형태로 입력했을 때, 글자가 깨지는 경우가 발생합니다. 다른 프로그램으로 읽으면 제대로 읽히긴 합니다.

<br>

[Hello Java3 copy.txt] 의 깨진모습
```
 Hello Java3
```
정체불명의 마크가 앞에 추가되어 있습니다...

<br><br>

# 3. BufferedReader / BufferedWriter

***

```
FileReader fr = null;
BufferedReader br = null;
FileWriter fw = null;
BufferedWriter bw = null;
		
try {
			
	// 'Hello Java.txt' 를 읽어옵니다
	fr = new FileReader("C:\\Projects\\Java_lecture\\Hello Java.txt");
	br = new BufferedReader(fr);
			
	// 'Buffered Hello Java.txt' 를 만듭니다
	fw = new FileWriter("C:\\Projects\\Java_lecture\\Buffered Hello Java.txt");
	bw = new BufferedWriter(fw);
			
	String strLine;
			
	// 'Hello Java.txt' 에서 읽은 것을 'Buffered Hello Java.txt'에 붙여넣습니다
	while ((strLine = br.readLine()) != null) {		
		bw.write(strLine);
	}
} catch (IOException e) {
	e.printStackTrace();
} finally {
		
	try {
		if (br != null) br.close();
		if (fr != null) fr.close();
				
		// BufferedWriter를 먼저 닫고 그 후에 FileWriter를 닫아야 한다
		if (bw != null) bw.close();
		if (fw != null) fw.close();
				
	} catch (IOException ex) {
		ex.printStackTrace();
	}
}
```

- 과정은 BufferedReader / BufferedWriter 도 다 똑같습니다.
- `FileReader` / `FileWirter` 로 생성한 것을 `BufferedReader` / `BufferedWriter` 에 집어넣어 사용합니다
- `br.readLine()`
  > 한 줄 단위로 읽어옵니다
- `bw.write(strLine);`
  > 한 줄 단위로 읽어온 `strLine` 을 붙여넣습니다
- 종료할 때, `Buffered`를 먼저 종료하고 `FileReader` /`FileWriter`를 종료하셔야 에러가 발생하지 않습니다.