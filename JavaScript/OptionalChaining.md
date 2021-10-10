## Optional Chaining (?. 연산자)

- chaining : `. 연산자`를 일컬음

```js
const user = { name: { first: "K", last: "KY" }, age: "28" };
console.log(user.name.last); // KY

// user.name에서 . 연산자 부분을 chaining이라고 일컬음
```

그러나, 객체를 탐색할 때는 항상 TypeError가 발생할 수도 있음
=> 찾고자하는 프로퍼티가 undefined일 경우

```js
const userLastName = user.birth && user.birth.month;
console.log(userLastName); // undefined
```

&&연산자나 || 연산자를 써서 TypeError를 피하는 것도 방법이기는 하나, **Optional Chaining을 통해 해당 객체가 nullish\*인 경우에는 TypeError 대신 undefined 값을 얻을 수 있게 됨**
\*nullish : undefined or null 인 경우

```js
console.log(user?.name?.first); // K
console.log(user?.birth?.month); // undefined
```

객체 뿐만 아니라, 배열이나 함수에서도 사용할 수 있음

```js
const arr = null;
console.log(arr?.[0]); // undefined

const func = undefined;
console.log(func?.()); // undefined
```
