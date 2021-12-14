## String

```py
str1 = 'asdf';

# 문자의 길이
print(len(str1))

# Raw String
raw_str1 = r'C:\Programs\Test\Bin'

# 멀티라인
multi_str = \
"""
문자열
멀티라인
"""

# 문자열 연산
str2 = "*"
str3 = "abc"

print(str2*100) # ***...(100개)
print(str2+str3) # *abc
print('a' in str2) # True
print('a' not in str2) # False

# 문자열 형 변환
print(str(10)+'a') # 10a (string 타입)
```

### 참고 사이트

- [문자열 함수](https://www.w3schools.com/python/python_ref_string.asp)
