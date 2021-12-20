## Exception (예외 처리)

항상 예외가 발생하지 않을 것으로 가정하고 먼저 코딩을 진행
그 후 런타임 때 예외 발생 시, 예외 처리 코드 작성을 권장함 (EAFP 코딩 스타일)
문법 에러뿐만 아니라, 코드 실행(런타임) 프로세스에서 발생하는 예외 처리도 중요함

### 에러 종류

- SyntaxError : 잘못된 문법
- NameError : 참조변수 없음
- ZeroDivisionError : 0 나누기 에러
- IndexError : 인덱스 범위가 오버됨
- KeyError : 없는 키를 조회하려고 함
  - 키를 사용하여 다이렉트로 접근하기보단, get 메소드를 통해 접근하는게 안전
    - 키에 해당하는 값이 없을 경우 None 반환
- AttributeError : 모듈, 클래스에 있는 잘못된 속성 사용시 발생
- ValueError : 참조 값이 없을 때 발생
- FileNotFoundError : 파일을 찾을 수 없을 때 발생
- TypeError : 타입이 다른 값들을 연산하려고 할 때 발생

### 기본적인 예외 처리 방법

- try : 에러가 발생할 가능성이 있는 코드 실행
- except : 에러명1
- except : 에러명2
- else : 에러가 발생하지 않았을 경우 실행
- finally : 항상 실행

```py
name = ["Kim", "Lee", "Park"]
try:
    z = 'Kim' # name에 없는 값으로 하면 예외 발생
    x = name.index(z)
    print('{} Found it! in name'.format(z, x+1))
except ValueError:
    print("Not found it! - Occurred ValueError")
except IndexError:
    print("Not found it! - Occurred IndexError")
except Exception: # 어떤 에러인지 모를 때 작성하는 처리 방법
    print("Not found it! - Occurred Error")
else:
    print("OK! else!")
finally:
    print("finally OK!")
```
