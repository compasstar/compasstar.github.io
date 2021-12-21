---
layout: post
title:  "[JAVA] 11. 소켓 Socket"
subtitle:   "소켓"
categories: JAVA
tags: JAVA
comments: true
date: 2021-12-21 00:23:47
---

<br>
인프런의 '자바 프로그래밍 입문 강좌 (renew ver.) - 초보부터 개발자 취업까지!!' 강의를 참고했습니다

<br><br>

# 1. Client Socket

***

```
public static void main(String[] args) {
		
	// Client 측
		
	// 필요한 모듈 설치
	Socket socket = null;
		
	OutputStream outputStream = null;
	DataOutputStream dataOutputStream = null;
		
	InputStream inputStream = null;
	DataInputStream dataInputStream = null;
		
	Scanner scanner = null;
		


	try {
	
		socket = new Socket("localhost", 9000);
		System.out.println("서버 연결 완료");
			
		outputStream = socket.getOutputStream();
		dataOutputStream = new DataOutputStream(outputStream);
			
		inputStream = socket.getInputStream();
		dataInputStream = new DataInputStream(inputStream);
			
		scanner = new Scanner(System.in);

		// 실행되는 것	
		while(true) {
			System.out.println("메세지 입력");
			String outMessage = scanner.nextLine();
			dataOutputStream.writeUTF(outMessage);
			dataOutputStream.flush(); // dataOutputStream을 비운다
				
			String inMessage = dataInputStream.readUTF();
			System.out.println("inMessage: " + inMessage);

			// 종료	
			if(outMessage.equals("STOP")) break;	
		}

	// 여기부터는 예외처리		
	} catch (Exception e) {
		e.printStackTrace();
	} finally {
			
		try {
			if(dataOutputStream != null) dataOutputStream.close();
			if(outputStream != null) outputStream.close();
			if(dataInputStream != null) dataInputStream.close();
			if(inputStream != null) inputStream.close();
				
			if(socket != null) socket.close();
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
}
```

- `new Socket("localhost", 9000);` localhost:9000 서버에 접속합니다
- `while`문 안에가 기능입니다
- 메세지를 입력하면 서버에 `writeUTF()`를 통해 입력하고, `readUTF()`를 통해 입력한 메세지를 보여줍니다

<br><br>

# 2. ServerSocket

***

```
public static void main(String[] args) {

	// Server 측
		
	// 필요한 모듈 설치
	ServerSocket serverSocket = null;
	Socket socket = null;
				
	OutputStream outputStream = null;
	DataOutputStream dataOutputStream = null;
				
	InputStream inputStream = null;
	DataInputStream dataInputStream = null;
				
	Scanner scanner = null;
				
				
	try {
			
		serverSocket = new ServerSocket(9000);
		System.out.println("클라이언트 맞을 준비 완료");
			
		socket = serverSocket.accept();
		System.out.println("클라이언트 연결");
		System.out.println("socket: " + socket);
					
		outputStream = socket.getOutputStream();
		dataOutputStream = new DataOutputStream(outputStream);
					
		inputStream = socket.getInputStream();
		dataInputStream = new DataInputStream(inputStream);

		// 실행 기능			
		while(true) {
				
			String clientMessage = dataInputStream.readUTF();
			System.out.println("clientMessage: " + clientMessage);
				
			dataOutputStream.writeUTF("메세지 전송 완료!");
			dataOutputStream.flush();
				
			if (clientMessage.equals("STOP")) break;	
		}

	// 여기부터 예외처리				
	} catch (Exception e) {
		e.printStackTrace();
	} finally {
					
		try {
			if(dataOutputStream != null) dataOutputStream.close();
			if(outputStream != null) outputStream.close();
			if(dataInputStream != null) dataInputStream.close();
			if(inputStream != null) inputStream.close();
						
			if(socket != null) socket.close();
		} catch(Exception e) {
			e.printStackTrace();
		}
	}
}
```
- `new ServerSocket(9000);` 9000번 서버를 엽니다
- `serverSocket.accept();` 클라이언트를 받아들입니다
- 클라이언트가 입력한 메세지를 `readUTF()`를 통해 읽어옵니다.
- 메세지가 전송되었음을 `writeUTF()`를 통해 알려줍니다


<br><br>


## [클라이언트 Console]

```
서버 연결 완료
메세지 입력
안녕하세요
inMessage: 메세지 전송 완료!
메세지 입력
오늘 날씨가 좋네요
inMessage: 메세지 전송 완료!
메세지 입력
STOP
inMessage: 메세지 전송 완료!
```

## [서버 Console]

```
클라이언트 맞을 준비 완료
클라이언트 연결
socket: Socket[addr=/127.0.0.1,port=56268,localport=9000]
clientMessage: 안녕하세요
clientMessage: 오늘 날씨가 좋네요
clientMessage: STOP
```