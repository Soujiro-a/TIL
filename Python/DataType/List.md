## List

- 순서있음
- 중복 가능
- 수정 가능
- 삭제 가능

```py
# 선언
a = [1,2,3,4]
b = list() # []
c = [1, 10, ["apple", "banana", "kiwi"]]

# 인덱싱
print(a[1]) # 2
print(a[-2]) # 3
print(a[3]+c[1]) # 4+10 = 14
print(c[-1][0]) # apple

# 슬라이싱
print(a[0:2]) # [1,2]
print(c[2][1:3]) # ["banana", "kiwi"]

# 연산
print(a+c) # [1,2,3,4,1,10,["apple", "banana", "kiwi"]]
print(a*3) # [1,2,3,4,1,2,3,4,1,2,3,4]

# 리스트 수정
c[0] = 100
print(c) # [100,10,["apple", "banana", "kiwi"]]
c[1:2] = [1000, 10000]
print(c) # [100,[1000, 10000],["apple", "banana", "kiwi"]]

# 리스트 삭제
del c[0]
print(c) # [[1000, 10000],["apple", "banana", "kiwi"]]

# 리스트 함수
d = [5,2,3,1,4]
d.append(6)
print(d) # [5,2,3,1,4,6]
d.sort()
print(d) # [1,2,3,4,5,6]
d.reverse()
print(d) # [6,5,4,3,2,1]
d.insert(3, 8)
print(d) # [6,5,4,8,3,2,1]
d.remove(3)
print(d) # [6,5,4,8,2,1]
d.pop()
print(d) # [6,5,4,8,2]
ex = [12, 34]
d.append(ex)
print(d) # [6,5,4,8,2,[12,34]]
d.extend(ex)
print(d) # [6,5,4,8,2,[12,34],12,34]
```

### List Comprehension

- 예시) 1~100까지 배열을 만드는 방법

```py
# 일반적인 방법
numbers = []

for n in range(1,101):
    numbers.append(n)

# List Comprehension
numbers2 = [x for x in range(1,101)]
```
