## DataType

- string : 문자열(시퀀스\*)
- boolean : 참/거짓
- int : 정수
- float : 실수
- complex : 복소수
- dictionary : 사전
- list : 리스트(시퀀스)
- tuple : 튜플(시퀀스)
- set : 집합
- \*시퀀스 : 순서가 있다는 의미

### 숫자형 연산자

| 연산자 |      기능      |
| :----: | :------------: |
|   +    |     더하기     |
|   -    |      빼기      |
|   \*   |     곱하기     |
|   /    |     나누기     |
|   //   |   나누기(몫)   |
|   %    | 나누기(나머지) |
|  \*\*  |      제곱      |

- 정수 + 실수 = 실수
- 정수 + 복소수 = 복소수

### 형 변환

```py
print(int(True)) # 1
print(float(4)) # 4.0
print(complex(9.2)) #(9.2+0j)
print(str(2)) # 2 (string 타입)
```

### 참고 사이트

- [math 모듈](https://docs.python.org/3/library/math.html)
- [숫자형 연산자](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex)
