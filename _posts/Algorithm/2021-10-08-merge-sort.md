---
layout: post
title:  "[Algorithm] 5. 합병정렬 (merge sort)"
subtitle:   "합병 정렬"
categories: Algorithm
tags: Algorithm
comments: true
date: 2021-10-08 00:15:56
---

<h1>합병 정렬 [merge sort]</h1>

합병 정렬은 리스트를 전부 조각조각 내어 분리한 후, 하나씩 합치면서 정렬하는 방식입니다. <br><br>

![그림1](https://user-images.githubusercontent.com/55419868/136515690-1989af65-3757-4bdc-89fd-ed56afc3546b.png)

>시간 복잡도는 nlog(n) 을 갖습니다. <br>
>하나의 줄 당 n 번의 정렬을 해야하고, 세로로 log(n) 개의 노드가
 있으니,<br> n * log(n) 입니다. 

<br>
단일연결리스트를 활용하여 노드들을 연결하여 사용하겠습니다.<br>

<br>

합병 정렬에서 사용되는 함수를 알아보겠습니다.<br>
- mergeSort(L)
- merge(L1, L2)
- mg_partition(L1, k)

<br><br>


# 1. mergeSort(L)

```
def mergeSort(L):
    
    # 재귀 호출
    if L.nodeCount > 1:
        L1, L2 = mg_partition(L,int(L.nodeCount/2))
        L1 = mergeSort(L1)
        L2 = mergeSort(L2)
        
        L = merge(L1, L2) # 합쳐진 L을 return

    return L
```

`mg_partition`을 사용하여 `L1` ,`L2` 로 나누고, 재귀 호출을 사용하여 계속해서 리스트에 하나의 노드만 남을 때까지 분리합니다. <br>
그 후, `merge` 를 이용하여 분리된 `L1` `L2` 를 정렬하여 합쳐줍니다.

<br><br>





# 2. merge(L1, L2)

```
def merge(L1, L2):
        pos = 1
    
    while (pos<=L1.nodeCount) and (L2.nodeCount > 0):    
        if L1.getAt(pos).data <= L2.head.data:
            pos += 1
                        
        else:
            newNode = Node(L2.head.data)
                        
            L1.insertAt(pos, newNode)
            L2.popAt(1)
            
            pos += 1
            
    while L2.nodeCount > 0:
        
        newNode = Node(L2.head.data)
        
        L1.insertAt(L1.nodeCount+1, newNode)
        L2.popAt(1)
    
    return L1
```

L1과 L2의 노드들을 비교해가며 크기에 맞추어 L2의 헤드를 차례로 L1으로 연결합니다. <br>
결국 L2의 모든 노드들이 L1으로 이동하게 됩니다. 그러면 정렬된 L1을 리턴합니다. <br><br>



# 3. mg_partition(L1, k)

```
def mg_partition(L1, k):
    
    L2 = SinglyLinkedList()
    
    for i in range(k):
        newNode = L1.popAt(1)
        L2.insertAt(L2.nodeCount+1, newNode)
    
    return L1, L2
```
L1을 두개의 연결리스트로 분리합니다. k는 L2의 노드 개수입니다.

<br><br>

# 전체코드

```
class Node():
    
    def __init__(self, item):
        self.data = item
        self.next = None

        
class SinglyLinkedList():
    
    def __init__(self):
        self.head = Node(None)
        self.tail = Node(None)
        self.nodeCount = 0
        
        
    def getAt(self, pos):
        if pos < 1 or pos > self.nodeCount:
            return None
        
        i = 1
        curr = self.head
        while i < pos:
            curr = curr.next
            i += 1
        
        return curr
    
    
    def insertAt(self, pos, newNode):
        if pos<1 or pos>self.nodeCount+1:
            return False
        
        
        if pos == 1:
            newNode.next = self.head
            self.head = newNode
            
        else:
            
            if pos == self.nodeCount+1:
                prev = self.tail
                
            else:
                prev = self.getAt(pos-1)

            newNode.next = prev.next
            prev.next = newNode
            
        if pos == self.nodeCount+1:
            self.tail = newNode

        self.nodeCount += 1
        
        return True
    
    
    def popAt(self, pos):
        if pos<1 or pos>self.nodeCount:
            return False
        
        curr = self.getAt(pos)
        prev = self.getAt(pos-1)
        
        if self.nodeCount==0:
            self.head=None
            self.tail=None
        
        if pos == 1:
            self.head = curr.next

        elif pos == self.nodeCount:
            prev.next = None
            sefl.tail = prev
            
        else:
            prev.next = curr.next
        
        self.nodeCount -= 1
        return curr
        
    
    def traverse(self):
        curr = self.head
        
        while curr.data != None:
            print(curr.data, end=" ")
            curr = curr.next
        
        return True

###################################################
    
# 합병 정렬 함수
def mergeSort(L):
    
    # 재귀 호출
    if L.nodeCount > 1:
        L1, L2 = mg_partition(L,int(L.nodeCount/2))
        L1 = mergeSort(L1)
        L2 = mergeSort(L2)
        
        L = merge(L1, L2) # 합쳐진 L return
    
    
    return L

# 두 연결리스트를 하나로 합친다.
def merge(L1, L2):
    
    pos = 1
    
    while (pos<=L1.nodeCount) and (L2.nodeCount > 0):
        
        if L1.getAt(pos).data <= L2.head.data:
            pos += 1
                        
        else:
            newNode = Node(L2.head.data)
                        
            L1.insertAt(pos, newNode)
            L2.popAt(1)
            
            pos += 1
            
    while L2.nodeCount > 0:
        
        newNode = Node(L2.head.data)
        
        L1.insertAt(L1.nodeCount+1, newNode)
        L2.popAt(1)
    
    return L1


# 크기 k와 ILI- k 크기로 분할
def mg_partition(L1, k):
    
    L2 = SinglyLinkedList()
    
    for i in range(k):
        newNode = L1.popAt(1)
        L2.insertAt(L2.nodeCount+1, newNode)
    
    return L1, L2
```

