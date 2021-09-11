---
layout: post
title:  "[Algorithm] 3. 선택/삽입 정렬"
subtitle:   "선택/삽입 정렬"
categories: Algorithm
tags: Algorithm
comments: true
date: 2021-09-11 00:19:23
---

<h1>선택/삽입 정렬</h1>

***

파이썬을 이용하여 구현해보겠습니다.<br><br>


## 1. 선택 정렬

```
def selection_sort(L):
    answer = []

    for i in range(len(L)):
        max = 0
        index = -1
        
        for j in range(len(L)):        
            if max<= L[j]:
                max = L[j]
                index = j
        
        # 가장 끝의 수와 나머지 중 가장 큰 수와 교환합니다
        L[index], L[len(L)-1] = L[len(L)-1], L[index]
        
        answer.insert(0, L[len(L)-1])
        # 범위를 하나씩 줄여 나갑니다
        del L[len(L)-1]
        
    return answer
```
범위를 하나씩 줄여가며 정렬합니다. <br>
가장 끝에 있는 수와 나머지 중 가장 큰 수와 교환해나갑니다. <br>

최초 상태: 8 31 48 <strong>73</strong> 3 65 20 <strong>29</strong> <br>
1번째 반복 후: 8 31 48 29 3 <strong>65</strong> <strong>20</strong> 73 <br>
2번째 반복 후: 8 31 <strong>48</strong> 29 3 <strong>20</strong> 65 73  <br>
3번째 반복 후: 8 <strong>31</strong> 20 29 <strong>3</strong> 48 65 73 <br>
4번째 반복 후: 8 3 <strong>20</strong> <strong>29</strong> 31 48 65 73 <br>
5번째 반복 후: <strong>8</strong> 3 <strong>20</strong> 29 31 48 65 73 <br>
6번째 반복 후: <strong>8</strong> <strong>3</strong> 20 29 31 48 65 73  <br>
7번째 반복 후: 3 8 20 29 31 48 65 73 <br>

<br>

## 2. 삽입 정렬

```
def insertion_sort(L):
    answer = []
    
    for j in range(len(L)):
        answer.append(L[j])

        # 역순으로 반복하며 index 끝부터 비교합니다
        for i in range(len(answer)-1,0,-1):

            if answer[i-1] > answer[i]:
                answer[i-1], answer[i] = answer[i], answer[i-1]

            else:
                break
           
    return answer
```

범위를 하나씩 늘려가며 정렬합니다. <br>
가장 끝에 있는 수와 바로 옆의 수와 비교해나가며 적절한 위치를 찾아 삽입합니다. <br>

최초 상태 : <strong>3</strong> 73 48 31 8 11 20 <br>
1번째 반복 후: <strong>3 73</strong> 48 31 8 11 20 <br>
2번째 반복 후: <strong>3 48 73</strong> 31 8 11 20 <br>
3번째 반복 후: <strong>3 31 48 73</strong> 8 11 20 <br>
4번째 반복 후: <strong>3 8 31 48 73</strong> 11 20 <br>
5번째 반복 후: <strong>3 8 11 31 48 73</strong> 20  <br>
6번째 반복 후: <strong>3 8 11 20 31 48 73</strong>
