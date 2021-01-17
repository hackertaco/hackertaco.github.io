---
title: 자료구조 2. doubly linked list, circular linked list
date: 2020-12-24 14:05:42
tags:
---

# doubly linked list

---

일반 연결 리스트가 next 포인터를 하나만 가지고 있어서 일방향이었다면,
doubly linked list는 양방향! 2개의 연결 포인트를 가지고 있다.

---

### use case ?

그런데 말입니다. doubly linked list는 실제로 어디에 쓰일까.
뭐 뒤로가기 이런 거 할 때 쓰이나?

찾아보니, <a href="https://codeforwin.org/2015/10/doubly-linked-list-data-structure-in-c.html">(출처)</a>
생각보다 다양한 부분에 쓰이고 있었다.

- 네비게이션의 앞과 뒤를 표현할 때.
- 뒤로가기, 앞으로 가기 (브라우저)
- undo redo
- 게임 패
- 게임의 여러 상태를 표현할 때

여튼 앞에서 뒤를 기억해야 하는 일이 있는 경우, 자주 사용되는 것으로 보인다.

### 구현

1. node class

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
    this.prev = null;
  }
}
```

2. create node

- head, tail 선언

```javascript
const head = new Node(1);
const secondNode = new Node(2);
head.next = secondNode;
secondNode.prev = head;

const tail = secondNode;
```

- 이렇게 선언한 걸로 순회 가능!

```javascript
//head에서 순회
let current = head;

while (current !== null) {
  current = current.next;
}
```

```javascript
let current = tail;

while (current !== null) {
  current = current.prev;
}
```

3. list create

- 이렇게 만든 node들로, doubly linked list class를 만들어볼 수 있다.
- 함께 list 에 data를 추가, 삭제, 검색 등이 가능하다.

```javascript
const head = Symbol("head");
const tail = Symbol("tail");

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  // 1. add data O(1), 아무 순회도 하지 않으므로 !
  add(data) {
    const firstNode = new Node(data);

    if (this.head === null) {
      this.head = firstNode;
    } else {
      this.tail.next = firstNode;
      firstNode.prev = this.tail;
      //tail과 연결
    }
    // tail에 재할당
    this.tail = firstNode;
  }

  //2. get data O(n),

  get(index) {
    if (index > -1) {
      let current = this.head;
      let i = 0;
      while (current !== null && i < index) {
        current = current.next;
        i++;
      }

      return current !== null ? current.data : undefined;
    } else {
      return undefined;
    }
  }

  //3. remove data in list O(n)
  remove(index) {
    if (this.head === null || index < 0) {
      throw new RangeError(`Index ${index} does not exist in the list.`);
    }
    if (index === 0) {
      this.head = this.head.next;
      if (this.head === null) {
        this.tail = null;
      } else {
        this.head.prev = null;
      }
    }
    let current = this.head;
    let i = 0;
    while (this.head !== null && index > i) {
      current = current.next;
      i++;
    }

    if (current !== null) {
      current.prev.next = current.next;
      if (this.tail === current) {
        this.tail = current.prev;
      } else {
        current.next.prev = current.prev;
      }
    }
  }
}
```

# 원형 연결리스트

---

다른 연결 리스트와 다른 점이라고 하면, data 값에 Null이 없다는 점 !
tail data의 next가 head를 가리키기 때문이다.
데이터들끼리 원형을 그려 원형 연결리스트라고 한다. 끝이 없음 !
양방향, 단방향 모두 구현 가능하다.

---

### 이용 시 장점

- 모든 리스트가 어디서든 순회 가능
- 단방향이더라도 우리는 이전 노드로 갈 수 있다.

### 이용 시 단점

- 상대적으로 거꾸로 가는 것이 복잡
- 제대로 조정하지 않으면 무한 루프
- 즉각적인 데이터 접근 불가 (다른 리스트처럼)

### use case

- OS에서 사용. 다양한 어플리케이션 이용을 위해.
- round robin처럼 시간 매커니즘에 사용
- 돌아가면서 하는 멀티플레이어 게임에 사용.

### 구현

- 단방향, 원형 연결 리스트로 만들어보겠다.
- circular list를 위한 node가 정의되어있다고 가정 후

```javascript
//tail이 없다 !

class CircularList{
    const head = Symbol('head');
    constructor(){
        this.head = null;
        this.length = 0;
    }

    push(data){
        //끝에 집어넣는 것. 아예 head 가 null인 경우가 있고 아닌 경우가 있다.
        const newNode = new Node(data);

        if(this.head === null){
            this.head = newNode;
            newNode.next = this.head;
        }else{
            // 끝을 찾아야.
            let current = this.head
            while(current !== null){
                current = current.next;

            }
           current = newNode;
           this.length++
           newNode.next = this.head;

        }
    }

    insert(data, index){
        // 중간에 끼워넣는 것
        if(index >= 0 && index <= this.length){
            const newNode = new Node(data);
            let current = this.head;
            if(index === 0){
                if(this.head === null){
                    this.head = newNode;
                    newNode.next = this.head;
                }else{
                    this.head.next = current;
                    this.head = newNode
                };
            }else if(index == this.length -1){
                while(current !== null){
                    current = current.next
                }
                current = newNode;
                current.next = this.head

            }else{
                let target = get(index-1);
                current = target.next;
                target.next = newNode;
                newNode.next = current

            }
            this.length++
        }


    }

    get(index){
        let counter = 0;
        let current = this.head;

        while(counter < index){
            current = current.next;
            counter++
        }

        return current

    }

    removeAt(index){
        if (index >= 0 && index < this.length) {
            if (this.head === null) {
                return null
            }
            let current = this.head;
             if (index == 0) {
                 this.head = current.next;
             } else if(index == this.length-1) {
                let target = get(index-1)
                 current = target.next;
                 target.next = this.head;
             }else{
                let target = get(index - 1);
                current = target.next;
                target.next = current.next;
             }

             this.length --;

         }
    }
}
```
