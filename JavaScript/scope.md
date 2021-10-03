## Scope

코드에서 어떠한 변수(식별자)가 실제로 가리키는 값을 결정하는 것을 **binding**이라고 함

JavaScript에서의 binding은 **lexical scope**를 통해 이루어짐

- lexical scope : inner scope에서 outer scope의 변수(식별자)에 접근할 수 있다는 의미

```js
function a() {
  let x = 1;
  function b() {
    const y = 2;
    console.log(x); // 1
    // 여기서 x는 세 줄 위의 x의 값을 가리킴
    console.log(y); // 2
  } // inner scope
  console.log(x); // 1
  console.log(y); // ReferenceError
} // outer scope
```

let, const는 block scoping이 되지만, var는 되지 않음

```js
var a = 1;
if (true) {
  var x = 2;
}
console.log(x); // 2

// var는 block scoping을 하지 않음
```
