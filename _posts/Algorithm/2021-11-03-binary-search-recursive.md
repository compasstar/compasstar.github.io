---
layout: post
title:  "[Algorithm] 7. 이진탐색 (재귀버전)"
subtitle:   "이진탐색 (재귀버전)"
categories: Algorithm
tags: Algorithm
comments: true
date: 2021-11-03 00:12:08
---

# 1. 이진탐색의 원리
<br>

## [개념]

- 오름차순으로 정렬 된 배열에서 찾고자하는 원소 x가 있습니다.
- 배열의 중앙에 있는 값과 x를 비교합니다.
- 만일 x가 더 크다면 배열에서 중앙값 이하 값들은 제거합니다. (절반 제거)
- 반대로 x가 더 작다면 배열에서 중앙값 이상 값들을 제거합니다. (절반 제거)
- 위 과정을 중앙에 있는 값과 x가 일치할 때까지 반복합니다.
<br><br>


## [예시]
<br>

[-92 -31 -7 4 14 20 29 44]
> x(20)를 찾고자 합니다.

[-92 -31 -7 4 <b>14</b> 20 29 44]
> 중앙값(14)과 x(20)를 비교했더니, x가 더 크므로 중앙값 이하 값들을 제외합니다.

[20 <b>29</b> 44]
> 중앙값(29)과 x(20)를 비교했더니, x가 더 작으므로 중앙값 이상 값들을 제외합니다.

[<b>20</b>]
> 중앙값(20)과 x(20)를 비교했더니, x와 같으므로 중앙값(20)을 index를 return 합니다.



<br><br>

## [시간복잡도]


> 한 번 수행마다 배열이 절반씩 줄어드므로, nlog₂(n) 을 갖습니다. <br>


<br><br>

# 2. 파이썬 코드



```
def binarySearch(dic, x, dic_origin):
    # 중앙값
    middle = dic[len(dic)//2]
    
    # 중앙값과 x가 같다면 해당 index를 리턴한다
    if middle==x:
        print(dic_origin.index(middle))
        return True   
    
    # 중앙값과 x 크기를 비교하여 재귀적으로 함수를 반복한다
    if (middle<x):
        binarySearch(dic[len(dic)//2+1:], x, dic_origin)
    else:
        binarySearch(dic[:len(dic)//2], x, dic_origin)
```
- dic은 주어진 배열이고, dic_origin도 dic과 동일한 배열입니다.
- 단, dic_origin은 index를 찾기 위해, 자르지 않고, dic만을 자르며 재귀함수를 수행합니다.