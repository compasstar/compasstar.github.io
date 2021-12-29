---
layout: post
title:  "[Spring] 1. 두 객체가 동일한지 비교하기 Assertions"
subtitle:   "두 객체가 동일한지 비교하기"
categories: Spring
tags: Spring
comments: true
date: 2021-12-29 00:14:15
---


<br><br>

# 두 객체가 동일한지 비교해보기

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
