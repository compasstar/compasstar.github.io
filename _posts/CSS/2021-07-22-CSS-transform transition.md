---
layout: post
title:  "[CSS] 10.CSS transform transition 속성"
subtitle:   "CSS transform/transition"
categories: CSS
tags: CSS
comments: true
date: 2021-07-22 00:14:52
---

<h1>transform</h1>

```
transform: translate(50px, 50px);
```
(x축, y축) 만큼 이동시킵니다

```
transform: scale(0.5, 0.5);
```
(가로,세로) 배수만큼 크기를 조절합니다. 

```
transform: rotate(90deg);
```
(degree)만큼 회전시킵니다.

```
transform: skew(30deg, 0);
```
(x축, y축) 만큼 경사를 만듭니다.
<br><br>


<h1>transition</h1>

`transition`은 property를 변경시킵니다.

```
div{
  transition: transform 3s;
}

div:hover{
  transform: scale(1.5) rotate(180dgr)
}
```

`div:hover`
> 마우스를 올리면 크기가 1.5배가 되고, 180도 돌리는 코드입니다.

`trnasition: transform 3s;`
> `transform`을 통해 크기를 바꾸고, 돌리는 코드를 3초에 걸쳐 실행하게 만들었습니다.