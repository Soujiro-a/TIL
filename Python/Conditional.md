## Conditional Statements(조건문)

### True/False 종류

- True : "내용", [내용], (내용), {내용}, 1
- False : "", [], (), {}, 0

### 논리 연산자

- x and y
- x or y
- not x y

### 계산 우선 순위

- 산술 > 관계 > 논리로 적용

```py
# 예시1
if True:
    print("Yes")

# 예시2
if False:
    print("No")

# 예시3
if False:
    print("No")
else:
    print("Yes!")

# 관계 연산자
a = 10
b = 0

print(a == b) # True
print(a != b) # True
print(a > b) # True
print(a >= b) # True
print(a < b) # False
print(a <= b) # False

city = ""

if city:
    print("True!")
else:
    print("False!")

# 논리 연산자
c = 100
d = 60
e = 15

print(c > d and d > e) # True
print(c > d or e > d) # True
print(not c > d) # False

# 계산 우선 순위 확인
print(1 + 2 > 0 and not 3 + 4 == 7) # False

score1 = 90
score2 = 'A'

if score >= 90 and score2 == 'A':
    print("합격")
else:
    print("불합격")

# 다중 조건문
num = 90

if num >= 90:
    print("A등급")
elif num >= 80:
    print("B등급")
else:
    print("F등급")
```
