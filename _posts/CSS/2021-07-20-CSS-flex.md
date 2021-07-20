---
layout: post
title:  "[CSS] 4.CSS keyframes"
subtitle:   "CSS keyframes"
categories: CSS
tags: CSS
comments: true
date: 2021-07-20 00:16:40
---

`keyframes`을 통해 회전하는 애니메이션을 만들어보겠습니다.

```
@keyframes rotate {
    0%{
        transform: translateY(0);
    }
    25%{
        transform: translateY(-20%);
    }
    50%{
        transform: translateY(-40%);
    }
    75%{
        transform: translateY(-60%);
    }
    100%{
        transform: translateY(-80%);
    }
}
```

5단계로 나누어 Y축의 위치를 20%씩 옮겨주었습니다. <br>

(-) 방향이므로 위쪽으로 올라가게 됩니다. <br>

```
animation: rotate 7s infinite;
```
적용시키고자 하는 개체에 위의 코드를 작성해주시면 적용이 됩니다.  <br>

7초 동안 회전하고, 무한으로 실행하라는 뜻입니다.


