> 늦은 퇴근으로 인해 JS대신 출퇴근길에 읽은 [면접을 위한 cs 전공지식 노트](https://book.naver.com/bookdb/book_detail.nhn?bid=22350247) 내용 중 연결리스트에 대해 정리해봅니다.

# 연결리스트

연결 리스트는 데이터를 감싼 노드를 포인터로 연결해서 공간적인 효율성을 극대화시킨 자료 구조입니다.

> 공간 복잡도
> 프로그램을 실행시켰을 때 필요로 하는 자원 공간의 양

![](https://velog.velcdn.com/images/kbm940526/post/7919d7bf-c1a4-4633-8495-0b276822255b/image.png)

삽입과 삭제가 O(1)이 걸리며 탐색에는 O(n)이 걸리기에 데이터 **삽입과 삭제에 특화**된 자료구조입니다.

## 종류

### 싱글 연결리스트

![](https://velog.velcdn.com/images/kbm940526/post/31341f9e-832d-470b-8421-e972e834bf3c/image.png)

**next** 포인터만 가지며 다음 노드로만 이동합니다.

### 이중 연결 리스트

![](https://velog.velcdn.com/images/kbm940526/post/f6e624ed-bb07-4ee3-a65e-a302a7d2c509/image.png)

**prev**와 **next**를 가지며 다음 노드와 이전 노드로 이동가능합니다.

### 원형 이중 연결 리스트

![](https://velog.velcdn.com/images/kbm940526/post/daf96957-1769-4d14-8949-42199dc373ef/image.png)

이중 연결 리스트와 같지만 마지막 노드의 **next**에서 헤드 노드를 가리키는 것을 말합니다.

## 구현

### 구조

```js
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

### linked list

```js
class LinkedList {
  constructor() {
    this.head = null;
    this.size = 0;
  }

  //처음에 추가
  add(el) {
    const node = new Node(el);

    if (this.head === null) {
      //list없을 때 리스트에 추가하고 헤더를 만듬
      this.head = node;
    } else {
      let currentPlace = this.head;
      while (currentPlace.next) {
        currentPlace = currentPlace.next;
      }
      currentPlace.next = node; // 노드 추가
    }
    this.size++; // 사이즈 업
  }

  //원하는 위치에 추가
  insertAt(el, idx) {
    if (idx < 0 || idx > this.size) {
      return console.log("값을 똑바로 넣어줭");
    } else {
      //인데스를 제대로 넣으면 우선 노드를 만듬

      const node = new Node(el);

      //첫번째 인덱스에면 거기에 추가
      if (idx === 0) {
        node.next = this.head;
        this.head = node;
      } else {
        let curr, prev;
        curr = this.head;
        let it = 0;

        while (it < idx) {
          it++;
          prev = curr;
          curr = curr.next;
        }

        //노드 추가
        node.next = curr;
        prev.next = node;
      }
      this.size++;
    }
  }

  //노드를 삭제합니다.
  removeFrom(idx) {
    if (index < 0 || index >= this.size)
      return console.log("값을 제대로 넣어줭");
    else {
      let curr = this.head;
      let prev,
        it = 0;

      if (idx === 0) {
        this.head = curr.next;
      } else {
        //반복하면서 위치를 하나씩 이동시킨다.
        while (it < idx) {
          it++;
          prev = curr;
          curr = curr.next;
        }

        //노드 삭제
        prev.next = curr.next;
      }
      this.size--;

      return curr.head; // 삭제된 값을 알려주장
    }
  }
}
```
