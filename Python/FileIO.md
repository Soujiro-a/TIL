## File I/O

- open 메소드 사용
- 읽기 모드 : r
- 쓰기 모드 : w
- 추가 모드(파일 생성 또는 추가) : a

```py
# 파일 읽기 (텍스트 파일)
# 예시1
f = open('파일경로','r')
content = f.read()
print(content)
f.close() # open으로 열었으면 반드시 close로 닫아주도록 하자

with open('파일경로', 'r') as f:
    # 예시2
    c = f.read()
    print(c)
    # 위와 같이 사용한다면 close로 닫아줄 필요가 없다

    # 예시3
    for c in f:
        print(c) # 한줄씩 출력

    content = f.read()
    print(content)
    # 위의 read 메소드가 불릴 시점에서 이미 안의 파일을 다 읽고 커서가 맨 뒤로 향해힜음
    # 그런 이유로 밑의 content 변수에는 아무런 내용이 담기지 않음
    content = f.read()
    print(content)

    # 예시4
    line = f.readline() # 한 줄씩 읽어오고, 해당 줄의 마지막에 커서가 향해있음
    while line:
        print(line)
        line = f.readline() # 현재 위치한 커서로부터 한 줄을 읽어옴

    # 예시5
    contents = f.readlines() # 각 줄을 리스트 형태로 담음
    for c in contents:
        print(c, end=' ')

# 파일 쓰기

# 예제1
with open('파일경로', 'w') as f:
    f.write("작성할 내용")

# 예제2
with open('파일경로', 'a') as f:
     # 경로에 해당 파일이 존재하면 아래 내용으로 덮어쓰고, 아니라면 새로 파일을 만듬
    f.write("덮어쓸 내용")

with open('파일경로', 'w') as f:
    # 예제3
    list = ['a','b','c']
    f.writelines(list)  # 리스트 -> 파일 저장

    # 예제4
    print("작성할 내용1", file=f)   # 해당하는 파일에 print 내용을 덧붙임
    print("작성할 내용2", file=f)
```
