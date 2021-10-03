---
layout: post
title:  "[tkinter] 2. messagebox"
subtitle:   "tkinter messagebox"
categories: Python
tags: tkinter
comments: true
date: 2021-08-08 00:22:07
---

`tkinter`에서의 `massagebox` 문법에 대해 알아보겠습니다.<br>

'나도코딩'님의 강의를 참고했습니다. <br>
<a href="https://www.inflearn.com/course/%EB%82%98%EB%8F%84%EC%BD%94%EB%94%A9-%ED%8C%8C%EC%9D%B4%EC%8D%AC-%ED%99%9C%EC%9A%A9%ED%8E%B8-2/dashboard">파이썬 무료 강의 (활용편2) - GUI 프로그래밍 (4시간)</a>
<br><br>

***

![massagebox](https://user-images.githubusercontent.com/55419868/128633039-fefa28d7-a270-47f9-93d8-e66654e12e01.JPG)

이러한 메시지박스를 띄우는 방법을 알아보겠습니다.

```
import tkinter.messagebox as msgbox
from tkinter import *

root = Tk()
root.title("Nado GUI")
root.geometry("640x480") 

# 여러 코드들 작성
# 여러 코드들 작성
# 여러 코드들 작성

root.mainloop()
```
기본적인 프레임은 위와 같습니다. <br><br>


```
msgbox.showinfo("알림", "정상적으로 예매 완료되었습니다.")
```
알림창을 띄웁니다.

```
msgbox.showwarning("경고", "해당 좌석은 매진되었습니다.")
```
경고창을 띄웁니다.

```
msgbox.showerror("에러", "결제 오류가 발생했습니다.")
```
에러창을 띄웁니다.

```
msgbox.askokcancel("확인 / 취소", "해당 좌석은 유아동반석입니다. 예약 하시겠습니까?")
```
확인/취소를 물어보는 창을 띄웁니다.

```
response = msgbox.askretrycancel("재시도 / 취소", "일시적인 오류입니다. 다시 시도하시겠습니다?")
    if response == 1: # 재시도
        print("재시도")
    elif response == 0: # 취소
        print("취소")
```
재시도를 요청하는 창을 띄웁니다. 값을 설정해주어 재시도와 취소를 눌렀을 때 실행할 기능을 구분해줄 수 있습니다.

```
msgbox.askyesno("예 / 아니오", "해당 좌석은 역방향입니다. 예매하시겠습니까?")
```
예/아니오를 묻는 창을 띄웁니다.

```
response = msgbox.askyesnocancel(title=None, message = "예매 내역이 저장되지 않았습니다. \n 저장 후 프로그램을 종료하시겠습니까?")
    if response == 1:
        print("예")
    elif response == 0:
        print("아니오")
    else:
        print("취소")
```
네/아니오/취소 를 묻는 창을 띄웁니다. 값을 받아 각자 다른 명령을 수행할 수 있습니다.
<br><br>


전체코드입니다<br>
```
import tkinter.messagebox as msgbox
from tkinter import *

root = Tk()
root.title("Nado GUI")
root.geometry("640x480") 

# 기차 예매 시스템이라고 가정
def info():
    msgbox.showinfo("알림", "정상적으로 예매 완료되었습니다.")

def warn():
    msgbox.showwarning("경고", "해당 좌석은 매진되었습니다.")

def error():
    msgbox.showerror("에러", "결제 오류가 발생했습니다.")

def okcancel():
    msgbox.askokcancel("확인 / 취소", "해당 좌석은 유아동반석입니다. 예약 하시겠습니까?")

def retrycancel():
    response = msgbox.askretrycancel("재시도 / 취소", "일시적인 오류입니다. 다시 시도하시겠습니다?")
    if response == 1: # 재시도
        print("재시도")
    elif response == 0: # 취소
        print("취소")
    
def yesno():
    msgbox.askyesno("예 / 아니오", "해당 좌석은 역방향입니다. 예매하시겠습니까?")

def yesnocancel():
    response = msgbox.askyesnocancel(title=None, message = "예매 내역이 저장되지 않았습니다. \n 저장 후 프로그램을 종료하시겠습니까?")
    if response == 1:
        print("예")
    elif response == 0:
        print("아니오")
    else:
        print("취소")

Button(root, command=info, text="알림").pack()
Button(root, command=warn, text="경고").pack()
Button(root, command=error, text="에러").pack()

Button(root, command=okcancel, text="확인 취소").pack()
Button(root, command=retrycancel, text="재시도 취소").pack()
Button(root, command=yesno, text="예 아니오").pack()
Button(root, command=yesnocancel, text="예 아니오 취소").pack()

root.mainloop()
```