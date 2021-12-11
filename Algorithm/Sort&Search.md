## Sort

### 종류

- 버블 정렬 : 인접한 두 원소를 모두 다 비교하고, 그 결괴에 따라 두 원소의 위치를 서로 바꿈
- 선택 정렬 : 최소값을 찾아 가장 앞으로 보내고, 그 다음으로 작은 값을 찾아 다음 위치로 보내는 방식으로 정렬함
- 삽입 정렬 : 한 번에 한 원소씩 정렬된 배열을 만드는 방식으로 정렬함
  - 크기가 작은 배열이라면 버블, 선택 정렬에 비해 성능이 우수함
- 병합 정렬 : 정렬할 배열을 원소가 하나뿐인 배열 단위로 나뉠 때까지 분할하고, 분할된 배열을 점점 더 큰 배열로 병합하는 방식으로 정렬함
- 퀵 정렬 : 병합 행렬처럼 분할/병합 방식으로 접근하지만, 원소를 하나 가진 배열이 될때까지 잘게 쪼개진 않음

## Search

### 종류

- 순차 검색 : 원하는 원소를 찾을 때까지 자료 구조 전체를 뒤져보는 알고리즘
- 이진 검색 : 특정 숫자보다 큰지 작은지를 파악하며 범위를 좁혀가며 숫자를 맞추는 알고리즘
  - 해당 자료구조의 정렬을 먼저 끝내놓을 필요가 있다

### 구현

```js
function ArrayList() {
  let array = [];

  // 원소 삽입
  this.insert = function (item) {
    array.push(item);
  };

  // 전체 원소를 문자열 하나로 합쳐 출력
  this.toString = function () {
    return array.join();
  };

  // 두 원소의 위치 변경
  const swap = function (index1, index2) {
    const aux = array[index1];
    array[index1] = array[index2];
    array[index2] = aux;
  };

  // 버블 정렬
  this.bubbleSort = function () {
    const length = array.length;
    for (let i = 0; i < length; i++) {
      //바깥쪽 루프의 반복 횟수를 차감해줌으로서 불필요한 비교작업이 줄어듬
      for (let j = 0; j < length - 1 - i; j++) {
        if (array[j] > array[j + 1]) {
          swap(j, j + 1);
        }
      }
    }
  };

  // 선택 정렬
  this.selectionSort = function () {
    const length = array.length;
    let indexMin; // 최소값을 가진 원소의 인덱스를 담을 변수
    for (let i = 0; i < length - 1; i++) {
      indexMin = i;
      for (let j = i; j < length; j++) {
        if (array[indexMin] > array[j]) {
          indexMin = j;
        }
      }
      if (i !== indexMin) {
        swap(i, indexMin);
      }
    }
  };

  // 삽입 정렬
  this.insertionSort = function () {
    const length = array.length;
    let j, temp;

    // 첫번째 원소는 정렬이 되어있다고 가정하기 때문에 1번째 원소부터 반복
    for (let i = 1; i < length; i++) {
      j = i;
      temp = array[i];
      // 직전 인덱스의 원소가 인덱스i의 원소보다 크다면
      while (j > 0 && array[j - 1] > temp) {
        // 직전 인덱스 원소를 한칸 앞으로 옮김
        array[j] = array[j - 1];
        j--;
      }
      array[j] = temp; // 위 while문을 통해 확정된 자리에 원소를 삽입
    }
  };

  // 병합 정렬
  this.mergeSort = function() {
      array = mergeSortRec(array);
  }

    // 배열을 분할 후 병합하는 함수를 호출하는 함수
  const mergeSortRec = function(array) {
      // ArrayList 내부의 array의 길이가 아닌, 매개변수 array의 길이
      const length = array.length;

        // 원소가 하나일때만 해당 배열을 반환
      if(length === 1){
          return array;
      }

      const mid = Math.floor(length / 2); // 배열의 중간지점을 찾는다
      const left = array.slice(0, mid); // 0 ~ mid-1
      const right = array.slice(mid,length); // mid ~ length-1(마지막)

      return merge(mergeSortRec(left), mergeSortRec(right));
  }

    // 두 배열을 병합하는 함수
  const merge = function(left ,right) {
      const result = [];
      let il = 0;
      let ir = 0;

      while(il < left.length && ir<right.length) { // 배열을 순회
      // 왼쪽과 오른쪽의 각 원소들 크기를 비교하며 결과 배열에 집어 넣는다
          if(left[il] < right[ir]){
              result.push(left[il++]);
          } else {
              result.push(right[ir++]);
          }
      }

      // left에 남은 원소들을 모두 결과 배열에 집어 넣는다
      while(il < left.length) {
          result.push(left[il++])'
      }

      // right에 남은 원소들을 모두 결과 배열에 집어 넣는다
      while(ir < right.length) {
          result.push(right[ir++])'
      }

      return result;
  }

  // 퀵 정렬
  this.quickSort = function() {
      quick(array, 0, array.length-1);
  }

  const quick = function(array, left, right) {
      // 서브 배열로 나누어 재귀호출 하기 위한 변수
      let index;

      // 배열 크기가 2 이상 일 때만(원소가 하나면 이미 정렬된 것이므로)
      if(array.length > 1) {
          // 파티션 작업을 통해 index값을 얻음
          index = partition(array, left, right);

          // 더 작은 원소들을 가진 서브배열이 존재할 경우 재귀
          if(left < index-1){
              quick(array, left, index-1);
          }

          // 더 큰 원소들을 가진 서브배열이 존재할 경우 재귀
          if(index<right) {
              quick(array, index, right);
          }
      }
  }

  const partition = function(array, left, right) {
      // 가운데 원소를 pivot으로 둠
      const pivot = array[Math.floor((left+right)/2)];
      let l = left; // 좌측 포인터
      let r = right; // 우측 포인터

      while(l<=r){ // 좌, 우 위치가 역전될 때 까지 반복
          // pivot 보다 같거나 큰 원소를 발견할 때까지 좌측 포인터를 우측으로 이동
          while(array[l] < pivot){
              l++;
          }
          // pivot 보다 같거나 작은 원소를 발견할 때까지 우측 포인터를 좌측으로 이동
          while(array[r] > pivot){
              r++;
          }
          // 두 포인터가 역전되지 않았다면
          if(l<=r){
              swapQuickSort(array, l, r); // 두 포인터가 기리키는 원소 둘을 서로 교환
              l++;
              r--;
          }
      }
      return l; // 좌측 포인터 변수를 반환하여 위의 quick 함수에서 활용
  }

  const swapQuickSort = function(array, index1, index2) {
    const aux = array[index1];
    array[index1] = array[index2];
    array[index2] = aux;
  }

  // 순차 검색
  this.sequentialSearch = function(item) {
    for(let i = 0; i<array.length; i++){
      if(item === array[i]) {
        return i;
      }
    }
    return -1;  // 찾고자 하는 원소가 존재하지 않을 경우 -1 반환
  }

  // 이진 검색
  this.binarySearch = function(item) {
    this.quickSort(); // 정렬 방식 아무거나 정렬만 잘되거나, 되어있다면 상관없음

    let low = 0;
    let high = array.length - 1;
    let mid, element;

    while(low <= high) {
      // 가운데 인덱스를 찾고, 해당 인덱스의 원소값도 담아둔다
      mid = Math.floor((low+high)/2);
      element = array[mid];
      if(element < item){ // 가운데 원소가 찾는 원소보다 작다면
        low = mid + 1; // 가운데보다 더 큰 값을 대상으로 다시 반복
      } else if(element > item){ // 가운데 원소가 찾는 원소보다 크다면
        high = mid - 1; // 가운데보다 더 작은 값을 대상으로 다시 반복
      } else { // 찾은 경우에는 해당 인덱스를 반환
        return mid;
      }
    }

    return -1;
  }
}
```
