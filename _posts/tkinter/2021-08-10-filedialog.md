---
layout: post
title:  "[tkinter] 3. filedialog 파일 / 폴더 추가"
subtitle:   "tkinter filedialog"
categories: tkinter
tags: tkinter
comments: true
date: 2021-08-10 00:15:23
---

tkinter 를 사용할 때, 파일을 추가하는 법을 알아보겠습니다.<br>

```
from tkinter import filedialog
```
`filedialog` 를 우선 `import` 해줍니다.

```
files = filedialog.askopenfilenames(title="이미지 파일을 선택하세요", filetypes=(("PNG 파일", "*.png"), ("모든 파일", "*.*")), initialdir="C:/")
```
위 코드를 사용하여 파일들을 불러올 수 있습니다. <br><br>
`filetypes`로 불러오고자 하는 파일의 형태를 결정하면 됩니다.<br>
`initialdir`로 파일 탐색창의 첫 디렉토리를 설정할 수 있습니다.
    
```
filedialog.askdirectory()
```
위 코드로는 폴더를 불러올 수 있습니다. (괄호 안의 내용은 동일)