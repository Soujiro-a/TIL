## Set

- 순서없음
- 중복 불가능
- 수정 가능
- 삭제 가능

```py
# 선언
a = set()
b = set([1,2,3,4])
c = set([1,4,5,6,6])

print(type(a)) # <class 'set'>

print(c) # {1,4,5,6}

t = tuple(b)
print(t) # (1,2,3,4)
l = list(c)
print(l) # [1,4,5,6]

s1 = set([1,2,3,4,5,6])
s2 = set([4,5,6,7,8,9])

# 교집합
print(s1.intersection(s2)) # {4,5,6}
print(s1 & s2)

# 합집합
print(s1.union(s2)) # {1,2,3,4,5,6,7,8,9}
print(s1 | s2)

# 차집합
print(s1.difference(s2)) # {1,2,3}
print(s1 - s2)

# 추가/제거
s3 = set([7,8,10,15])
s3.add(18)
s3.add(7)
print(s3) # {7,8,10,15,18}

s3.remove(8)
print(s3) # {7,10,15,18}
```
