---
layout: post
title:  "[Python] 2. 이중 for 문 탈출하기"
subtitle:   "이중 for 문 출하기"
categories: Python
tags: Python
comments: true
date: 2021-08-02 00:14:34
---

```
for i in range(0, 10):
    print(i)
    if i > 5:
        break
```
저희는 `for` 문을 탈출할 때 `break` 를 사용합니다. <br>
그런데 `for` 문 안에 또 `for` 문이 들어있다면 어떻게 두 반목문을 동시에 나갈 수 있을까요?

```
for i in range(0, 10):
    for j in range(0, 10):
        if j == 5:
            break
    else:
        continue
    break
```

`for` 문에도 `else` 를 사용할 수 있습니다. <br> 
범위를 전부 순회하면 그 후 `else` 로 향해서 실행하게 됩니다. <br>
그러나 위의 코드처럼 중간에 `break` 로 순회를 깨주게 되면, `else` 를 지나치게 됩니다. <br>
그래서 첫번째 `for` 문의 `break` 에 도달하게 되는 것이죠.