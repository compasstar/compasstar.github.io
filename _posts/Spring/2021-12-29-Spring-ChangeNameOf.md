---
layout: post
title:  "[Spring] 2. 단축키
subtitle:   "단축키"
categories: Spring
tags: Spring
comments: true
date: 2021-12-29 00:14:20
---

'IntelliJ' 에서 사용하는 단축키들을 알아보겠습니다.

<br><br>

# 1. [Shift + F6] : 한번에 동일한 변수이름들 바꾸기 

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


<br><br>

# 2. [Ctrl + Alt + v] : Optional<> 추가

```
memberRepository.findByName(member.getName());
```

```
Optional<Member> byName = memberRepository.findByName(member.getName());
```
`Ctrl + Alt + v` 를 누르면 위의 코드에서 아래와 같이 자동으로 입력이 됩니다.<br>
`byName`만 자신이 원하는 이름으로 변경하시면 됩니다.
