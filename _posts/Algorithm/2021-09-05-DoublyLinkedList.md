---
layout: post
title:  "[Algorithm] 2. 이중연결리스트 DoublyLinkedList"
subtitle:   "이중연결리스트"
categories: Algorithm
tags: Algorithm
comments: true
date: 2021-09-05 00:22:32
---

<h1>이중연결리스트</h1>

***

이중연결리스트에 대해서 알아보겠습니다. <br>
파이썬을 이용하여 구현해보겠습니다.<br><br>


### 이중연결리스트에 다음과 같은 함수들을 작성해 보겠습니다


* traverse() - 리스트를 순회하며 출력한다
* getAt(position) - 리스트의 position 번째에 위치한 node 를 리턴한다
* insertAt(position, newNode) - 리스트의 position 번째에 insertAfter 함수를 실행시켜 노드를 추가시킨다
* insertAfter(self, prev, newNode) - insertAt 에서 받은 위치를 토대로 새로운 노드를 추가한다
* deleteAt(position) - 리스트의 position 번째에 deleteAfter 함수를 실행시켜 노드를 삭제한다
* deleteAfter(prev) - deleteAt 에서 받은 위치를 토대로 원하는 노드를 삭제한다


***

## 1. 초기화 __init__()

```
class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None

class DoublyLinkedList:
    def __init__(self):
        self.header = Node(None)
        self.trailer = Node(None)
        self.trailer.prev = self.header
        self.header.next = self.trailer
        self.nodeCount = 0
```
노드와 이중연결리스트의 클래스를 만들어줍니다.<br>
헤더와 트레일러를 만들어 주겠습니다.<br><br>

## 2. traverse()

```
class DoublyLinkedList:
    def traverse(self):
        entry_list = list()
        curr = self.header
 
        while curr.next.next:
            curr = curr.next
            entry_list.append(curr.data)
        
        for i in entry_list:
            print(i, end="")
```
새로 빈 리스트를 만들어 줍니다. `header`부터 `next` 해나가며 리스트에 추가시켜줍니다.<br><br>

## 3. getAt(position)

```
class DoublyLinkedList:
    def getAt(self, position):
        # 예외처리
        if (position>self.nodeCount) or (position<0):
            print("invalid position")
            return
        
        node = self.header
        i = 0
        while i<position:
            node = node.next
            i += 1
            
        return node
```
찾고자 하는 범위가 이중연결리스트를 넘어가면 예외처리를 해줍니다<br>
`header`부터 출발하여 `position` 만큼 `next` 해주어 원하는 노드에 다다르면 `return` 해줍니다
<br>

## 4. insert()

```
class DoublyLinkedList:
    def insertAt(self, position, newNode):
        # 예외처리
        if position<1 or position > self.nodeCount+1:
            print("invalid position")
            return False
        prev = self.getAt(position-1)
        return self.insertAfter(prev, newNode)
        
    def insertAfter(self, prev, newNode):
        next = prev.next
        next.prev = newNode
        newNode.next = next
        newNode.prev = prev
        prev.next = newNode

        self.nodeCount += 1
```
범위 바깥은 예외처리를 해줍니다. <br>
포지션 하나 뒤의 노드를 기준으로 하여 새로운 노드를 집어넣어 줍니다.
<br><br>

## 5. delete()

```
class DoublyLinkedList:
    def deleteAt(self, position):
        # 예외처리
        if position<1 or position> self.nodeCount:
            print("invalid position")
            return False
        else:
            prev = self.getAt(position-1)
            return self.deleteAfter(prev)
    
    def deleteAfter(self, prev):
        next = prev.next.next
        next.prev = prev
        prev.next = next
        
        self.nodeCount -= 1
```
범위 바깥은 예외처리 해줍니다<br>
원하는 포지션 하나 뒤를 `prev` 로 기준삼아 원하는 노드를 제거해줍니다.
<br>

