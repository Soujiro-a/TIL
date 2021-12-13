## Dynamic Programming

**주어진 문제를 여러 개의 하위 문제로 나누어 푼 뒤, 하위 문제들의 해결 방법을 결합하여 주어진 문제를 해결하는 방식**

### 사용조건

1. 주어진 문제에서 작은 문제로 나눌 수 있고, 작은 문제가 중복해서 발견됨.
   - 작은 문제는 주어진 문제를 해결할 때 여러 번 반복 사용될 수 있어야함.
2. 작은 문제에서 구한 답이 해당 작은 문제를 포함하는 주어진 문제에서도 같다.
   - 작은 문제들의 최적의 해법을 찾아서 결합하면 주어진 문제에 대한 최적의 해법.

### 주로 사용하는 방법

#### Memorization

**하위 문제의 해결책을 저장한 뒤, 동일한 하위 문제가 나왔을 경우 저장해놓은 해결하는 사용하는 방법**

_동일한 계산을 반복할 때, 이전에 계산한 값을 메모리에 저장해놓음으로서 반복수행을 줄여 실행속도를 빠르게 하는 방법_

큰 문제를 해결하기위해 작은 문제를 호출한다고 하여 **Top-down방식**이라고 부르기도 함.
예시(피보나치 수열)

```js
function fib(n, memo = []) {
  // 이미 해결한 하위 문제라면 해당하는 값을 반환
  if (memo[n] !== undefined) {
    return memo[n];
  }
  // 피보나치 수열은 2번째까지는 값이 1로 정해져있다.
  if (n <= 2) {
    return 1;
  }
  // 처음 계산하는 수라면 n-1번쨰와 n-2번째를 이용하여 값을 계산함.
  const result = fib(n - 1, memo) + fib(n - 2, memo);
  memo[n] = result; // 동일한 문제를 만났을 때 사용하기 위해 값을 반환하기 전에 memo에 저장

  return result;
}
```

#### Iteration + Tabulation

**하위 문제에서 시작해서 주어진 문제를 해결해 나가는 방법**

하위 문제의 값을 배열에 저장하고, 필요할 때 조회하여 사용하는 건 Memorization을 이용한 방법도 동일하지만, 큰 문제로부터 작은 문제로가는 방법과 정반대임.
따라서 이 방식을 **Bottom-up방식**이라고 부르기도 함.

예시

```js
function fib(n) {
  if (n <= 2) {
    return 1;
  }
  // n이 1&2일 때의 값을 미리 배열에 저장
  const fibNum = [0, 1, 1];

  // n>=3 부터는 위 배열에서 저장해놓은 값들을 이용하여

  for (let i = 3; i <= n; i++) {
    fibNum[i] = fibNum[i - 1] + fibNum[i - 2];
  }
  // n번째 피보나치 수를 구한 뒤 배열에 저장한 후 값을 반환함
  return fibNum[n];
}
```

### 그 외의 예시

- 최소 동전 교환 문제
  - 주어진 금액을 특정 금액의 동전(10, 50, 100, 500 등)으로 바꿔줄 때, 필요한 동전의 최소 개수를 찾는 문제
    ex) 780원을 동전으로 바꿀 경우
    - 10원 : 3개
    - 50원 : 1개
    - 100원 : 2개
    - 500원 : 1개
  - 단, 동전 종류가 오름차순 정렬을 해줘야 계산하기 수월함

```js
function minCoinChange(coins) {
  let coins = coins; // 동전 종류들
  let cache = {}; // 중복 계산을 최대한 피하기위한 객체

  this.makeChange = function (amount) {
    const me = this;

    if (!amount) {
      // 금액이 음수라면 빈 배열 반환
      return [];
    }

    // 해당 금액에 대해 이미 캐싱이 되어있는 상태라면 캐싱되어있는 값을 반환
    if (cache[amount]) {
      return cache[amount];
    }

    //
    let min = [];

    // newMin : 동전의 최소 개수
    // newAmount : 유효한 최소 금액
    let newMin, newAmount;

    for (let i = 0; i < coins.length; i++) {
      const coin = coins[i];
      newAmount = amount - coin; // 각 동전에 대한 newAmount를 계산

      //  유효한 금액에 대해 다시 재귀호출을 통하여 결과를 담음
      if (newAmount >= 0) {
        newMin = me.makeChange(newAmount);
      }

      if (
        newAmount >= 0 && // newAmount가 유효한 값인가
        // newMin이 최적값으로 도출 됐는지
        (newMin.length < min.length - 1 || !min.length) &&
        // newMin, newAmount 모두 유효 값인지
        (newMin.length || !newAmount)
      ) {
        // 위 조건들을 모두 충족한다면, 이전보다 더 나은 결과를 얻었다는 반증
        min = [coin].concat(newMin);
      }
    }
    return (cache[amount] = min); // 최종 결과를 반환
  };
}
```
