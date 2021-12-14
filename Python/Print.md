## Print

- 결과값을 콘솔에 출력하기위한 함수

### 사용 예시

```py
# 기본 출력
print('Hello World!')
print("Hello World!")
print('''Hello World!''')
print("""Hello World!""")

# Separator 옵션
print("test", "gmail.com", sep='@') # test@gmail.com

# end 옵션
print('Hello', end=' ')
print('World', end='!') # 위의 print 함수와 합쳐져 Hello World!

# format 옵션
print('{} and {}'.format('apple', 'banana')) # apple and banana
print('{0} are {1}'.format('you', 'developer')) # you are developer
print('{a} or {b}'.format(a='rice', b='bread')) # rice or bread

# 원하는 값 출력
# %s : 문자, %d : 정수, %f : 실수

# Banana : 123cm, Price: 1234.567$
print("Banana: %3dcm, Price: %4.2f$" %(123, 1234.567))
print("Banana: {a: %3d}cm, Price:{b:%4.2f}$" %(a=123, b=1234.567))
```

### 이스케이프 문자

| 문자 |                    기능                    |
| :--: | :----------------------------------------: |
|  \n  |        개행(커서를 다음 줄로 이동)         |
|  \r  | 캐리지 리턴(커서를 현재 줄 맨 앞으로 이동) |
|  \t  |                     탭                     |
|  \\  |                   문자\|                   |
|  \'  |                   문자'                    |
|  \"  |                   문자"                    |
|  \f  |                  폼 피드                   |
|  \a  |                  벨 소리                   |
|  \b  |                백 스페이스                 |
| \000 |                 Null 문자                  |
