## let & const

- ES2015(ES6)에 추가된 변수 선언 키워드
- hoisting 규칙이 없음
- block scoping을 지원
  - var보다 예측 가능한 코드를 짤 수 있게 해줌

### let vs const

- let : 변수의 값이 **바뀔 수 있음**
- const : 처음 선언한 변수의 값을 **변경할 수 없음**

```js
let x = 1;
x = 2;

const y = 1;
y = 2; // Uncaught TypeError : Assignment to constant variable
```

### var vs let & const

- var : 특정 scope 내에서 **동일이름의 변수를 여러 번 정의할 수 있음**
- let & const : 특정 scope 내에서 **동일이름의 변수를 두 번 이상 정의할 수 없음**

```js
var x = 1;
var x = 2;

let y = 1;
let y = 2; // Uncatght SyntaxError : Identifier 'y' has already been declared
```

- var : 변수를 정의하기전이라도 해당 이름의 변수를 사용가능([Hoisting](https://github.com/Soujiro-a/TIL/blob/main/JavaScript/Hoisting.md))
- let & const : 변수를 정의하기전에는 해당 변수를 사용할 수 없음

```js
console.log(x); // undefined
var x = 1;

console.log(y); // ReferenceError : Cannot access 'y' before initialization
const y = 1;
```

- var : block scoping 미지원
- let & const : block scoping 지원

```js
var x = 1;
{
    var x = ;
    console.log(x); // 2
}
console.log(x) // 2

const y = 1;
{
    const y = 2;
    console.log(y); // 2
}
console.log(y); // 1
```

### 정리

- 예측 가능성, 유지보수성인 측면에서 let & const > var
- 가능하다면 const, 필요에 따라 let을 쓰고, **var는 사용하지 말기!**
