---
title: 자료구조 4 stack
date: 2020-12-28 14:19:04
tags: 스터디
---

# stack?

---

<img src="https://miro.medium.com/max/900/1*Bh6Vm9QFj7PfCRw1_0r8Tw.png" />

자료의 입출력이 한 방향에서만 이루어진다.
queue와 같이 선형적 구조를 가지지만, 다른 부분이 있다.
데이터를 삭제하는 순서가 다르다!
LIFO 제일 마지막에 들어간 요소를 제일 먼저 빼는!

- queue와 비슷하게, 데이터를 제일 뒤에 집어넣는 삽입, 뒤에서 빼는 삭제 등의 작업이 가능하다.
  삽입을 하는 enqueue의 경우 O(1), 삭제를 하는 dequeue의 경우 O(1)의 복잡도를 가진다.
  접근을 하는 경우 O(n)의 복잡도를 가진다.

---

### use case?

---

즉각적으로 삽입, 삭제가 가능해 많이 사용된다.

- JavaScript call stack
- Applications that implement undo/redo
- Applications that include recently used
- Any data that needs to be handled with Last In First Out logic

---

### 구현

#### javascript로는 배열을 이용해 아- 주 간단히, shift()과 unshift(), 혹은 push() pop()으로 queue의 핵심 기능을 구현할 수 있다.

#### 그러나 링크드 리스트를 이용해 봄.

#### shift()와 unshift()개념으로 기능을 구현할 것. 그 이유는 linked list에는 next만 있고 previous는 없기 때문에, pop()을 구현할 경우 O(n)이 나온다.

1. declare

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class Stack {
  constructor() {
    //data가 따로 없으므로 parameter x
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
}
```

2. unshift using linked list

```javascript
unshift(data){
    let node = new Node(data);

    if(!this.head){
        this.head = node;
        this.tail = node;
    }else{
        node.next = this.head
        this.head = node
    }
    this.length ++;
    return this.length;
}
```

3. shift using linked list

```javascript
shift(){
    let data = null;

    if(!this.head){

    }else if(this.length === 1){

        this.head = null;
        this.tail = null;
        this.length--;
    }else{

        this.head = this.head.next;
        this.length --;
    }
}
```
