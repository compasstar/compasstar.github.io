---
layout: post
title:  "[tkinter] 1. tkinter 기본문법(1)"
subtitle:   "tkinter frame"
categories: tkinter
tags: tkinter
comments: true
date: 2021-08-05 00:14:02
---

`tkinter`의 문법에 대해 알아보겠습니다.<br>

'나도코딩'님의 강의를 참고했습니다. <br>
<a href="https://www.inflearn.com/course/%EB%82%98%EB%8F%84%EC%BD%94%EB%94%A9-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%ED%99%9C%EC%9A%A9%ED%8E%B8-2/dashboard">파이썬 무료 강의 (활용편2) - GUI 프로그래밍 (4시간)</a>

<br><br>

<h1>1. 프레임</h1>

```
from tkinter import *

root = Tk()
root.title("Nado GUI")
root.geometry("640x480") # 가로 * 세로

root.mainloop()
```

***

기본적으로 이 프레임으로 코드를 작성해 나갑니다.<br>
 앞으로 나오는 코드들은 `root.geomery()` 와 `root.mainloop()` 사이에 작성됩니다.

`import *`
>`tkinter` 의 모든 것을 `import` 한다는 뜻입니다.

```
root.geometry("640x480+300+100")
```
가로크기 640, 세로크기 480, x좌표 300, y좌표 100 으로 GUI 를 조절합니다.<br>
 크기와 창이 나타나는 위치를 설정할 수 있습니다.


```
root.resizeable(False, False)
```
x값, y값을 변강하지 못하게 하여, GUI 사이즈 조절을 막습니다.

<br><br>

<h1>2. 버튼</h1>

```
btn1 = Button(root, fg="red", bg="yellow", text="버튼1")
btn1.pack()
```
버튼을 만들어줍니다. <br>
root라는 곳에 글자색은 red, 배경색은 yellow, 텍스트는 "버튼1"의 버튼을 만듭니다. <br>
`.pack()`을 적어주어야 GUI에 버튼이 나타나게 됩니다. 이 명령어는 버튼 뿐만 아니라 다른 것들도 마찬가지입니다.

```
photo = PhotoImage(file="gui_basic/img.png")
btn6 = Button(root, image=photo)
btn6.pack()
```
버튼을 image형태로 만들어 줄 수도 있습니다.

```
def btncmd():
    print("버튼이 클릭되었어요")

btn7 = Button(root, text="동작하는 버튼", command=btncmd)
btn7.pack()
```
버튼을 누르면 함수를 실행하도록 했습니다.

<br><br>

<h1>3. 라벨</h1>

```
label1 = Label(root, text="안녕하세요")
label1.pack()

photo = PhotoImage(file="img.png")
label2 = Label(root, image=photo)
label2.pack()

def change():
    label1.config(text="또 만나요")

    global photo2
    photo2 = PhotoImage(file="img2.png")
    label2.config(image=photo2)

btn = Button(root, text="클릭", command=change)
btn.pack()
```

<img src="https://user-images.githubusercontent.com/55419868/128297144-22c63af0-b10d-4e61-8b22-8e15c3062922.JPG" width="400px">

<img src="https://user-images.githubusercontent.com/55419868/128297196-341b26a7-e699-4366-8612-209a39fd055a.JPG" width="400px">

***

`label`을 만들고 버튼을 누르면 `config`를 통해 텍스트와 이미지가 바뀌도록 하였습니다. <br>
`global` 을 사용한 이유는 `global`을 쓰지 않으면 함수가 나갈 때, `photh2` 변수가 사라져 버립니다. 그래서 함수를 나가도 `photo2`가 사라지지 않도록 `global`을 통해 정의해주었습니다.

<br><br>

<h1>4. text / entry</h1>

```
txt = Text(root, width=30, height=5)
txt.pack()
txt.insert(END, "글자를 입력하세요.") 

e = Entry(root, width=30)
e.pack()
e.insert(0, "한 줄만 입력해요")
```
![text entry](https://user-images.githubusercontent.com/55419868/128298330-14ce85ac-4c7b-4ad6-8294-d898aa088fc0.JPG)

***

`Text` 는 텍스트상자를 만듭니다.
`Entry` 는 한 줄짜리 텍스트 상자를 만듭니다.

```
`.insert(END), "글자를 입력하세요.")` 
```
위치와 내용을 받아 삽입합니다.


```
txt.get("1.0", END)
```
1번 `row`의 0번 `column` 부터 `END` 까지를 선택합니다.

```
txt.delete("1.0", END)
```
1번 `row`의 0번 `column` 부터 `END` 까지를 삭제합니다.

<br><br>

<h1>5. listbox</h1>

```
listbox = Listbox(root, selectmode="extended", height=0) # single도 있는데, 선택할 수 있는 개수의 차이이다. height는 보여지는 개수. 0으로 하면 다 보인다.
listbox.insert(0, "사과")
listbox.insert(1, "딸기")
listbox.insert(2, "바나나")
listbox.insert(END, "수박")
listbox.insert(END, "포도")
listbox.pack()
```

![listbox](https://user-images.githubusercontent.com/55419868/128299661-f95a9fb7-600b-4fca-ae31-9b39bf976135.JPG)


`selectmode="extended"` 로 하면 리스트박스에서 여러개를 선택할 수 있습니다. <br>
`height`는 리스트박스에서 보여지는 개수 입니다. 0으로 하면 전부 보여줍니다.

```
listbox.delete(0)
```
0번째 인덱스의 항목을 삭제합니다.

```
listbox.size()
```
리스트박스의 사이즈를 반환합니다.

```
listbox.curselection()
```
리스트박스에서 선택된 항목을 인덱스로 반환합니다.