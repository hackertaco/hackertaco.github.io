---
title: 자료구조 9 binary search tree
date: 2021-01-18 01:24:04
tags:
---

일전에 binary tree 구조를 다룬 적이 있다.
이름도 비슷한 binary search tree는, 각 노드가 root에서부터 leaf까지 정렬이 되어있는 구조다.

이 bst는, (줄여 말하겠음) 이진 탐색과 연결 리스트를 결합한 구조로, 이진탐색의 효율적인 탐색 능력을 유지하고, 연결리스트의 장점인 삽입과 삭제가 빠르게 진행되도록 한다.
힙이랑 비슷한듯 한데, 힙은 자식노드보다 부모 노드가 무조건 크거나(최대힙) 무조건 작은(최소힙) 특징을 가지고 있으나, bst의 경우는 왼쪽 자식이 제일 작고, 부모가 그 다음으로 크고, 오른쪽 자식이 제일 큰.. 다소 신기한 구조를 가지고 있다.

따라서, 힙은 우선순위 정렬에, bst는 탐색에 강점이 있다고들 합니다.

## 이진 탐색 use case

- 데이터 검색
- 부수적인 알고리즘이나 자료구조 생성

## 이진 탐색의 구현

```javascript
//1. node 선언
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  //2. insert
  insert(value) {
    let newNode = new Node(value);
    if (this.root === null) {
      this.root = newNode;
    }
    let current = this.root;
    while (current) {
      if (value === current.value) return undefined;
      if (value < current.value) {
        if (current.left === null) {
          current.left = newNode;
        }
        current = current.left;
      } else {
        if (current.right === null) {
          current.right = newNode;
        }
        current = current.right;
      }
    }
  }

  find(value) {
    if (!root) return false;
    let current = this.root;
    let found = false;
    while (current && !found) {
      if (value < current.value) {
        current = current.left;
      } else if (value > current.value) {
        current = current.right;
      } else {
        found = current;
      }
    }
    return found;
  }
}
```
