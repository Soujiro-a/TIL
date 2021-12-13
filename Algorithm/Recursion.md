## Recursion (재귀)

- 어떤 문제를 작은 단위의 동일한 문제들로 나누어 해결하는 방법
- 자기 자신을 다시 호출
- 별 다른 조건 없이 실행하면 끝없이 자기 자신을 호출하는 무한루프에 빠짐
  - 멈추는 조건(base case)이 반드시 필요함

### 사용 예시

- 피보나치 수열
  - 1항, 2항의 값은 1이다
  - n>2인 경우, n항은 (n-1)+(n-2)항의 합이다.

```js
// 재귀를 사용하지 않는 경우의 피보나치 수열 코드
function fib(num) {
  let n1 = 1;
  let n2 = 1;
  n = 1;
  for (let i = 3; i <= num; i++) {
    n = n1 + n2;
    n1 = n2;
    n2 = n;
  }
  return n;
}
// 재귀를 사용하는 경우의 피보나치 수열 코드
function fibonacci(num) {
  if (num === 1 || num === 2) {
    return 1;
  }

  return fibonacci(num - 1) + fibonacci(num - 2);
}
```
