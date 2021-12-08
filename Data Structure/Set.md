## Set (집합)

### 특징

- 정렬되지 않음
- 중복 원소가 없음

### 구현

```js
function Set() {
  let elements = {};

  // 매개변수로 받은 값이 집합에 포함되어있는지 여부를 true/false로 판단
  this.has = function (value) {
    // 매개변수로 받은 값이 집합(elements)의 프로퍼티중 하나인지 확인
    return value in elements;
    // return elements.hasOwnProperty(value); => 이렇게 작성해도 됨
  };

  // 원소 추가
  this.add = function (value) {
    // 매개변수로 받은 value가 아직 포함되어있지 않은지 판단
    if (!this.has(value)) {
      elements[value] = value;
      return true;
    }
    return false;
  };

  // 원소 제거
  this.remove = function (value) {
    // 매개변수로 받은 value가 이미 포함되어있는지 판단
    if (this.has(value)) {
      delete elements[value];
      return true;
    }
    return false;
  };

  // 집합 초기화
  this.clear = function () {
    elements = {};
  };

  //집합의 원소 갯수 반환
  this.size = function () {
    // 집합의 모든 프로퍼티를 배열로 변환한 후에 해당 배열의 길이를 반환
    return Object.keys(elements).length;
  };

  //집합의 모든 원소를 배열 형태로 반환
  this.values = function () {
    return Object.keys(elements);
  };

  // 합집합
  this.union = function (otherSet) {
    let unionSet = new Set();

    let values = this.values();
    for (let i = 0; i < values.length; i++) {
      unionSet.add(values[i]);
    }
    values = otherSet.values();
    for (let i = 0; i < values.length; i++) {
      unionSet.add(values[i]);
    }
    return unionSet;
  };

  // 교집합
  this.intersection = function (otherSet) {
    let intersectionSet = new Set();

    let values = this.values();
    for (let i = 0; i < values.length; i++) {
      if (otherSet.has(values[i])) {
        intersectionSet.add(values[i]);
      }
    }

    return intersectionSet;
  };

  // 차집합
  this.difference = function (otherSet) {
    let differenceSet = new Set();

    let values = this.values();
    for (let i = 0; i < values.length; i++) {
      if (!otherSet.has(values[i])) {
        differenceSet.add(values[i]);
      }
    }

    return differenceSet;
  };

  // 현재 인스턴스의 집합이 매개변수로 받은 집합의 부분집합인지를 판단
  this.subset = function (otherSet) {
    if (this.size() > otherSet.size()) {
      return false;
    } else {
      let values = this.values();
      for (let i = 0; i < values.length; i++) {
        if (!otherSet.has(values[i])) {
          return false;
        }
      }
      return true;
    }
  };
}
```
