---
layout: post
title:  "[Algorithm] 6. 퀵정렬"
subtitle:   "퀵 정렬"
categories: Algorithm
tags: Algorithm
comments: true
date: 2021-11-02 00:21:27
---

# 1. 퀵 정렬의 원리
<br>

## [개념]

- 배열을 left, middle, right 로 나누어가며 정렬해 나갈 것입니다.<br>
- left, right 자체적으로는 배열이 안되어있지만, left는 middle 보다는 작은 원소들로 구성되어 있고, right는 middle 보다는 큰 원소로 구성되게 만들 것입니다.<br>
- 배열의 크기가 1이 될 때까지 나누어가면 모든 원소가 정렬이 되게 됩니다.
<br><br>

## [예시]
<br>

[4 5 3 1 2]<br>
> 배열에서 중앙 인덱스에 있는 원소를 pivot으로 삼습니다.<br>
>  (꼭 중앙일 필요는 없습니다. 원소의 크기가 배열 중에 가장 크거나 가장 작으면 비효율적이 됩니다.)

[4 5 1 2 : 3]
> pivot을 배열의 끝으로 이동시킵니다.

[<b>4</b>(low) 5 1 <b>2</b>(high) : 3]
> - pivot을 제외하고 가장 왼쪽 인덱스를 low, 가장 오른쪽 인덱스를 high 로 여깁니다. <br>
> - 만약 low가 pivot 보다 작다면 오른쪽으로 한칸씩 이동하고, pivot보다 크다면 해당 원소를 선택합니다.
> - 만약 high가 pivot 보다 크다면 왼쪽으로 한칸씩 이동하고, pivot보다 작다면 해당 원소를 선택합니다.
> - low, high 가 서로 선택한 원소의 위치를 바꿉니다.
> - low 가 high 보다 앞설 때까지 반복합니다.

[2 <b>5</b>(low) <b>1</b>(high) 4 : 3]

[2 <b>1</b>(high) <b>5</b>(low) 4 : 3]
> low가 high를 앞섰으니 반복을 종료합니다

[2 1 3 5 4]
> pivot 을 가운데에 넣어줍니다

[2 1] [3] [5 4]
> - pivot 보다 작은 원소들을 left 배열로 만들고, 큰 원소들을 right 배열로 만듭니다.
> - left 배열에서 위의 과정을 반복합니다.
> - right 배열에서 위의 과정을 반복합니다.
> - 계속 반복해서 원소의 크기가 1이 된다면 정렬이 완료됩니다.

<br><br>

## [시간복잡도]

![그림1](https://user-images.githubusercontent.com/55419868/136515690-1989af65-3757-4bdc-89fd-ed56afc3546b.png)

>시간 복잡도는 nlog₂(n) 을 갖습니다. <br>
>하나의 줄 당 n 번의 정렬을 해야하고, 세로로 log₂(n) 개의 노드가
 있으니,<br> nlog₂(n) 입니다. 


<br><br>

# 2. 파이썬 코드


<br><br>


# 2-1. find_pivot_index()

```
def find_pivot_index(array):
    
    if len(array)<3:
        return False 
    middle = array[len(array)//2]   

    index_list = list(filter(lambda x: array[x] == middle, range(len(array))))

    return index_list
```
- 배열의 중앙에 있는 값을 선택하여, 배열에서 그와 동일한 값을 갖는 원소들의 인덱스들을 리턴합니다.
- 해당 원소가 배열에서 중복해서 있을 수 있기 때문에 `index_list`의 길이는 길어질 수 있습니다.
- 해당 함수는 간단해서 따로 만들지 않기도 합니다.

<br><br>

# 2-2. partition()

```
def partition(array, pivot_index):
    
    
    # 피벗을 배열의 맨 뒤로 보낸다
    for i in range(len(pivot_index)-1,-1,-1):
        tempt = array.pop(pivot_index[i])
        array.append(tempt)
        i += 1
    
    # 크기 별로 분류하기
    low = 0
    high = len(array) -1 -len(pivot_index)
    pivot = array[-1]
    

    # 분류시작
    while low<high:
        
        while array[low]<pivot:
            low += 1
            
        while array[high]>pivot:
            high -= 1
            
        if low < high:    
            array[low], array[high] = array[high], array[low]
            low, high = low+1, high-1

# pivot 집어넣기
    
    # 예외 처리
    if low==high:
        if pivot >array[low]:
            for repeat in range(len(pivot_index)):
                tempt = array.pop()
                array.insert(low+1, tempt)
                
            return array[0:low+1], array[low+1:low+1+len(pivot_index)], array[low+1+len(pivot_index):]
        else:
            for repeat in range(len(pivot_index)):
                tempt = array.pop()
                array.insert(low, tempt)
                
        
            
    else:
        for repeat in range(len(pivot_index)):
            tempt = array.pop()
            array.insert(low, tempt)
        
    return array[0:low], array[low:low+len(pivot_index)], array[low+len(pivot_index):]
```
- 피벗을 배열의 맨 뒤로 보냅니다.
- low를 오른쪽으로, high를 왼쪽으로 향하며 pivot 보다 크냐 작냐 정도로 정렬합니다.
- left middle right 로 분류된 것을 리턴합니다.

<br><br>



# 2-3. quick_sort()

```
def quick_sort(array):
    
    # 예외처리 (배열의 크기가 3보다 작을 때)
    if len(array) <= 1:
        return array

    elif len(array) == 2:
        if array[0]>array[1]:
            array[0], array[1] = array[1], array[0]
        return array
    
    pivot_index = find_pivot_index(array)
    
    left_array, middle_array, right_array = partition(array, pivot_index)

    return quick_sort(left_array) + middle_array + quick_sort(right_array)
```

- pivot을 구하고 partition을 통해 left, middle, right 3개의 배열로 나누어 줍니다.
- 재귀를 통해 left, right에서 계속 `quick_sort()`를 반복한 후, 전부 다 더해서 하나의 배열로 합쳐줍니다.
- 정렬 된 배열이 리턴됩니다.

<br><br>

# 2-4. 전체코드

```
def find_pivot_index(array):
    
    if len(array)<3:
        return False 
    middle = array[len(array)//2]   

    index_list = list(filter(lambda x: array[x] == middle, range(len(array))))

    return index_list


def partition(array, pivot_index):
    
    
    # 피벗을 배열의 맨 뒤로 보낸다
    for i in range(len(pivot_index)-1,-1,-1):
        tempt = array.pop(pivot_index[i])
        array.append(tempt)
        i += 1
    
    # 크기 별로 분류하기
    low = 0
    high = len(array) -1 -len(pivot_index)
    pivot = array[-1]
    

    # 분류시작
    while low<high:
        
        while array[low]<pivot:
            low += 1
            
        while array[high]>pivot:
            high -= 1
            
        if low < high:    
            array[low], array[high] = array[high], array[low]
            low, high = low+1, high-1

# pivot 집어넣기
    
    # 예외 처리
    if low==high:
        if pivot >array[low]:
            for repeat in range(len(pivot_index)):
                tempt = array.pop()
                array.insert(low+1, tempt)
                
            return array[0:low+1], array[low+1:low+1+len(pivot_index)], array[low+1+len(pivot_index):]
        else:
            for repeat in range(len(pivot_index)):
                tempt = array.pop()
                array.insert(low, tempt)
                
        
            
    else:
        for repeat in range(len(pivot_index)):
            tempt = array.pop()
            array.insert(low, tempt)
        
    return array[0:low], array[low:low+len(pivot_index)], array[low+len(pivot_index):]


def quick_sort(array):
    
    # 예외처리 (배열의 크기가 3보다 작을 때)
    if len(array) <= 1:
        return array

    elif len(array) == 2:
        if array[0]>array[1]:
            array[0], array[1] = array[1], array[0]
        return array
    
    pivot_index = find_pivot_index(array)
    
    left_array, middle_array, right_array = partition(array, pivot_index)

    return quick_sort(left_array) + middle_array + quick_sort(right_array)
```

