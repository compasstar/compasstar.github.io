---
layout: post
title:  "[Algorithm] 1. 이진탐색트리 Binary Search Tree"
subtitle:   "이진탐색트리"
categories: Algorithm
tags: Algorithm
comments: true
date: 2021-08-24 00:15:25
---

<h1>Binary Search Tree</h1>

***

이진탐색트리에 대해서 알아보겠습니다. <br>
파이썬을 이용하여 구현해보겠습니다.<br><br>
<b>프로그래머스</b>의 [어서와! 자료구조와 알고리즘은 처음이지?](https://programmers.co.kr/learn/courses/57) 강의를 참고했습니다.<br><br>

<img width = "300" src="https://user-images.githubusercontent.com/55419868/130561781-83270cf7-7fdd-43b6-8f10-e109b10e5725.JPG"/>


이진탐색트리는 위와같이 생겼습니다.<br>
 하나의 노드에서 자기보다 값이 작은 노드는 왼쪽으로, 값이 큰 노드는 오른쪽으로 이어준 모양입니다.<br>
 가장 왼쪽의 노드부터 오른쪽 노드까지 순서대로 보시면, 값이 가장 작은 것부터 가장 큰 것까지 순서대로 나열되어 있습니다.

***

### 이진탐색트리에 다음과 같은 함수들을 작성해 보겠습니다

* insert(key, data) - 트리에 주어진 데이터 원소를 추가
* remove(key) - 특정 원소를 삭제
* lookup(key) - 특정 원소를 검색
* inorder() - 키의 순서대로 데이터 원소 나열
* min, max() - 최소 키, 최대 키를 가지는 원소를 각각 탐색

<i>(key는 노드가 담고 있는 숫자, data는 노드가 담고 있는 데이터를 뜻합니다)</i>
<br><br>

## 1. 초기화 __init__()

```
class Node:
    def __init__(self, key, data):
        self.key = key
        self.data = data
        self.left = None
        self.right = None

class BinSearchTree:
    def __init__(self):
        self.root = None
```
노드와 이진탐색트리의 클래스를 만들어줍니다.<br><br>

## 2. inorder(key)

```
class Node:
    def inorder(self):
            traversal = []
            if self.left:
                traversal += self.left.inorder()
            traversal.append(self)
            if self.right:
                traversal += self.right.inorder()
            return traversal 

class BinSearchTree:
    def inorder(self):
        if self.root:
            return self.root.inorder()
        else:
            return []
```
이진트리의 전위순회의 원리와 동일합니다. <br>
이진탐색트리에서는 가장 왼쪽부터가 가장 크기가 작은 노드이므로, 가장 왼쪽 노드부터 순서대로 `traversal`에 `.append`해주었습니다.<br>
혹시 이해가 잘 되지 않으신 분들은 이진트리의 순회를 먼저 공부하고 오시기 바랍니다.<br><br>

## 3. min(), max()

```
class Node:
    def min(self):
        if self.left:
            return self.left.min()
        else:
            return self
        
    def max(self):
        if self.right:
            return self.right.max()
        else:
            return self

class BinSearchTree:
    def min(self):
        if self.root:
            return self.root.min()
        else:
            return None
        
    def max(self):
        if self.root:
            return self.root.max()
        else:
            None
```
`min()`은 재귀를 이용하여 가장 왼쪽 노드를 찾아주었고, `max()`는 재귀를 이용하여 가장 오른쪽 노드를 찾아주었습니다.<br><br>

## 4. lookup(key)

```
class Node:
    def lookup(self, key, parent=None):
        if key < self.key:
            if self.key.left:
                return self.left.lookup(key, self)
            else:
                return None, None
        elif key > self.key:
            if self.key.right:
                return self.right.lookup(key, self)
            else:
                return None, None
        # key 와 self.key가 같을 경우 (찾고자 하는 노드)
        else:
            return self, parent


class BinSearchTree:
    def lookup(self, key):
        if self.root:
            return self.root.lookup(key)
        else:
            return None, None
```
`lookup(key)`으로 특정 노드와 함께 그 부모 노드까지 찾아주겠습니다. 부모까지 함께 찾는 이유는 `remove(key)`를 할 때 필요하기 때문입니다. <br>
찾고자 하는 `key`값이 현재 노드의 `key`보다 작으면 왼쪽으로 계속 향하고, 크다면 오른쪽으로 향합니다.<br><br>

## 5. insert(key, data)

```
class Node:
    def insert(self, key, data):
        if key < self.key:
            if self.left:
                return self.left.insert(key, data)
            else:
                self.left = Node(key, data)
        elif key > self.key:
            if self.right:
                return self.right.insert(key, data)
            else:
                self.right = Node(key, data)
        # 추가하고자 하는 key가 이미 있다면 Error 발생시키기
        else:
            raise KeyError

class BinSearchTree:
    def insert(self, key, data):
        if self.root:
            return self.root.insert(key, data)
        else:
            self.root = Node(key, data)
```
크기를 비교해 나가며 root부터 leaf까지 나아갑니다. 적절한 위치의 leaf에 도달했다면, 노드를 `insert` 합니다.<br><br>

## 6. remove(key)
```
class Node:
    def countChildren(self):
        count = 0
        if self.left:
            count += 1
        if self.irght:
            count += 1
        return count

class BinSearchTree:
    def remove(self, key):
        node, parent = self.lookup(key)
        if node:
            nChildren = node.countChildren()
            # node에 자식이 없을 경우
            if nChildren == 0:
                if parent:
                    if parent.left == node:
                        parent.left = None
                    elif parent.right == node:
                        parent.right = None
                else:
                    self.root = None
            # node 에 자식이 한쪽만 있을 경우
            elif nChildren == 1:
                if node.left:
                    s = node.left
                else:
                    s = node.right
                if parent:
                    if parent.left == node:
                        parent.left = s
                    elif parent.right == node:
                        parent.right = s
                else:
                    self.root = s
            # node에 자식이 left, right 양 쪽에 있을 때
            else:
                parent = node
                successor = node.right
                while successor.left:
                    parent = successor
                    successor = successor.left
                    
                node.key = successor.key
                node.data = successor.data
                if parent.left == successor:
                    parent.left = successor.right
                #제거하고자 하는 노드의 바로 오른쪽 자식노드가
                #왼쪽 끝 노드일 경우
                elif parent.right == successor:
                    parent.right = successor.right
            return True

        else:
            return False
```
`remove(key)`를 할 때에는 세가지 경우로 나누어 생각해 볼 수 있습니다.

1. 선택한 노드에 자식이 없을 경우
2. 선택한 노드에 자식이 하나 있을 경우
3. 선택한 노드에 자식이 둘 있을 경우

### 1. 선택한 노드에 자식이 없을 경우
> 노드가 부모의 left 에 이어졌는지 right 에 이어졌는지만 확인하여 그 연결을 끊어주면 됩니다.

### 2. 선택한 노드에 자식이 하나 있을 경우
> 노드의 자식을 부모와 연결시켜줍니다. 이 역시 노드가 부모의 left right 어느 쪽에 연결되어 있는 지를 확인하여, 그 방향으로 자식 노드를 이어주면 됩니다.

### 3. 선택한 노드에 자식이 둘 있을 경우

<hr>

이 경우는 조금 복잡해집니다. <br>
아래 이미지에서 7을 remove 한다고 생각해보겠습니다. 

<img width = "300" src="https://user-images.githubusercontent.com/55419868/130561781-83270cf7-7fdd-43b6-8f10-e109b10e5725.JPG"/>

7의 오른쪽 트리를 바라볼 때, 가장 왼쪽에 있는 노드를 찾아줍니다.(8)<br>
8을 7이 있는 곳에 넣어줍니다. 그리고 8의 자식노드를(존재한다면) 8의 부모노드와 연결합니다.

<img width="300" src="https://user-images.githubusercontent.com/55419868/130566099-e70c0a51-dae4-4a87-8520-d1e73cfbb9f6.png"/>





