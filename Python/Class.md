## Class

- 네임스페이스 : 객체를 인스턴스화 할 때 저장된 공간
- 클래스 변수 : 직접 사용 가능, 객체보다 먼저 생성
- 인스턴스 변수 : 객체마다 별도로 존재, 인스턴스 생성 후 사용 가능

```py
class User:
    total = 0 # 클래스 변수
    def __init__(self, name): # 인스턴스 생성 시 실행되는 매직 메소드
        self.name = name
        User.total += 1
    def printCount(): # 클래스 메소드
        print(User.total)
    def printName(self): # 인스턴스 메소드
        print(self.name)
    def __del__(self): # 인스턴스 삭제 시 실행되는 매직 메소드
        User.total -= 1

user1 = User('Code')
user2 = User('Hello')

# user1.printCount() # 오류 발생
User.printCount() # 2

user1.printName() # Code
user2.printName() # Hello

print(user1.total) # 2, 조회 가능
print(user2.total) # 2

del user1 # class 내의 __del__ 매직 메소드 실행

User.printCount() # 1
```

### 상속

- 서브 클래스(자식)에서 슈퍼 클래스(부모)의 속성, 메소드도 모두 사용 가능
- 코드를 재사용할 수 있고, 중복 코드를 최소화할 수 있음

```py
class Car:
    """Parent Class"""
    def __init__(self, tp, color):
        self.type = tp
        self.color = color
    def show(self):
        return 'Car Class "Show Method!"'

class BmwCar(Car):
    """Sub Class"""
    def __init__(self, name, tp, color):
        super().__init__(tp, color)
        self.name = name

    def show_model(self) -> None:
        return "Your Car Name : %s" % self.name

class BenzCar(Car):
    """Sub Class"""
    def __init__(self, name, tp, color):
        super().__init__(tp, color)
        self.name = name

    def show_model(self) -> None:
        return "Your Car Name : %s" % self.name

    # Method Overriding(오버라이딩)
    def show(self):
        print(super().show()) # Parent Method Call
        return 'Car Info : %s %s %s' %(self.name, self.type, self.color)

# 일반 사용
model1 = BmwCar('520d', 'sedan', 'red')

print(model1.color) # Super
print(model1.type) # Super
print(model1.name) # Sub
print(model1.show()) # Super
print(model1.show_model()) # Sub
print(model1.__dict__) # {'type': 'sedan', 'color': 'red', 'name': '520d'}

model2 = BenzCar("220d", "suv", "black")
print(model2.show())

# 상속 정보 조회(리스트)
print(BmwCar.mro())
```

#### 다중 상속

- 새 클래스를 선언할 때 매개변수로 다른 클래스들을 여러개 넣어줌으로서 다중 상속을 할 수 있음

```py
class X():
    pass

class Y():
    pass

class Z():
    pass

class A(X,Y):
    pass

class B(Y,Z):
    pass

class C(B,A,Z):
    pass
```
