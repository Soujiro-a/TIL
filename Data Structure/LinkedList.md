## Linked List

### 특징

- 원소를 배열처럼 차례대로 저장하지만, 메모리 상 연속적으로 위치하지는 않음
- 각 원소는 원소 자신과 다음 원소를 가리키는 참조 정보가 포함된 노드(Node)로 구성됨
  - Node : 데이터의 저장 단위가 (값, 포인터)로 구성됨
    - 포인터(Pointer) : 각 노드 안에서, 이전/다음 노드와의 연결 정보를 가지고 있는 공간
- 원소 추가/삭제 시 다른 원소들을 이동하지 않아도 됨
- 특정 원소에 바로 접근 할 수는 없다.
  - 특정 원소를 찾기 위해서는 처음(헤드 또는 루트)부터 루프를 통해 찾아야 함

### 구현

```js
function LinkedList() {
  const Node = function (element) {
    this.element = element;
    this.next = null;
  };

  let length = 0; // 연결 리스트내의 원소 갯수(리스트의 크기)
  let head = null; // 연결의 시작점 참조

  // 연결 리스트 끝에 원소를 추가
  this.append = function (element) {
    const node = new Node(element);
    let current;

    if (head === null) {
      // 리스트가 비어있을 때
      head = node;
    } else {
      current = head;

      while (current.next) {
        // 마지막 원소를 찾을 때 까지 순환
        current = current.next;
      }
      // 마지막 원소를 연결할 수 있게 다음 노드에 할당
      current.next = node;
    }
    // 리스트의 크기를 업데이트한다.
    length++;
  };

  // 리스트안에 임의의 위치에 원소 삽입
  this.insert = function (position, element) {
    // 위치값이 현재 리스트 안에 있는지 확인
    if (position > -1 && position < length) {
      const node = new Node(element);
      let current = head;
      let previous;
      let index = 0;

      // 첫번째에 추가
      if (position === 0) {
        node.next = current;
        head = node;
      } else {
        while (index < position) {
          previous = current;
          current = current.next;
        }

        // 위 루프를 벗어난 뒤에 previous와 current 사이에 새로 만든 node가 들어가기 때문에
        // 아래와 같이 연결 시켜준다.
        previous.next = node;
        node.next = current;
      }
      length++;

      return true;
    } else {
      return null;
    }
  };

  // 원소를 위치를 기준으로 삭제
  this.removeAt = function (position) {
    // 위치값이 현재 리스트 안에 있는지 확인
    if (position > -1 && position < length) {
      let current = head;
      let previous;
      let index = 0;

      // 첫번째 원소를 삭제할 경우
      if (position === 0) {
        head = current.next;
      } else {
        while (index < position) {
          previous = current;
          current = current.next;
          index++;
        }

        // 위 루프를 벗어난 뒤에는 current 변수가 삭제하려는 원소에 해당하기 때문에
        // previous.next를 current.next와 바로 연결시켜주면
        // current는 리스트에서 제외가 되므로 삭제가 된다고 볼 수 있다.
        previous.next = current.next;
      }

      // 리스트의 크기를 업데이트한다.
      length--;

      return current.element; //삭제된 요소를 반환
    } else {
      return null;
    }
  };

  //
  this.remove = function (element) {
    const index = this.indexOf(element);
    return this.removeAt(index);
  };

  // 매개변수로 받은 원소의 인덱스를 반환. 존재하지 않는다면 -1을 반환
  this.indexOf = function (element) {
    let current = head;
    let index = 0;

    while (current) {
      if (element === current.element) {
        return index;
      }
      index++;
      current = current.next;
    }
    return -1;
  };

  // 연결 리스트가 비어있는지 아닌지를 판단
  this.isEmpty = function () {
    return length === 0;
  };

  // 연결 리스트의 크기(길이)를 반환
  this.size = function () {
    return length;
  };

  // 연결 리스트를 문자열로 변환
  this.toString = function () {
    let current = head;
    let string = ""; // 결과를 담을 변수

    while (current) {
      string += current.element;
      current = current.next;
    }
    return string;
  };
}
```

## 장점/단점

- 장점
  - 데이터 공간을 미리 할당하지 않아도 됨
- 단점
  - 값 이외에 포인터도 같이 저장을 하기위한 데이터 공간이 필요해서 효율적이지 않음
  - 연결 정보를 찾는 시간이 필요하기 때문에, 접근 속도가 느림
  - 중간에 있는 노드를 삭제 할 경우, 해당 노드의 앞/뒤 연결을 재구성해야하는 추가 작업이 필요함
