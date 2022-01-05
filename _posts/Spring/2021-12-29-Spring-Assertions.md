---
layout: post
title:  "[Spring] 1. 테스트케이스 Assertions"
subtitle:   "Assertions"
categories: Spring
tags: Spring
comments: true
date: 2021-12-29 00:14:15
---


<br><br>

# 1. [assertThat] 두 객체가 동일한지 비교해보기

***

```
import org.assertj.core.api.Assertions;

@Test
public void test(){

int one = 1;
int two = 1;

Assertions.assertThat(one).isEqualTo(two);
}
```

`one`과 `two`가 동일하다면 테스트케이스를 통과하고, 다르다면 오류가 발생합니다.

<br><br>

2. [assertThrows] 

***

```
memberService.join(member1);

IllegalStateException e = assertThrows(IllegalStateException.class, () -> memberService.join(member2));


Assertions.assertThat(e.getMessage()).isEqualTo("이미 존재하는 회원입니다");
```
`memeber2`를 `join`하면 `IllegalStateException`이 발생하는 상황입니다. <br>
`assertThrows`를 이용해 람다함수를 실행했을 때, 해당에러가 발생하면 그 에러를 반환합니다. <br>
만일 지정한 에러가 아니라면 테스트에서 실패합니다.