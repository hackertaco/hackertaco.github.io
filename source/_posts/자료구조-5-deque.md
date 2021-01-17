---
title: 자료구조 5 deque
date: 2021-01-04 23:27:55
tags: 스터디
---

# deque?

 <img src="https://cdn.programiz.com/sites/tutorial2program/files/deque.png" />

큐와 스택을 공부하면서, 큐는 fifo, 스택은 lifo로 데이터들이 움직이는 것을 보았다.
그런데, deque는 앞에도 뒤에서도 데이터가 들어오고 빠져나갈 수 있다고 한다.

---

# possible operations?

---

- add front
- add back
- remove front
- remove back
- select front
- select back
- size
- is empty
- clear

---

# use case?

---

- 최근의 케이스는 undo, history 등에서 많이 쓰인다고.
- 조금 더 과정이 덜한 큐나 스택을 만드는 데 의의가 있지 않을까.

---

# realize deque

1. 클래스 만들기

```javascript
class deque {
  constructor() {
    this.items = {};
    this.size = 0;
    this.smallSize = 0;
  }
}
```

2. add front

```javascript
addBack(data){
    this.items[this.size] = data
    this.size ++
}
```

3. add back

```javascript
addFront(data){
    if(this.isEmpty() === 0){
        addBack(data)
    }else if (this.smallSize > 0){
        this.smallSize--;
        this.items[this.smallSize] = data;
    }else{
        for(let i = this.size; i > 0; i--){
            this.items[this.size] = this.items[this.size - 1]
        }
        this.size++
        this.items[0] = data;
    }
}
```

4. remove front

```javascript
removeFront(){
    if(this.isEmpty() === 0){
        return;
    }

    let result = this.items[this.smallSize];
    delete this.items[this.smallSize];
    this.smallSize++;

}
```

5. remove back

```javascript
removeBack(){
   if(this.isEmpty() === 0){
        return;
    }

    let result = this.items[this.size - 1];
        delete this.items[this.size - 1];
        this.size--;
}
```

6. is empty?

```javascript
isEmpty(){
    return this.length() === 0
}
```

7. length

```javascript
length(){
    return this.size - this.smallSize
}
```
