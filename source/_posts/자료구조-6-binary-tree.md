---
title: 자료구조 6 binary tree
date: 2021-01-07 00:30:54
tags:
---

# binary tree?

---

binary tree는 root 라고 불리는 제일 꼭대기의 노드가 조상이라 가정하고, 그 조상으로부터 두명의 아이가 항상 태어나는 형태라고 생각하면 된다. 조상은 하나지만,, 끝은 2배씩 늘어난 자식들로 가득하다 ! 한 노드 당 최대 두명의 자식을 가질 수 있는데, 우리는 이를 각각 left와 right라고 부른다.

만일 이들이 자식이 없으면, 최 하단, 이파리라 불린다.

---

# Use case?

실은 binary tree 자체로 실 사용 케이스에 적용되는 것은 아니라 할 수 있다. 그 까닭은, 만약 이 트리가 랜덤한 순서대로 구성되어 있다면, linked list와 별반 다르지 않는 복잡도를 가지기 때문이다. 따라서, binary tree는 잘 정렬되지 않으면 별 소용이 없다. 다만, 이진 탐색 트리나 heap 등에서 많이 응용되는 자료구조다.

# Big O

- insertion: O(1)
- Deletion: O(n)
- Search: O(n)

삭제하거나, 노드를 탐색하는 경우 ! 자식을 차례대로 탐색하면서 내려가야 한다. 그 이유는 아무런 sorting이 돼있지 않기 때문.
최악의 경우 이파리에 위치하지... 따라서 O(n)

# Realization

- binary tree는 종류가 생각보다 다양하다.
- 모든 부모 노드에 자식이 2개씩 꽉꽉 들어차 있으면 그건 완전 이진트리.
- 그게 아니고 조금 편향돼있으면 편향 트리...

```javascript
// 1. node class 선언
class Node {
	constructor(data) {
		this.data = data;
		this.left = null;
		this.right = null;
	}
}

// 2. tree class 선언
class BinaryTree {
	constructor(){
		this.root = null;
	}
}

// 3. 삽입을 시작하지

insert(data){
	let newNode = new Node(data);
	if(this.root === null){
		this.root = newNode;
	}

	let curr = this.root;
traverse(curr)

}

//4. 사실은 순회부터 먼저 해야 했다.
traverse(root){

	if(root == null){
		return;
	}
	traverse(root.left)
	traverse(root.right)
}
```
