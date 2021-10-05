## Spread Syntax (...)

- 객체의 Key-Value 병합

```js
const personalData = {
  name: "KKY",
  email: "test@github.com",
};

const publicData = {
  age: 28,
};

const user = {
  ...personalData,
  ...publicData,
};

/*
 user = {
    name: 'KKY',
    email: 'test@github.com',
    age: 28
}
*/
```

- 같은 Key인 경우에는 덮어쓰기 가능

```js
const overrides = {
  DB_HOST: "hello",
  DB_PASSWORD: "password",
};

const dbConfig = {
  DB_HOST: "host",
  DB_PASSWORD: "********",
  DB_USERNAME: "KKY",
  ...overrides, // 덮어 씌우고 싶은 Value가 속해있는 객체를 뒤에 써줘야함
};

/*
dbConfig = {
  DB_HOST: "hello",
  DB_PASSWORD: "password",
  DB_USERNAME: "KKY",
};
*/
```

- 객체 구조 분배 할당에 사용할 수 있음

```js
const user = {
  name: "KKY",
  age: 28,
  email: "test@github.com",
};

const { name, ...userData } = user;
console.log(userData); // { age: 28, email: "test@github.com" }
```

- 배열을 합치는데도 사용할 수 있음

```js
const low = ["a", "b", "c"];
const up = ["A", "B", "C"];
const alphabets = [...low, ...up];
console.log(alphabets); // ["a", "b", "c", "A", "B", "C"]
```

- 배열의 구조 분배 할당에 쓰일 수 있음

```js
const [head, ...tail] = [1, 2, 3];
console.log(head); // 1
console.log(tail); // [2, 3]
```

- 객체의 데이터 조건부 덮어쓰기

```js
const isOverride = true;

const user = {
  ...{
    name: "KKY",
    email: "test@github.com",
  },
  ...{
    password: "password",
  },
  ...(isOverride
    ? {
        email: "test@naver.com",
      }
    : null),
};

// isOverride = true
// => {name: "KKY", email: "test@naver.com", password: "password" }
// isOverride = false
// => {name: "KKY", email: "test@github.com", password: "password" }
```

- 함수의 매개변수로 활용하기

```js
function a(head, ...tail) {
  console.log(head);
  console.log(tail);
}

a(1, 2, 3, 4);

// 출력 결과
// 1
// [2, 3, 4]
```
