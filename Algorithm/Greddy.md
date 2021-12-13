## Greddy Algorithm

**당장 눈앞에 보이는 최적의 상황만을 쫓아 최종 해답에 도달하는 방법**

해당 알고리즘을 사용하는 문제는 대부분 탐욕 선택 조건, 최적 부분구조 조건 두가지를 만족함.

탐욕 선택 조건 : 앞의 선택이 이후의 선택에 영향을 주지 않음
최적 부분구조 조건 : 문제에 대한 최적화된 답은, 부분 문제에 대해서도 최적화된 답을 제공함.

### 단계 구분

1. 선택 절차 : 현재 상태에서의 최적의 답을 선택
2. 적절성 검사 : 선택된 해가 문제의 조건을 만족하는지 검사
3. 해답 검사 : 처음 받은 문제가 해결됐는지를 검사하고, 해결되지 않았다면 선택 절차부터 다시 반복.

### 예시

- 최소 동전 교환 문제
  - [동적 프로그래밍](https://github.com/Soujiro-a/TIL/blob/main/Algorithm/Dynamic%20Programming.md) 방식보다 단순하게 구현할 수 있음

```js
function MinCoinChange(coins) {
  let coins = coins;

  this.makeChange = function (amount) {
    const change = [];
    let total = 0;

    for (let i = coins.length; i >= 0; i--) {
      let coin = coins[i];
      // 각 동전에 대해 금액이 큰것부터 작은 것 순으로 total에 더해감
      // 현재 동전 금액으로 더 이상 추가할 수 없다면 그 다음으로 큰 금액의 동전을 찾아가는 방식
      while (total + coin <= amount) {
        change.push(coin);
        total += coin;
      }
    }
    return change;
  };
}
```
