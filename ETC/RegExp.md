## 정규표현식이란?

**문자열에서 특정한 문자를 찾아내는 도구**

## 정규표현식의 사용방식

- 리터럴 패턴

> 정규표현식 규칙을 /로 감싸 사용함.
> ex) let searchA = /A/;
> 'A를 찾을게!'라고 명령을 내리는 변수. 이 변수를 이용하여 A를 찾을 수 있다.

- 생성자 함수 호출 패턴

> RegExp 객체의 생성자 함수를 호출하여 사용함.
> ex) let searchA = new RegExp('A');
> new를 이용해서 정규표현식 객체를 생성함. 리터럴 패턴과 동일하게 이 변수를 이용하여 A를 찾을 수 있다.

## 정규표현식의 내장 메소드

### RegExp 객체의 메소드

- exec() : 원하는 정보를 뽑아내고자 할 때 사용

```js
let searchA = /A/;
searchA.exec("Abca"); // 검색하려는 대상을 exec 메소드의 첫번째 인자로 전달.

// 위 케이스에서는 'Abca'가 'A'를 포함하고 있는지를 확인함.
// 포함하고 있으면 ['A'], 포함하고있지 않으면 null을 반환함.
```

- test() : 찾고자하는 문자열이 대상안에 있는지 여부를 Boolean 타입으로 반환함.

```js
let searchB = /B/;
searchB.test("Banana"); // true

// 위 케이스에서는 'Banana'가 'B'를 포함하고 있는지를 확인하여, Boolean 타입으로 반환.
```

### String 객체의 메소드

- match() : RegExp 객체의 exec 메소드와 유사한 역할을 하는 메소드. 그러나 사용법이 조금 다르다.

```js
let searchC = /C/;
let str = "Code";
str.match(searchC); // ['C']

// 위 케이스에서는 str안에 searchC가 포함되어있는지를 확인함.
// 포함하고 있으면 ['C'], 포함하고있지 않으면 null을 반환함.
```

- replace() : 검색 후 해당하는 문자(열)를 바꾸는 작업을 함.

```js
let searchD = /D/;
let str = "Depth";
str.replace(searchD, "d"); // 'depth'

// 위 케이스에서는 str안에 searchD를 포함하고있는지를 확인함.
// 해당하는 문자(열)를 replace 메소드의 두번째 인자로 바꾼 결과를 반환함.
```

- split() : 매개변수를 구분자로 삼아, 문자열을 부분 문자열로 나눈 배열을 반환함.

```js
"010-1234-5678".split("-"); // ['010','1234','5678']
"123415671890".split("1"); // ['234','567','890']

// 매개변수와 일치하는 문자(열)는 결과에 포함되지 않음.
```

- search() : 정규표현식을 인자로 받아, 가장 처음 매칭되는 부분 문자열의 위치를 반환함.

```js
"HelloWorld".search(/o/); // 4
"HelloWorld".search(/O/); // -1
"HelloWorld".search(/World/); // 5

// 위 케이스들에서는 인자에 있는 정규표현식과 가장 처음 매칭되는 부분의 앞문자의 위치를 반환함.
// 대소문자를 구분하고, 일치하지 않으면 -1을 반환함.
```

## flag

추가적인 검색 옵션의 역할을 함. 순서에 구분이 없고, 각자 사용하거나 같이 사용하는 것 모두 가능함.

- i : 대소문자를 구분하지 않음.

```js
let searchDd = /D/i;
let searchD = /D/;
"depth".match(searchDd); // ['d'];
"depth".match(searchD); // null

// 대소문자를 구분하지 않고 해당하는 문자(열)를 찾아 반환함.
```

- g : 검색된 모든 결과를 반환함.

```js
let globalSearchA = /A/g;
let searchA = /A/;

"AbcaA".match(globalSearchA); //['A','A']
"AbcdA".match(searchA); //['A']

// g가 없을 경우에는 첫번째 검색 결과만 반환함.
```

- m : 여러 행을 검색함.

```js
let str = `
1 : Abcd
2 : ABcd
3 : ABCd
4 : ABCD
`;
str.match(/A/gm); //['A','A','A','A'] 4개의 행을 검색하여 모든 A를 반환함.
str.match(/A/m); //['A'] 4개의 행을 검색하지만, flag g가 빠져있어서 검색 대상을 찾는 순간 검색을 멈추기때문에 첫 행의 ['A']만 반환함.
```
