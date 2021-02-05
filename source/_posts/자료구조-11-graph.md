---
title: 자료구조 11 graph
date: 2021-01-31 23:40:05
tags:
---

## 그래프는 무엇일까?

그래프는 하나의 점, 그리고 그 점들을 연결하는 선들의 집합이다.
우리가 이전에 본 트리도 이 그래프의 일종이다.
다만, 그래프는 보다 넓은 의미에서, 꼭 정점이라고 일컬어지는 점이 선으로 연결될 필요는 없다.
또한 트리와는 다르게 그래프에 꼭 루트가 있을 필요도, 부모나 자식의 개념이 있을 필요도 없다.
그만큼 상당히 유연한 자료구조.

이 그래프를 네트워크 구조라고 부르는 것도 이때문인 것 같다.

<img src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F97cfbe0b-3001-47e7-9980-d9208c5101eb%2FUntitled.png?table=block&id=ad32a006-9d55-414d-86cc-21830fd30fa1&spaceId=00c0e427-2f8c-4249-93b2-79d7f73ab93c&width=2880&userId=1b74d7d4-6e2e-4bdb-a251-ceed856fd2cc&cache=v2"/>

<img src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F1d5ab396-c8f8-4a6c-a727-633f1b8f31cf%2FUntitled.png?table=block&id=128d52ea-5423-45d2-85e2-fdbbc38f61a2&spaceId=00c0e427-2f8c-4249-93b2-79d7f73ab93c&width=2880&userId=1b74d7d4-6e2e-4bdb-a251-ceed856fd2cc&cache=v2"/>

<img src="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fce16787e-cdf3-4de5-add8-2d69107b1af1%2FUntitled.png?table=block&id=a035a6e5-f55f-431d-a14f-c97c4e001e38&spaceId=00c0e427-2f8c-4249-93b2-79d7f73ab93c&width=2880&userId=1b74d7d4-6e2e-4bdb-a251-ceed856fd2cc&cache=v2"/>

## 그래프 표현 방법 : 인접리스트와 인접매트릭스

1. 인접 매트릭스

행렬은 모든 노드를 가로 혹은 세로로 나열한다.
인접 행렬의 연결을 찾는 데에는 O(1)의 시간 복잡도가 소요되지만,
공간 복잡도는 O(n2)이 든다.
n은 여기서 노드의 수다.
노드를 추가하게 되면? O(n2)가 또 든다.

2. 인접 리스트

가장 일반적으로 그래프를 나타내는 방법.
구현하는 데는 해쉬맵을 주로 사용하고 있다.

```javascript
const graph = {
  a: ["a", "b"],
  b: ["c"],
  c: ["d"],
  d: ["b", "c"],
};
```

노드를 추가하기 위해서?

혹은 삭제하기 위해서? 는 이 방법은 효율적이지는 않다. 왜냐하면, 우리는 b 노드를 삭제하기 위해 b뿐 아니라 다른 b와 연결돼있는 것도 삭제해야하기 때문이다.

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.adjacents = [];
  }
  addAdjacent(node) {
    this.adjacents.push(node);
  }
  removeAdjacent(node) {
    const index = this.adjacents.indexOf(node);
    if (index > -1) {
      this.adjacents.splice(index, 1);
      return node;
    }
  }
  getAdjacents() {
    return this.adjacents;
  }

  isAdjacent(node) {
    return this.adjacents.indexOf(node) > -1;
  }
}
```

이렇게 정점(노드) 클래스를 만들어놓고, 이들이 서로 엮인 그래프를 만든다.

3. BFS와 DFS

- 인접 노드먼저 방문하기 위한 것, 너비 우선(BFS), queue이용

- 한개의 노드의 가장 깊은 곳까지 가는 DFS, stack 이용
