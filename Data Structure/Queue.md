## Queue

### 특징

- FIFO : First In First Out
- 배열을 사용할 때와는 달리 특정 인덱스에 접근하지 않는다.
- 데이터를 추가하거나 삭제하는 연산만 가능하다
- 최상위의 항목을 제거하더라도 원소들을 하나씩 옆으로 밀어줄 필요는 없다.

### 구현

```js
class Queue {
  constructor() {
    this.storage = {};
    this.front = 0;
    this.rear = 0;
  }

  size() {
    return this.rear - this.front;
  }

  // 데이터 추가
  enqueue(element) {
    this.storage[this.rear] = element;
    this.rear += 1;
  }

  // 데이터 추출
  dequeue() {
    // 빈 Queue에 대해 dequeue를 적용했을 때의 에러를 방지
    if (this.rear === this.front) {
      return;
    }

    const result = this.storage[this.front];
    delete this.storage[this.front];
    this.front += 1;

    return result;
  }
}
```

### 사용 예시

- 너비 우선 탐색(BFS)

  - 처리햐야할 노드의 리스트를 저장하는 용도로 사용
  - 노드를 하나 처리할 때마다 해당 노드의 인접 노드들을 큐에 다시 저장
  - 노드를 접근 순서대로 처리 가능

- 우선순위가 같은 작업 예약
- 프린터의 출력 처리
