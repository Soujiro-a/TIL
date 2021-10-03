## Hoisting

### 변수

변수의 선언만을 해당하는 스코프 내의 가장 위로 끌어올림

```js
console.log(x); // undefined,
var x = 1;
// Hoising을 통해, 아랫줄에 var타입의 x의 선언 부분만 해당 코드보다 위로 올라가게 됨
```

```js
// 위의 예시와 동일함
var x;
console.log(x);
x = 1;
```

```js
console.log(x);
x = 1;
// 이 경우는 변수의 선언 자체가 이루어지지 않았으므로 ReferenceError가 발생함
```

### 함수

아래의 두 예시의 실행 결과는 동일함

```js
function a() {
  return "a";
}
console.log(a());
```

```js
console.log(a());
function a() {
  return "a";
}
```

함수의 선언과 값의 초기화는 서로 다르기 떄문에, Hoisting도 다르게 이루어짐
