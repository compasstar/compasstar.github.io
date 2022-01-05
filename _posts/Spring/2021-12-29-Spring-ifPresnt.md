---
layout: post
title:  "[Spring] 3. 해당 객체가 존재하는지 확인하기 ifPresent"
subtitle:   "해당 객체가 존재하는지 확인하기 ifPresent"
categories: Spring
tags: Spring
comments: true
date: 2021-12-29 00:16:47
---


<br><br>

# ifPresent()

***

```
Optional<Member> result = memberRepository.findByName(member.getName());

result.ifPresent(m -> {
    throw new IllegalStateException("이미 존재하는 회원입니다");
});
```

`Optional<>`을 이용하면 해당 변수가 null값이라도 받을 수 있습니다. <br>
`Optional<>` 형태를 띄고 있을 때, `ifPresent()`를 사용할 수 있습니다. <br>
만일 해당 변수가 존재한다면, 기능을 실행합니다.

<br><br>

```
memberRepository.findByName(member.getName())
    .ifPresent(m -> {
        throw new IllegalStateException("이미 존재하는 회원입니다");
});
```
요렇게 줄여서 사용할 수도 있습니다.