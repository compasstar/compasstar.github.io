---
layout: post
title:  "[CSS] 10.CSS 컨탠트(content)"
subtitle:   "CSS content"
categories: CSS
tags: CSS
comments: true
date: 2021-07-22 00:14:39
---


```
<style>
  .title:before, .title:after{
    content: "-example-";
  }
</style>

<div class="title"> Title </div>
```

<style>
  .title:before, .title:after{
    content: "-example-";
  }
</style>

<div class="title"> Title </div>

***

`:before`
> `content` 값을 앞쪽에 붙입니다.

`:after`
> `content` 값을 뒤쪽에 붙입니다.