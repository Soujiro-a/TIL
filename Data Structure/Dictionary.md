## Dictionary

### 특징

- 데이터를 [키, 값] 쌍으로 담아두는 자료구조
- Map이라고도 불림

### 구현

```js
function Dictionary() {
  let elements = {};

  // 키에 해당하는 원소가 존재하면 true, 아니면 false를 반환
  this.has = function (key) {
    return key in elements;
  };

  // Dictionary에 원소를 추가
  this.set = function (key, value) {
    elements[key] = value;
  };

  // 키에 해당하는 원소를 삭제
  this.remove = function (key) {
    if (this.has(key)) {
      delete elements[key];
      return true;
    }
    return false;
  };

  // 키에 해당하는 원소의 값을 반환
  this.get = function (key) {
    return this.has(key) ? elements[key] : undefined;
  };

  // Dictionary의 모든 값을 배열로 반환
  this.values = function () {
    const values = [];
    for (let k in elements) {
      if (this.has(k)) {
        values.push(elements[k]);
      }
    }
    return values;
  };

  // 모든 원소를 삭제
  this.clear = function () {
    elements = {};
  };

  // 원소의 갯수를 반환
  this.size = function () {
    // 집합의 모든 프로퍼티를 배열로 변환한 후에 해당 배열의 길이를 반환
    return Object.keys(elements).length;
  };

  // Dictionary의 모든 키를 배열로 반환
  this.keys = function () {
    // 집합의 모든 프로퍼티를 배열로 변환한 후에 해당 배열의 길이를 반환
    return Object.keys(elements);
  };

  // elements를 가져오는 메소드
  this.getElements = function () {
    return elements;
  };
}
```
