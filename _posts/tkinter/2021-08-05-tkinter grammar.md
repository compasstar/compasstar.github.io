---
layout: post
title:  "[tkinter] 1. tkinter 기본문법"
subtitle:   "tkinter 기본문법"
categories: Python
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
listbox = Listbox(root, selectmode="extended", height=0)
listbox.insert(0, "사과")
listbox.insert(1, "딸기")
listbox.insert(2, "바나나")
listbox.insert(END, "수박")
listbox.insert(END, "포도")
listbox.pack()
```

![listbox](https://user-images.githubusercontent.com/55419868/128299661-f95a9fb7-600b-4fca-ae31-9b39bf976135.JPG)


`selectmode="extended"` 로 하면 리스트박스에서 여러개를 선택할 수 있습니다. `single` 이라면 한 개만 선택할 수 있습니다. <br>
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

<br><br>

<h1>6. checkbox</h1>

```
chkvar = IntVar() 
chkbox = Checkbutton(root, text="오늘 하루 보지 않기", variable=chkvar)
chkbox.pack()
```
`chkvar` 는 체크가 되었다면 1, 안 되었다면 0의 값을 저장합니다.
```
chkbox.select() 
```
자동으로 선택되게 처리합니다.

<br><br>

<h1>7. radiobutton</h1>

```
Label(root, text="메뉴를 선택하세요").pack()

burger_var = IntVar() # 여기에 int 형으로 값을 저장한다
btn_burger1 = Radiobutton(root, text="햄버거", value=1, variable=burger_var)
btn_burger1.select()
btn_burger2 = Radiobutton(root, text="치즈버거", value=2, variable=burger_var)
btn_burger3 = Radiobutton(root, text="치킨버거", value=3, variable=burger_var)

btn_burger1.pack()
btn_burger2.pack()
btn_burger3.pack()
```

`burger_var` 가 `Int` 형태의 값을 가지기에, `value` 에도 `Int` 형태로 값이 들어갔습니다.

<br><br>

<h1>8. combobox</h1>

```
import tkinter.ttk as ttk

values = [str(i) + "일" for i in range(1, 32)]
combobox = ttk.Combobox(root, height=5, values=values)
combobox.pack()
combobox.set("카드 결제일")
```

<img width="250" src="https://user-images.githubusercontent.com/55419868/128630717-d5af8b39-a4e6-4f12-8060-1bf5cc989962.JPG"/>

이렇게 생긴 창이 combobox 입니다.

combobox를 사용하기 위해서는 `tkinter.ttk`를 `import` 해주세요. <br>

`height` 는 combobox가 펼쳐질 때, 보여줄 항목의 개수입니다. (5일 까지 나온 것을 확인할 수 있습니다)<br>
`set`을 통해 최초 목록 제목을 설정할 수 있습니다.

<br><br>

<h1>9. progressbar</h1>

```
import time
import tkinter.ttk as ttk

p_var2 = DoubleVar()
progressbar2 = ttk.Progressbar(root, maximum=100, length=150, variable=p_var2)
progressbar2.pack()

def btncmd2():
    for i in range(1, 101):
        time.sleep(0.01) # 0.01 초 대기

        p_var2.set(i) # progress bar 의 값 설정
        progressbar2.update() # ui 업데이트


btn = Button(root, text="시작", command=btncmd2)
btn.pack()

root.mainloop()
```

![progressbar](https://user-images.githubusercontent.com/55419868/128630895-a79daa79-6558-4e9b-98b1-b97a31a64706.JPG)

로딩 시 흔히 볼 수 있는 brogressbar 입니다. <br>

이번에도 `tkinter.ttk`를 `import` 해주세요

***

`maximum` 은 실제 갖는 값입니다. `maximum` 값이 100이고, `for` 문을 통해 1~100 까지 값을 설정했으므로, progressbar가 끝까지 차게 됩니다. 만일 `maximum`이 200이라면, 절반만 차게 될 것입니다. <br><br>
`length` 는 창에서 보이는 길이 입니다. 스크린에 나타나는 `progressbar`의 길이가 조절 됩니다. <br><br>
`variable`은 작은 단위로 변하기에 `Double` 형태로 값을 주었고, `.set`을 통해 입력해주었습니다. <br><br>

`update`를 통해 계속 반영해야 `progressbar`가 차오르는 것을 부드럽게 확인할 수 있습니다.

***

```
progressbar = ttk.Progressbar(root, maximum=100, mode="indeterminate")
```
`mode`를 주는 것으로 로딩이 끝나지 않도록 만들 수 있습니다.

```
progressbar.start(10)
```
위의 코드처럼 `for`문을 통해 값을 계속 설정해주지 않아도, 이 코드를 사용하여 10ms 마다 움직이게 설정할 수 있습니다. 

<br><br>

<h1>10. menu</h1>

```
menu = Menu(root)

# File 메뉴
menu_file = Menu(menu, tearoff=0)
menu_file.add_command(label="New File")
menu_file.add_command(label="New Window")
menu_file.add_separator()
menu_file.add_command(label="Open File...")
menu_file.add_separator()
menu_file.add_command(label="Save All", state="disable") 
menu_file.add_separator()
menu_file.add_command(label="Exit", command=root.quit)

menu.add_cascade(label="File", menu=menu_file)

root.config(menu=menu)
```

<img width=250 src="https://user-images.githubusercontent.com/55419868/128631266-34999807-2fc5-4d1a-99a3-2c1eb2654469.JPG"/>

1. `menu = Menu(root)`
> 메뉴를 만듭니다.

2. `menu_file = Menu(menu, tearoff=0)`
> 변수를 만들어 메뉴를 집어 넣습니다.

3. `menu.add_cascade(label="File", menu=menu_file)`
> 해당 변수에 이름을 붙이고, 메뉴에 띄우게 합니다.

4. `root.config(menu=menu)`
> 해당 메뉴에 적용시킨 여러 것들을 적용시킵니다.

* `state="disable"`
> 해당 메뉴를 비활성화 시킵니다. <br>

* `menu_file.add_separator()`
> 줄을 그어 구분합니다.

<br><br>

<h1>11. frame</h1>

```
Label(root, text="메뉴를 선택해 주세요").pack(side="top")

Button(root, text="주문하기").pack(side="bottom")

frame_burger = Frame(root, relief="solid", bd=1)
frame_burger.pack(side="left", fill="both", expand=True)

Button(frame_burger, text="햄버거").pack()
Button(frame_burger, text="치즈버거").pack()
Button(frame_burger, text="치킨버거").pack()
```

<img width=400 src="https://user-images.githubusercontent.com/55419868/128632560-aa41d9ae-88ad-4140-8144-6ab1564b93f8.JPG"/>

여태는 `root` 에만 여러 인터페이스들을 띄웠습니다. 그런데, `frame`을 만들어 그곳에도 버튼이나 라벨 등을 만들 수 있습니다. <br>

프레임을 만들어주고, 만들어 주는 위치를 그 프레임으로 만들어 주시면 됩니다.
<br><br>


<h1>12. scrollbar</h1>

```
frame = Frame(root)
frame.pack()

scrollbar = Scrollbar(frame)
scrollbar.pack(side="right", fill='y')

# set 이 없으면 스크롤을 내려도 다시 올라옴
listbox = Listbox(frame, selectmode="extended", height=10, yscrollcommand = scrollbar.set)

for i in range(1, 32):
    listbox.insert(END, str(i) + "일") # 1일, 2일 ...

listbox.pack(side="left")

scrollbar.config(command=listbox.yview)
```

스크롤바를 만드는 코드입니다.
리스트박스를 만들어 그곳에 적용시켜보았습니다.
`listbox`와 `scrollbar` 양 쪽에서 `.config` 와 `yscrollcommand` 를 이용해 서로 연결을 시켜주어야 합니다. 

<br><br>


<h1>13. grid</h1>

`grid`를 통해 격자모양을 만들 수 있습니다. 좌표를 찍는다고 생각하시면 편할 것 같습니다.

```
btn1 = Button(root, text="버튼1")
btn2 = Button(root, text="버튼2")

btn1.grid(row=0, column=0)
btn2.grid(row=1, column=1)
```

![grid](https://user-images.githubusercontent.com/55419868/128632935-f5d67ecb-15b8-4548-b222-0c3746ca704f.JPG)


원하는 인터페이스를 만든 후, `.grid`를 통해 위치를 설정해 줍니다. (0,0) (1,1) 위치로 입력했습니다. <br>
참고로 `.pack()` 이 필요 없습니다!