---
title: 자료구조 3 Queue
date: 2020-12-27 22:52:36
tags: 스터디
---

# queue?

---

<img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2014/02/Queue.png"/>
Queue는 FIFO, 즉 선입 선출형 자료형이다.
the queues of bus stop 즉, 버스정류장에서 따온 queue는 먼저 온 사람(제일 오래 기다린 사람)이 제일 먼저 탄다는 원리를 그대로 따왔다.

데이터를 제일 뒤에 집어넣는 enqueue, 데이터를 제일 앞에서 추출하는 dequeue 등의 작업이 가능하다.
삽입을 하는 enqueue의 경우 O(1), 삭제를 하는 dequeue의 경우 O(1)의 복잡도를 가진다.
접근을 하는 경우 O(n)의 복잡도를 가진다.

---

### use case?

---

즉각적으로 삽입, 삭제가 가능해 많이 사용된다.

- Game servers that pair you up with other users (any networking to handle congestion)
- Any waiting line
- Background tasks
- Printer processes
- Traversing a Binary Search Tree or a Graph

---

### 구현

#### javascript로는 배열을 이용해 아- 주 간단히, pop()과 unshift()로 queue의 핵심 기능을 구현할 수 있다.

#### 그러나 링크드 리스트를 이용해 봄.

1. declare

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class Queue {
  constructor() {
    //data가 따로 없으므로 parameter x
    this.head = null;
    this.tail = null;
    this.length = 0;
  }
}
```

2. enqueue using linked list

```javascript
enqueue(data){
    let node = new Node(data);
    //1. 리스트에 아무것도 없을 경우
    if(!this.head){
        this.head = node;
        this.tail = node;
    } else {
        //2. 뭔가가 있을 경우
        this.tail.next = node;
        this.tail = node;
    }
    this.length ++;
    return this.length;
    // length 반환
}
```

3. dequeue using linked list

```javascript
dequeue(){
    let data = null;
    if(!this.head){

    }else if(this.length === 1){
        data = this.head.data;
        this.head = null;
        this.tail = null;
        this.length--;
    }else{
        data = this.head.data;
        this.head = this.head.next;
        this.length--;
    }
    return data;
}
```
