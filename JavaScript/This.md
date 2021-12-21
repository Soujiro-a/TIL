## This

- JavaScript에서 각 함수는 내부에 `this`라는 객체가 추가됨
- 유사 배열 객체인 arguments와 함께 함수 내부로 암묵적으로 전달됨
- 함수 호출 상황에 따라 `this`는 달라짐

```js
this.name = "Lee"; // 전역 객체에 name 키의 값을 할당
// 혹은 var로 선언해주어도 전역 객체에 담김(let, const는 안됨)
const myObj = {
  name: "Kim",
  getName1: function () {
    console.log(`getName1's name : ${this.name}`);

    const getName2 = function () {
      console.log(`getName2's name : ${this.name}`);
    };
    getName2();
  },
};

myObj.getName1();
// getName1's name : Kim
// getName2's name : Lee
```

### Binding

- 위에서 설명한 `this`를 상황에 맞는 객체로 바꾸는 것을 Binding이라 함
- 명시적으로 바꿔주는 함수는 아래 3가지가 있음
  - call
  - apply
  - bind

```js
function getInfo(age) {
  return `My name is ${this.name}. I'm ${age} years old.`;
}

const obj = { name: "Kim" };

getInfo(20); // My name is . I'm 20 years old.
getInfo.call(obj, 22); // My name is Kim. I'm 22 years old.
getInfo.apply(obj, [22]); // My name is Kim. I'm 22 years old.

const kimInfo = getInfo.bind(obj);
kimInfo(23); // My name is Kim. I'm 23 years old.
```
