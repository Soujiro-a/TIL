## loop Statements (반복문)

- for
- while

```py
# while 문
v1 = 1
while v1 < 11:
    print("v1 is :", v1)
    v1+=1

# for 문
for v2 in range(1,11):
    print("v2 is :",v2)

# 1~100 합

total = 0
cnt = 1
while cnt <=100:
    total += cnt
    cnt +=1

print(total)

# 시퀀스(순서가 있는)자료형 반복
# iterable 리턴 함수 : range, reversed, enumerate, filter, map, zip 등

names = ["Kim", "Park", "Cho", "Choi", "Yoo"]

for name in names:
    print("You are ", name)

word = "word"

for s in word:
    print("word :", s) # 한글자씩 출력

info = {
    "name" : "Kim",
    "age" : 28,
    "country" : "Korea"
}

# 기본 (키)
for key in info:
    print("key : ", key)

# 키
for key in info.keys():
    print("key : ", key)

# 값
for value in info.values():
    print("value : ", value)

# 키 and 값
for key, value in info.items():
    print("key : ", key)
    print("value : ", value)

name = "kIM Ky"

# 이름 대소문자 변경시 활용 가능
for n in name:
    if n.isupper():
        print(n.lower())
    else:
        print(n.upper())

# break
numbers = [3, 14, 57, 20, 80, 33, 15, 6, 12, 93]

for num in numbers:
    if num == 33:
        print("found 33")
        break # 33을 찾았을 경우 더 이상 반복문을 실행하지 않음
    else:
        print("not found 33")

# for - else 구문
# for 문이 정상적으로 끝까지 수행 된 경우 else 블럭을 수행
for num in numbers:
    if num == 33:
        print("found 33")
        break # 33을 찾았을 경우 더 이상 반복문을 실행하지 않음
    else:
        print("not found 33")
else: # break로 빠져나온 경우에는 해당 블럭이 수행되지 않음
    print("not found 33...")

# continue

lt = ["2", 3, 4, False, 5.6, complex(7)]

for v in lt:
    if type(v) is Float:
        continue # 아랫 부분은 수행되지 않고 다음 순회할 값으로 이동하여 다시 수행
    print("타입 :", type(v))
```
