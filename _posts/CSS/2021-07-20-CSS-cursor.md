---
layout: post
title:  "[CSS] 6.CSS 버튼에 효과주기"
subtitle:   "CSS 버튼"
categories: CSS
tags: CSS
comments: true
date: 2021-07-20 00:16:46
---

버튼에 효과를 주어보겠습니다.

```
.button button{
    width: 300px;
    height: 50px;
    padding: 5px;
    border-style: none;
    border-radius: 10px;
    font-family: 'NEXON Lv1 Gothic OTF';
    font-size: 20px;
    font-weight: bold;
    background-color: #ffffff;
    color: #7F47DD;
    cursor: pointer;
    margin-bottom: 20px;

}
```
버튼을 적당히 만들어줍니다. <br>

`cursor: potiner;`
> 버튼에 마우스를 올렸을 때, 마우스 모양을 변환시킵니다.
 
<br>

```
.button button:hover {
    text-decoration: underline;
    background-color: aqua;
    transition: all 2s;
}
```
`button:hover`
> 효과를 주기 위한 코드입니다. <br>
> `transition: all 2s;` 로 인해 2초에 걸쳐 밑줄이 생기고, 배경색이 아쿠아색으로 변합니다.
