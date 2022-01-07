## Space Complexity(공간 복잡도)

- 프로그램을 실행 및 완료하는데 필요한 저장공간의 양
- 총 필요 저장 공간 : 고정 공간 + 가변 공간
  - 고정 공간 : 코드 저장 공간, 단순 변수 및 상수
    - 알고리즘과 무관한 공간
  - 가변 공간 : 실행 중 동적으로 필요한 공간
- [빅 오 표기법](https://github.com/Soujiro-a/TIL/blob/main/Algorithm/Time%20Complexity.md#big-o-%ED%91%9C%EA%B8%B0%EB%B2%95)을 토대로 생각해보면, 공간 복잡도는 가변 공간에 의해 좌우됨
  - 고정 공간은 입력(매개변수)과 상관이 없는 상수로서 생각하기 때문
- 그러나 최근엔 대용량 시스템이 보편화 되면서, 공간 복잡도보다는 시간 복잡도가 우선시 됨
  - 그래서 알고리즘은 [시간 복잡도](https://github.com/Soujiro-a/TIL/blob/main/Algorithm/Time%20Complexity.md)를 중심으로 생각함

### 공간 복잡도 계산

- 실제 사용되는 저장 공간을 계산함
  - [빅 오 표기법](https://github.com/Soujiro-a/TIL/blob/main/Algorithm/Time%20Complexity.md#big-o-%ED%91%9C%EA%B8%B0%EB%B2%95)으로 표현

#### 예제

팩토리얼(n!)을 구하는 방법

```js
function factorial(n) {
  if (n <= 1) {
    return 1;
  }
  result = 1;
  for (let i = 2; i <= n; i++) {
    result *= i;
  }

  return result;
}

// 매개변수 n의 값과 상관없이, 변수 n, result, i 만 필요하기 때문에 공간 복잡도는 O(1)

function recursionFac(n) {
  if (n > 1) {
    return n * recursionFac(n - 1);
  } else {
    return 1;
  }
}

// 재귀함수를 사용했기 때문에 매개변수 n에 따라 n부터 1까지 스택에 쌓여 변수 n이 n개 만들어짐
// => 공간 복잡도는 O(n)
```
