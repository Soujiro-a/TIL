## Dictionary

- 순서없음
- 중복 불가능
- 수정 가능
- 삭제 가능

```py
# 선언
a = {"name": "Kim", "Phone": "010-1234-5678", "Birth": 980710}
b = {0:"Hello Python", 1:"Hello Coding"}
c = {'arr': [1,2,3,4,5]}

print(type(a)) # <class 'dict'>

print(a['name']) # Kim
print(a.get('name')) # Kim
print(a.get('address')) # None
print(c['arr'][1:3]) # [2,3]

# 추가
a['address'] = 'Seoul'
print(a) # {"name": "Kim", "Phone": "010-1234-5678", "Birth": 980710, "address": "Seoul"}
a['rank'] = [1,3,4]
a['rank2'] = (1,2,3,)

# keys, values, items
print(a.keys()) # dict_keys(['name', 'Phone', 'Birth', 'address', 'rank', 'rank2'])
print(a.values()) # dict_values(['Kim', '010-1234-5678', 980710, 'Seoul', [1,3,4], (1,2,3)])
print(a.items()) # dict_items([('name', 'Kim'), ('Phone', '010-1234-5678'), ('Birth', 980710), ('address', 'Seoul'), ('rank', [1,3,4]), ('rank2', (1,2,3))])

d = list(a.keys())
print(d[1:3]) # ['Phone', 'Birth']

# 그 외
print(2 in b) # False
print('name2' not in a) # True

```
