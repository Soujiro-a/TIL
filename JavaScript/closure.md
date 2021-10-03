## Closure

function(함수)가 하나 선언될 때 마다 하나씩 생김

function + environment

- environment : 함수 자신을 둘러 싸고 있는 접근할 수 있는 모든 Scope를 뜻함

```js
function a(x) {
  return function b(y) {
    return x + y;
  };
}

const hello = a("hello");
console.log(hello("world")); // helloworld

/*
hello의 closure
  - 함수 : b
  - 환경 : x -> "hello"
*/

const java = a('java');
console.log(java('script)) // javascript

/*
java의 closure
  - 함수 : b
  - 환경 : x -> "java"
*/

// hellwo, code 모두 함수는 같은 b지만, 각각 주어진 변수가 다름
// x에 binding되어있는 값이 다르므로, 다른 closure를 형성하고 있다고 볼 수 있음
```

위 예시와 같이 **closure는 higher-order function을 만드는데 유용함**

- higher-order function : 다른 함수를 반환하는 고차 함수
