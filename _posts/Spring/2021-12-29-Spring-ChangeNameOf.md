---
layout: post
title:  "[Spring] 2. 단축키: 한번에 동일한 변수이름들 바꾸기"
subtitle:   "단축키: 한번에 동일한 변수이름들 바꾸기"
categories: Spring
tags: Spring
comments: true
date: 2021-12-29 00:14:20
---


<br><br>

# [Shift + F6] : 한번에 동일한 변수이름들 바꾸기 

***

```
Member member1 = new Member();
member1.setName("spring1");
repository.save(member1);

Member member2 = new Member();
member2.setName("spring1");
repository.save(member2);
```

위 코드에서 위의 3줄을 복사하여 아래 붙여넣기 하였습니다. 그리고 `member1`을 전부 `member2`로 바꿔야 합니다. <br>
하나씩 변경하면 귀찮기 때문에 `Shift` + `F6`을 누르면 한꺼번에 바꿀 수 있습니다.
