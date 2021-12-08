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

  // 가장 앞 원소를 반환(Queue에서 제거하진 않음)
  front() {
    return this.storage[this.front];
  }

  // Queue가 비어있는지 아닌지를 판단
  isEmpty() {
    return this.storage.length === 0;
  }

  // Queue의 길이를 반환
  size() {
    return this.storage.length;
  }

  // Queue내의 모든 원소를 제거
  clear() {
    this.storage = [];
  }

  // Queue의 내용물들을 출력
  print() {
    console.log(this.storage.toString());
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

## Priority Queue (우선순위 큐)

- 기존 Queue와 원소가 우선순위에 따라 추가되고 삭제되는 점이 다름

### 구현

- 우선순위를 결정하여 원소를 정확한 위치에 추가하는 부분만 작성
- 작성한 부분 이외의 메소드들은 기존 Queue와 동일함

```js
class PriorityQueue() {
  constructor() {
    this.arr = [];
  }

  class QueueElement(element, priority) {
    this.element = element;
    this.priority = priority;
  }

  enqueue(element, priority) {
    const queueElement = new QueueElement(element, priority);

    if(this.arr.isEmpty()) {
      this.arr.push(queueElement);
    } else {
      let added = false;
      for(let i = 0; i<this.arr.length; i++) {
        if(queueElement.priority < this.arr[i].priority) {
          this.arr.splice(i,0,queueElement);
          added=true;
          break;
        }
      }
      if(!added) {
        this.arr.push(queueElement);
      }
    }
  }
}
```
