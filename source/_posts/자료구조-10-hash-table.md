---
title: 자료구조 10 hash table
date: 2021-01-31 23:39:47
tags:
---

## what is hash table?

대부분의 프로그래밍 언어는 <b>해시 테이블</b>이라는 자료구조를 포함한다.
이 해쉬는 굉장히 다양한 이름으로 불리는데,
해시, 해시 맵, 맵, 딕셔너리, 연관 배열 등의 아주 다양한 이름을 갖는다.
어쩐지 해시와 관련된 단어를 많이 듣기는 했는데 서로 차이를 알 수 없다 했더니.. 그냥 똑같은 것들이었다.

---

이 해시 테이블은 쌍으로 이뤄진 값들의 리스트다.
js로 표현해보자면, 객체 let hash = {key: value}로 이뤄졌다고 보면 되겠다.
첫 번째 항목을 키라 부르고, 두 번째 항목을 값이라고 부른다.
<img src="https://adrianmejia.com/images/hashmap-drawer.jpg"/>
해쉬맵, 혹은 해쉬 테이블은 이렇게 일반 통에 라벨을 붙인 것과 같이 생겼다고 이해하면 된다.
굳이 toy를 찾기 위해 다른 서랍을 살펴볼 필요가 없다.
이 라벨은 굳이 말하자면 인덱스의 기능을 한다.
그런데 이렇게 인덱스의 기능을 하게 하려면, 해쉬 함수라고 불리는 함수를 통해야만 한다.

---

<img src ="https://www.notion.so/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2Fe6b44926-e428-4bad-a1ef-998b1a60419a%2FUntitled.png?table=block&id=5ed2c756-7a88-4a64-8bf5-1c147519421d&spaceId=00c0e427-2f8c-4249-93b2-79d7f73ab93c&width=2880&userId=1b74d7d4-6e2e-4bdb-a251-ceed856fd2cc&cache=v2"/>

해시 테이블에서는 키의 값으로 값을 룩업할 수가 있다.
예를 들면, hash[key]가 value라는 값으로 반환된다.
이 탐색은, 딱 한단계만 걸리므로 시간 복잡도가 O(1)이 된다.

2. 해시 함수

이렇게 검색을 빨리할 수 있는 이유는 해싱이라는 과정을 통해 데이터를 효율적으로 관리하고자 했기 때문이다.
즉 해시 테이블은 해싱(hashing)의 결과물이다.

해시테이블은 내부적으로 배열(버킷)을 사용하여 데이터를 저장한다.
key 값에 일정한 해시 함수를 적용하고, 배열의 고유한 index를 생성한다.
그리고 이 index를 활용해 값을 저장하거나 검색한다.
이 실제 값이 적용되는 장소를 버킷이라고 한다.

이렇게 특정 값으로 변환하는 데 사용된 것을 해시 함수라고 부른다.

3. 해시 충돌
   해시 충돌이란, 키가 서로 다른데 같은 value를 가지게 되는 상황을 의미한다.

```javascript
class hashMap {
  constructor(initial = 2) {
    this.buckets = new Array(initial);
  }
  set(key, value) {
    const index = this.getIndex(key);
    this.buckets[index] = value;
  }
  get(key) {
    const index = this.getIndex(key);
    return this.buckets[index];
  }

  hash(key) {
    return key.toString().length;
  }

  getIndex(key) {
    const indexHash = this.hash(key);
    const index = indexHash % this.buckets.length;
    return index;
  }
}
```

이 코드에서 볼 수 있듯,

- 여기에서 너무나도 많은 중복값이 일어날 수 있다. 'bye' 'cat' 'sam' 등 같은 글자 수라면, 많은 충돌이 일어난다.
- 그러나 이 충돌은 어쩔 수 없이 일어나는 것이다. 충돌 자체를 막을수는 없다. 이를 막기위해 체이닝을 시도한다. 그러나, 그럼에도 배열의 사이즈가 2개뿐이 없어서 이 방법도 소용없다.

\*\* 체이닝이란 ?

버켓 내 연결리스트 할당하는 방법을 통해 이 충돌이 발생하면 연결리스트로 데이터를 연결한다.

- 따라서 이를 해결하기 위해서는, 애초에 큰 bucket을 이용하거나ㅡ 적절한 함수를 만드는 것이 중요하다.
