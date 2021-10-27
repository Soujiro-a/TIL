## Object-Oriented Programming - 객체 지향 프로그래밍

객체(Object)의 핵심적인 개념 또는 기능만을 추출하는 추상화를 통해 모델링하려는 프로그래밍 패러다임
=> 주변에서 사물을 인지하는 방식을 프로그래밍에 접목하려는 것

JavaScript에서의 OOP는 모든 것이 다 객체(Object)로 되어있고, 객체로 설명이 가능하다

### Class & Prototype

객체 지향 프로그래밍을 지원하는 언어는 **클래스 기반**과 **프로토타입 기반**으로 나누어져있다.

- 클래스 기반 : C++, Java 등
- 프로토타입 기반 : JavaScript 등

나는 현재 JavaScript를 공부하고 있기때문에, JavaScript 중심으로 작성할 예정

### 객체 생성 방법

1. 리터럴
   - 간단하게 변수에 직접 객체를 작성해 넣는 방법

```js
const a = {
  b: 0,
  c: function () {
    this.b++;
  },
  d: function () {
    this.b--;
  },
};

// 장점 : 간단하게 작성할 수 있음
// 단점 : 외부에서 내부 속성에 접근이 가능하기 때문에 객체의 기능을 임의로 조작할 수 있음

// 단점을 보완하기 위한 방법으로는 즉시 실행 함수를 통한 캡슐화가 있다.

const a = (function () {
  let b = 0;

  return {
    c: function () {
      this.b++;
    },
    d: function () {
      this.b--;
    },
  };
})();

// 단, 이렇게 캡슐화된 a를 대량으로 사용하기엔 적절한 방법이 아님
```

2. new 생성자 함수
   - new 연산자는 사용자 정의 객체 타입 또는 내장 객체 타입의 인스턴스*를 생성함
     *인스턴스 : new 연산자와 함께 생성자 함수를 호출해서 생성한 객체

```js
function a() {
  this.b = 0;

  a.prototype.c = function () {
    this.b++;
  };

  a.prototype.d = function () {
    this.b--;
  };
}

const e = new a();
const f = new a();

// 장점 : 대량 생산에 용이함
// 단점 : 외부에서 내부 속성에 접근이 가능하기 때문에 객체의 기능을 임의로 조작할 수 있음

// Factory Function*를 통하여 캡슐화 + 대량 생상이 가능하게 할 수 있다.
// *Factory Function : 객체(Object)를 반환하는 함수(Function)

function aFactory() {
  let b = 0;

  return {
    c: function () {
      b++;
    },
    d: function () {
      b--;
    },
  };
}

const e = new aFactory();
const f = new aFactory();
```

3. Object.create();
   - 매개변수 속 객체를 prototype으로 하는 객체를 생성
   - 주의할 점은 : constructor를 재연결해주어야 상위 메소드와 본인이 가지고 있는 메소드 모두 사용할 수 있음

```js
function a() {
  this.b = 0;
}

a.prototype.c = function () {
  this.b++;
};

a.prototype.d = function () {
  this.b--;
};

// 위와 같은 a 생성자 함수가 있다고하자.

function e() {
  a.call(this);

  this.f = false;
}

e.prototype = Object.create(a.prototype); // prototype 연결
e.prototype.constructor = e; // constructor 재연결

e.prototype.g = function () {
  this.f = !this.f;
};

const h = new e();
const i = new e();

// 장점 : 중복 코드를 줄이고, 프로토타입 체인으로 메소드를 상속할 수 있다.
// 단점 : 코드가 길어지고, 코드의 위치에 따라 결과가 크게 달라지기 때문에 주의가 필요함
// => 하위 생성자에서 메소드 정의 후 상위 생성자와 연결하면, 하위 생성자에서 정의한 메소드들을 쓸 수 없게 됨.
```

### Class

JavaScript에서는 ES6부터 사용가능하게 된 개념으로, 기존 프로토타입 방법과 비교해, 작성법만 제외하면 크게 다르지 않다.

```js
class a {
    constructor() {
        this.b = 0;
    }

    c = function() {
        this.b++;
    }

    d = function() {
        this.b--;
    }
}

// 앞선 프로토타입으로 객체를 생성할 때와는 다르게, 프로토타입 연결을 따로 해주는 게 아니라 상속을 통해 상위 생성자와 연결할 수 있다.

class e extends a {
  constructor(props) {
      super(props);
  }

  this.f = false;

  g = function() {
    this.f = !this.f;
  }
}
```
