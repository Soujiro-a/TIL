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

## 정규식 패턴

|                                    제목                                     | 내용                                                          |
| :-------------------------------------------------------------------------: | :------------------------------------------------------------ | ------------------------------------------ |
|                                      ^                                      | 문자열의 시작에서 일치                                        |
|                                      $                                      | 문자열의 끝에서 일치                                          |
|                                      .                                      | (특수기호, 공백을 포함한) 임의의 한 문자                      |
|                                     `a                                      | b`                                                            | a or b, 인덱스가 작은 것을 우선적으로 반환 |
|                                     \*                                      | 0회 이상 연속으로 반복되는 문자와 가능한 많이 일치 (={0,})    |
|                                     \*?                                     | 0회 이상 연속으로 반복되는 문자와 가능한 적게 일치 (={0})     |
|                                      +                                      | 1회 이상 연속으로 반복되는 문자와 가능한 많이 일치 (={1,})    |
|                                     +?                                      | 1회 이상 연속으로 반복되는 문자와 가능한 적게 일치 (={1})     |
|                                     {4}                                     | 숫자 4개 연속 일치                                            |
|                                    {4,}                                     | 숫자 4개 이상 연속 일치                                       |
|                                   {4, 7}                                    | 숫자 4개 이상 7개 이하 연속 일치                              |
|                                     ()                                      | 캡쳐할 그룹                                                   |
|                                     [^]                                     | []안에서 문자열 앞에 ^이 쓰일 경우, []안에 없는 문자를 검색함 |
|                                    [a-z]                                    | a~z사이의 문자 구간에 일치 (소문자)                           |
|                                    [A-Z]                                    | A~Z사이의 문자 구간에 일치 (대문자)                           |
|                                    [0-9]                                    | 0~9사이의 문자 구간에 일치 (숫자)                             |
| \|escape 문자. 특수 기호앞에 붙이면 정규식 패턴이 아니라 기호 자체로 인식함 |
|                                     \d                                      | 숫자를 검색함. [0-9]와 동일                                   |
|                                     \D                                      | 숫자가 아닌 문자를 검색함 [^0-9]와 동일                       |
|                                     \w                                      | 영어 대소문자, 숫자, underbar를 검색함. [A-Za-z0-9_]와 동일   |
|                                     \W                                      | \w와 일치하지 않는 문자를 검색함. [^a-za-z0-9_]와 동일        |

### Anchors : ^, $

```js
"coding is difficult".match(/^co/); // ['co']
"coding is difficult".match(/^difficult/); // null

// ^는 문자열 처음을 의미하며, 뒤에 붙은 표현식으로 시작하는 부분을 찾음.
// 일치하는 부분이 있더라도, 문자열의 시작 부분이 아니면 null을 반환함.

"coding is difficult".match(/cult$/); // ['cult']
"coding is difficult".match(/is$/); // null

// $는 문자열 끝을 의미하며, 앞에 붙은 표현식으로 끝나는 부분을 찾음.
// 일치하는 부분이 있더라도, 문자열의 끝 부분이 아니면 null을 반환함.

"coding is difficult".match(/^coding is difficult$/); // ['coding is difficult']
// 문자열을 ^와$로 감싸주면 그 사이에 들어간 문자열과 정확히 일치하는 부분을 찾음.
```

### Quantifiers : \*, +, ?, {}

```js
"a ab abc abcd abcdddd abcdifficult".match(/bcd*/g); // ['bc', 'bcd', 'bcdddd', 'bcd']

// *는 바로 앞의 문자가 0번 이상 나타나는 경우를 검색함.
// /bcd*/g 를 사용하게 되면, 'bc'가 들어가면서 그 뒤에 d가 0번이상 포함된 모든 문자열을 반환함.

"a ab abc abcd abcdddd abcdifficult".match(/bcd+/g); // ["bcd", "bcdddd", "bcd"]

// *와 같은 방식으로 작동하지만, 바로 앞의 문자가 1번 이상 나타나는 경우만 검색한다는 점이 다름.

"a ab abc abcd abcdddd abcdifficult".match(/bcd?/g); // ["bc", "bcd", "bcd", "bcd"]
"a ab abc abcd abcdddd abcdifficult".match(/bcd*?/g); // ["bc", "bc", "bc", "bc"]
"a ab abc abcd abcdddd abcdifficult".match(/bcd+?/g); // ["bcd", "bcd", "bcd"]

// ?는 앞의 문자가 0번 혹은 1번 나타나는 경우만 검색함.
// *?일 경우는 0번 나타날 때, +?일 경우는 1번 나타날 때의 경우만 검색하는 것을 확인할 수 있음.

"a ab abc abcd abcdddd abcdifficult".match(/bcd{1,4}/g); // ["bcd", "bcdddd", "bcd"]

// *, +, ? 보다 범용성이 좋아, 직접 숫자를 넣어서 연속되는 갯수를 정할 수 있음
// /bcd{1,4}/g를 사용하게 되면, 'd'를 1개이상 4개 이하 포함한 문자열을 검색함.
```

### Or operator : |

```js
"aA bB cC dD".match(/A|b/g); // ["A", "b"]
"AAaa Bbb cCc dddDD".match(/A+|d+/g); // ["AA", "ddd"]

// |는 or조건으로 검색하여, 왼쪽 혹은 오른쪽의 검색결과를 반환함.
```

### Bracket Operator : [ ]

```js
"Aaaa BBbb CCCc DDDD".match(/[aD]+/g); // ["aaa", "DDDD"]

// a or D가 한 번 이상 반복된 문자열을 반환.

"Aaaa BBbb CCCc DDDD".match(/[a-d]+/g); // ["aaa", "bb", "c"]

// a or b or c or d 가 한 번 이상 반복된 문자열을 반환.

"Aaaa BBbb 1234 CCCc DDDD".match(/[A-Da-d]+/g);
"Aaaa BBbb 1234 CCCc DDDD".match(/[A-D]+/gi);
// ["Aaaa", "BBbb", "CCCc", "DDDD"]

// /[A-Da-d]+/g : A~D, a~d에서 한번 이상 반복되는 문자열을 반환.
// /[A-D]+/gi : flag i를 써서 대소문자 구분을 없앰.
```

### Character classes : \d, \w

```js
"q1w2e3r4".match(/\d/); // ["1"]
"q1w2e3r4".match(/\d/g); // ["1", "2", "3", "4"]
"q1w2e3r4".match(/\D/); // ["q"]
"q1w2e3r4".match(/\D/g); // ["q", "w", "e", "r"]

// \d === [0-9], \D === [^0-9], d <=> D
// d는 digit을 의미하며 숫자를 검색하는데 사용됨.

"q1w2_e3r4@abc.kr".match(/\w/); // ["q"]
"q1w2_e3r4@abc.kr".match(/\w/g);
// ["q", "1", "w", "2", "_", "e", "3", "r", "4", "a", "b", "c", "k", "r"]
"q1w2_e3r4@abc.kr".match(/\W/); // ["@"]
"q1w2_e3r4@abc.kr".match(/\W/g); // ["@", "."]

// w는 특수문자를 제외한 나머지 문자들을 검색하는데 사용됨. w<=>W
```

### Grouping and Capturing : ()

```js
"abab".match(/ab+/); // ["ab", index: 0, input: "abab", groups: undefined]
"abbbabbb".match(/ab+/); // ["abbb", index: 0, input: "abbbabbb", groups: undefined]

"abab".match(/(ab)+/); // ["abab", "ab", index: 0, input: "abab", groups: undefined]
"abbbabbb".match(/(ab)+/); // ["ab", "ab", index: 0, input: "abbbabbb", groups: undefined]

// /ab+/ : a를 검색하고 b가 1회 이상 연속으로 반복되는 문자를 검색
// /(ab)+/ : "ab"가 1회 이상 연속으로 반복되는 문자를 검색 => Grouping
/* 
    /(ab)+/의 작동방식.
        1.()로 "ab"를 캡쳐
        2. 캡쳐한 "ab"는 놔두고, + 표현식이 Grouping한 "ab"츼 1화 이상 연속으로 반복되는 문자를 검색
        3. 캡쳐 이외의 표현식이 다 끝난 뒤, 캡쳐해두었던 "ab"를 검색.
*/

"coding hard".replace(/(\w+)\ (\w+)/, "$2 $1"); // "hard coding"

// 위와 같이 replace 메소드를 사용한 문자 치환 시 참조 패턴으로 사용될 수 있음.
// 첫번쨰 (\w+)가 "coding"을, 두번째 (\w+)가 "hard"를 캡쳐.
// (사이의 공백은 \를 사용하여 두 문자 사이의 공백을 나타내기 위함임)
// 캡쳐된 값은 순서대로 $1,$2와 같이 참조하기때문에 위와 같은 결과를 얻을 수 있음.
```

### Non-capturing : `(?:)`

```js
"abab".match(/(ab)+/); // ["abab", "ab", index: 0, input: "abab", groups: undefined]
"abab".match(/(?:ab)+/); // ["abab", index: 0, input: "abab", groups: undefined]

// (?:)표현식을 이용하여 그룹은 만들지만, 캡쳐는 하지 않도록 할 수 있음.
```

### lookahead : (?=)

```js
"abcde".match(/ab(?=c)/); // ["ab", index: 0, input: "abcde", groups: undefined]

// "ab"가 "c"앞에 있기때문에 ["ab"]를 반환함

"abcde".match(/ab(?=d)/); // null

// "d"앞에는 "abc'가 있기 때문에 null을 반환함.

// nagated : (?!) => (?=)의 부정 형태로 사용
"abcde".match(/ab(?!c)/); // null
"abcde".match(/ab(?!d)/); // ["ab", index: 0, input: "abcde", groups: undefined]
```
