## Stack

### 특징

- 가장 나중에 넣은 데이터를 가장 먼저 뺄 수 있는 구조
- LIFO : Last In First Out, FILO : First In Last Out (<=> [Queue](https://github.com/Soujiro-a/TIL/blob/main/Data%20Structure/Queue.md))
- 배열을 사용할 때와는 달리 특정 인덱스에 접근하지 않는다.
- 데이터를 추가하거나 삭제하는 연산만 가능하다
  - push : 데이터를 Stack에 넣는 기능
  - pop : 데이터를 Stack에서 꺼내는 기능

### 구현

```js
class Stack {
  // 초기 값 섫정
  constructor() {
    this.arr = [];
    this.idx = 0;
  }

  // 데이터 추가
  push(item) {
    this.arr[this.idx] = item;
    this.idx++;
  }

  // 데이터 추출
  pop() {
    // 빈 Stack에 대해 pop을 적용했을 때의 에러를 방지
    if (this.idx === 0) {
      return;
    }

    const result = this.arr[this.idx - 1];
    delete this.arr[this.idx - 1];
    this.idx--;

    return result;
  }

  // 꼭대기에 있는 원소 반환 (마지막에 추가된 원소 반환)
  peek() {
    return this.arr[this.arr.length - 1];
  }

  // 스택이 비어있는지 아닌지를 판단
  isEmpty() {
    return this.arr.length === 0;
  }

  // 스택의 길이를 반환
  size() {
    return this.arr.length;
  }

  // 스택내의 모든 원소를 제거
  clear() {
    this.arr = [];
  }

  // 스택의 내용물들을 출력
  print() {
    console.log(this.items.toString());
  }
}
```

### 장점/단점

- 장점

  - 단순한 구조로 구현이 쉬움
  - 데이터 저장/읽기 속도가 빠름

- 단점
  - 데이터 최대 개수를 정해야함 (가변형 배열로 스택을 구현하는게 아닐 경우)
    - 재귀함수에 많이 쓰이는데, 재귀 함수의 호출 가능 횟수가 언어마다 다르기 때문
  - 저장 공간 낭비가 발생할 수 있음
    - 데이터 최대 개수만큼 저장 공간을 확보해야하기 때문

### 사용 예시

- 깊이 우선 탐색(DFS)

  - 정점을 스택에 저장하고, 경로를 따라 정점을 찾아가면서 인접 정점이 있으면 방문하는 탐색 방식

- 재귀 알고리즘

  - 재귀적으로 함수 호출할 때 임시 데이터를 Stack에 쌓아둔다.
  - 재귀함수를 빠져나와 이어서 검색을 할 때는 Stack에 넣은 임시 데이터를 빼줘야함.

- 브라우저의 뒤로가기 & 앞으로가기 기능
  - 새 페이지로 접속 할 때 현재 페이지를 Prev Stack에 보관
  - 뒤로가기 버튼으로 이전 페이지로 돌아갈 때는, 현재 페이지를 Next Stack에 보관한 후, Prev Stack에서 가장 마지막으로 보관된 페이지를 현재 페이지로 가져옴
  - 앞으로가기 버튼으로 앞서 방문한 페이지로 돌아갈 때는, 현재 페이지를 Prev Stack에 보관한 후, Next Stack에서 가장 마지막으로 보관된 페이지를 현재 페이지로 가져옴
