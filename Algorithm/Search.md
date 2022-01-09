## Search

### 종류

- 순차 검색 : 원하는 원소를 찾을 때까지 자료 구조 전체를 뒤져보는 알고리즘
- 이진 검색 : 특정 숫자보다 큰지 작은지를 파악하며 범위를 좁혀가며 숫자를 맞추는 알고리즘
  - 해당 자료구조의 정렬을 먼저 끝내놓을 필요가 있다

### 구현

```js
let array = [1, 2, 3, 4, 5, 6]; // 이 배열을 검색하는 로직을 아래에 구현 예정

// 순차 검색
sequentialSearch = function (item) {
  for (let i = 0; i < array.length; i++) {
    if (item === array[i]) {
      return i;
    }
  }
  return -1; // 찾고자 하는 원소가 존재하지 않을 경우 -1 반환
};

// 이진 검색
binarySearch = function (item) {
  // 혹시나 검색할 배열이 안되어있을 경우, 정렬을 먼저 해줘야 함

  let low = 0;
  let high = array.length - 1;
  let mid, element;

  while (low <= high) {
    // 가운데 인덱스를 찾고, 해당 인덱스의 원소값도 담아둔다
    mid = Math.floor((low + high) / 2);
    element = array[mid];
    if (element < item) {
      // 가운데 원소가 찾는 원소보다 작다면
      low = mid + 1; // 가운데보다 더 큰 값을 대상으로 다시 반복
    } else if (element > item) {
      // 가운데 원소가 찾는 원소보다 크다면
      high = mid - 1; // 가운데보다 더 작은 값을 대상으로 다시 반복
    } else {
      // 찾은 경우에는 해당 인덱스를 반환
      return mid;
    }
  }

  return -1;
};
```
