# 240725 - Python 08: OOP 2 & Exception
> ## Index
> 
> 1) 상속 `Inheritance`
> 2) 내장 함수 `super()`
> 3) `에러`와 `예외`
> 4) 예외 처리: `try` - `except`
> ---

<br>

### 1) 상속 `Inheritance`
---

- `상속 Inheritance`

    - 기존 클래스의 속성과 메서드를 물려받아 새로운 하위 클래스를 생성하는 것

<br>

- 상속이 필요한 이유

    - `코드 재사용`

        - 상속을 통해 기존 클래스의 속성과 메서드(기능) 재사용 가능
        
        - 새로운 클래스를 작성할 때 중복된 코드를 줄일 수 있음

    - `계층 구조`

        - 상속을 통해 클래스들 간의 계층 구조를 형성할 수 있음
        
        - 부모 클래스와 자식 클래스 간의 관계를 표현하고, 더 구체적인 클래스를 만들 수 있음

    - `유지 보수의 용이성`

        - 상속을 통해 기존 클래스의 수정이 필요한 경우, 해당 클래스만 수정하면 되므로 유지 보수 용이

        - 코드의 일관성을 유지하고, 수정이 필요한 범위를 최소화할 수 있음

<br>

- 클래스 상속

    - `단일 상속`

    ``` python
    # 상속 없는 경우 - 1
    class Person:
        def __init__(self, name, age):
            self.name = name
            self.age = age
        def talk(self):
            print(f'반갑습니다. {self.name}입니다.')

    s1 = Person('김학생', 23)
    s1.talk()  # 반갑습니다. 김학생입니다.

    p1 = Person('박교수', 59)
    p1.talk()  # 반갑습니다. 박교수입니다.


    # 상속 없는 경우 - 2
    class Professor:
        def __init__(self, name, age, department):
            self.name = name
            self.age = age
            self.department = department

        def talk(self):  # 중복
            print(f'반갑습니다. {self.name}입니다.')

    class Student:
        def __init__(self, name, age, gpa):
            self.name = name
            self.age = age
            self.gpa = gpa

        def talk(self):  # 중복
            print(f'반갑습니다. {self.name}입니다.')


    # 상속을 사용한 계층구조 변경
    class Person:
        def __init__(self, name, age):
            self.name = name
            self.age = age

        def talk(self):  # 메서드 재사용
            print(f'반갑습니다. {self.name}입니다.')


    class Professor(Person):
        def __init__(self, name, age, department):
            self.name = name
            self.age = age
            self.department = department


    class Student(Person):
        def __init__(self, name, age, gpa):
            self.name = name
            self.age = age
            self.gpa = gpa


    p1 = Professor('박교수', 49, '컴퓨터공학과')
    s1 = Student('김학생', 20, 3.5)

    # 부모 Person 클래스의 talk 메서드를 활용
    p1.talk()  # 반갑습니다. 박교수입니다.

    # 부모 Person 클래스의 talk 메서드를 활용
    s1.talk()  # 반갑습니다. 김학생입니다.
    ```

<br>

- `다중 상속`

    - 둘 이상의 상위 클래스로부터 여러 행동이나 특징을 상속받을 수 있는 것

    - 상속받은 `모든 클래스의 요소`를 활용 가능

    - 중복된 속성이나 메서드가 있는 경우 `상속 순서`에 의해 결정됨

    ``` python
    # 다중 상속 예시
    class Person:
        def __init__(self, name):
            self.name = name

        def greeting(self):
            return f'안녕, {self.name}'


    class Mom(Person):
        gene = 'XX'

        def swim(self):
            return '엄마가 수영'


    class Dad(Person):
        gene = 'XY'

        def walk(self):
            return '아빠가 걷기'


    class FirstChild(Dad, Mom):

        def __init__(self, name):
            super().__init__(name)
            
        def swim(self):
            return '첫째가 수영'

        def cry(self):
            return '첫째가 응애'


    baby1 = FirstChild('아가')
    print(baby1.cry())  # 첫째가 응애
    print(baby1.swim())  # 첫째가 수영
    print(baby1.walk())  # 아빠가 걷기
    # print(baby1.gene)  # XY
    ```

<br>

    - 다이아몬드 문제 `The diamond problem`

        - 두 클래스 B와 C가 A에서 상속되고 클래스 D가 B와 C 모두에서 상속될 때 발생하는 모호함

        ---

        ![image](https://postfiles.pstatic.net/MjAyNDA3MjVfNjgg/MDAxNzIxODY2OTQzNTUw.gcwUMMCOUFZKXSTA0AVxbAM2h51n3JHbg3MnadWptmAg.ladwVWVnBJZtc5sq3J7mxO6r_vXuS4r3FLAO4ZEn_rwg.PNG/%EA%B7%B8%EB%A6%BC1.png?type=w773)

        ---

        - B와 C가 재정의한 메서드가 A에 있고 D가 이를 재정의하지 않은 경우
        
            - D는 B의 메서드 중 어떤 버전을 상속하는가?
            
            - 아니면 C의 메서드 버전을 상속하는가?

<br>


- 해결책: `MRO(Method Resolution Order)`

    - 메서드 결정 순서

    - `mro() 메서드` (Ex. class_name.mro())
    
        - 해당 인스턴스의 클래스가 어떤 부모 클래스를 가지는지 확인하는 메서드
        
        - 기존의 인스턴스 → 클래스 순으로 이름 공간을 탐색하는 과정에서 상속 관계에 있으면 인스턴스 → 자식 클래스 → 부모 클래스로 확장
        
        - MRO가 필요한 이유
        
            - 부모 클래스들이 여러 번 액세스되지 않도록 각 클래스에서 지정된 왼쪽에서 오른쪽으로 가는 순서 보존을 위해 각 부모를 오직 한 번만 호출하고, 우선순위에 영향을 주지 않으며 서브 클래스를 만드는 단조적인 구조 형성
            
            - 프로그래밍 언어의 신뢰성 있고 확장성 있는 클래스 설계에 도움
            
            - 클래스 간의 메서드 호출 순서가 예측되며, 코드의 재사용성과 유지 보수성 향상

``` python
class A:
    def __init__(self):
        print('A Constructor')


class B(A):
    def __init__(self):
        super().__init__()
        print('B Constructor')


class C(A):
    def __init__(self):
        super().__init__()
        print('C Constructor')


class D(B, C):
    def __init__(self):
        super().__init__()
        print('D Constructor')


# [<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
print(D.mro())
```


<br>
<br>

### 2) 내장 함수 `super()`
---

> `super()`

- 부모 클래스 객체를 반환하는 내장 함수

- 현재 클래스가 상속하는 모든 부모 클래스 중 다음에 호출될 메서드를 결정하여 자동 호출

<br>

> 단일 상속 구조

- 명시적으로 이름을 지정하지 않고, 부모 클래스를 참조하여 코드의 유지 관리 용이

- 클래스 이름이 변경되거나 부모 클래스가 교체되어도 super()를 사용하면 코드 수정 적음

<br>

> 다중 상속 구조

- MRO를 따른 메서드 호출

- 복잡한 다중 상속 구조에서 발생할 수 있는 문제를 방지

<br>

``` python
# super 사용 전
class Person:
    def __init__(self, name, age, number, email):
        self.name = name
        self.age = age
        self.number = number
        self.email = email


class Student(Person):
    def __init__(self, name, age, number, email, student_id):
        self.name = name
        self.age = age
        self.number = number
        self.email = email
        self.student_id = student_id


# super 사용 예시 - 단일 상속
class Person:
    def __init__(self, name, age, number, email):
        self.name = name
        self.age = age
        self.number = number
        self.email = email

class Student(Person):
    def __init__(self, name, age, number, email, student_id, gpa):
        super().__init__(name, age, number, email)
        self.student_id = student_id
        self.gpa = gpa


# super 사용 예시 - 다중 상속
class ParentA:
    def __init__(self):
        self.value_a = 'ParentA'

    def show_value(self):
        print(f'Value from ParentA: {self.value_a}')


class ParentB:
    def __init__(self):
        self.value_b = 'ParentB'

    def show_value(self):
        print(f'Value from ParentB: {self.value_b}')


class Child(ParentA, ParentB): # class Child는 인스턴스 변수 2개를 가짐
    def __init__(self):
        super().__init__()
        self.value_c = 'Child'

child1 = Child()
print(child1.value_a) # 상속받은 __init__에서 얻은 인스턴스 변수
print(child1.value_c) # 본래 class Child가 가지고 생긴 인스턴스 변수
print(child1.value_b) # AttributeError: 'Child' object has no attribute 'value_b'
```

<br>

> 상속 이후 메서드 사용 예시

``` python
# 자식 클래스에서 부모 클래스의 클래스 메서드 호출하기


class Animal:
    total_count = 0

    def __init__(self, name):
        self.name = name
        Animal.total_count += 1

    @classmethod
    def get_total_count(cls):
        return f'전체 동물 수: {cls.total_count}'


class Dog(Animal):
    dog_count = 0

    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
        Dog.dog_count += 1

    @classmethod
    def get_dog_info(cls):
        # cls.get_total_count()는 부모 클래스의 클래스 메서드를 호출하여 전체 동물 수를 출력
        return f'{cls.get_total_count()}, 강아지 수: {cls.dog_count}'


class Cat(Animal):
    cat_count = 0

    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
        Cat.cat_count += 1

    @classmethod
    def get_cat_info(cls):
        # cls.get_total_count()는 부모 클래스의 클래스 메서드를 호출하여 전체 동물 수를 출력
        return f'{cls.get_total_count()}, 고양이 수: {cls.cat_count}'


dog1 = Dog('멍멍이', '삽살개')
dog2 = Dog('바둑이', '진돗개')
print(Dog.get_dog_info())  # 출력: 전체 동물 수: 2, 강아지 수: 2


cat1 = Cat('노아', '페르시안')
cat2 = Cat('루비', '코숏')
print(Cat.get_cat_info())  # 출력: 전체 동물 수: 4, 고양이 수: 2
```

<br>
<br>


### 3) `에러`와 `예외`
---
우리는 흔히 소프트웨어에서 발생하는 오류 또는 결함, 즉 프로그램의 예상된 동작과 실제 동작 사이의 불일치에 대해 `버그 bug`라고 한다. 그리고 소프트웨어에서 발생하는 버그를 찾아내고 수정하는 과정을 가리켜 `디버깅 Debugging`이라고 하며, 이와 같은 프로그램의 오작동 원인을 식별하여 수정하는 작업에는 다양한 방법이 존재한다.

<br>

- `Print 함수` 활용

    - 특정 함수 결과, 반복/조건 결과 등 나눠서 생각
    - 코드를 bisection으로 나눠서 생각

- `개발 환경(text editor, IDE 등)에서 제공하는 기능` 활용

    - breakpoint, 변수 조회 등

- `Python tutor` 활용

    - 단순 파이썬 코드인 경우

- 뇌 컴파일, 눈 디버깅 등

<br>

### ✔ 에러 `Error`
---
프로그램 실행 중에 발생하는 예외 상황


> 문법 에러 Syntax Error

- 프로그램의 구문이 올바르지 않은 경우 발생

- 오타, 괄호 및 콜론 누락 등의 문법적 오류

    - invalid syntax (문법 오류)
    - assign to literal (잘못된 할당)
    - EOL (End of Line)
    - EOF (End of File)

> 예외 Exception

- 프로그램 실행 중에 감지되는 에러

- 내장 예외 `Built-in Exceptions`

    ``` python
    파이썬 내에는 예외 상황을 나타내는 예외 '클래스'들이 이미 정의되어 있다. 이들은 특정 예외 상황에 대한 처리를 위해 사용되며, 클래스이기 때문에 상속이 가능하여 '계층 구조'가 존재할 수 있다.
    ```

    - `ZeroDivisionError` (나누기 또는 모듈로 연산의 두 번째 인자가 0일 때)

    - `NameError` (지역 또는 전역 이름을 찾을 수 없을 때)

    - `TypeError` (타입 불일치, 인자 누락 및 초과, 인자 타입 불일치)

    - `ValueError` (부적절한 값의 인자를 받거나, IndexError처럼 구체적 설명 불가한 경우)

    - `IndexError` (시퀀스 인덱스가 범위를 벗어날 때 발생)

    - `KeyError` (딕셔너리에 해당 키가 존재하지 않는 경우)

    - `ModuleNotFoundError` (모듈을 찾을 수 없을 때)

    - `ImportError` (모듈은 있으나 import하려는 이름을 찾을 수 없을 때)

    - `KeyboardInterrupt` (사용자가 Control-C 또는 Delete를 누를 때)

    - `IndentationError` (잘못된 들여쓰기와 관련된 문법 오류)


<br>
<br>

### 4) 예외 처리: `try` - `except`
---
파이썬에는 앞서 설명한 예외가 발생했을 때 프로그램이 비정상적으로 종료되지 않고, 적절하게 처리할 수 있도록 하는 `예외 처리 Exception Handling` 구문이 존재한다.

<br>

> 예외 처리 사용 구문

- `try`

    - 예외가 발생할 수 있는 코드 작성

- `except`

    - 예외가 발생했을 때 실행할 코드 작성

- `else`

    - 예외가 발생하지 않았을 때 실행할 코드 작성

- `finally`

    - 예외 발생 여부와 상관없이 항상 실행할 코드 작성

<br>

> `try - except` 구조

- try 블록 안에는 예외가 발생할 수 있는 코드 작성

- except 블록 안에는 예외가 발생했을 때 처리할 코드 작성

- 예외가 발생 시 프로그램은 try 블록을 빠져나와 해당 예외에 대응하는 except 블록으로 이동

<br>

``` python
try:
    result = 10 / 0
except ZeroDivisionError: # 이렇게만 쓰는 경우에는 except: 라고만 써도 가능
    print('0으로 나눌 수 없습니다.')

try:
    num = int(input('숫자 입력: '))
except ValueError:
    print('숫자가 아닙니다.')
```

<br>

> 복수 예외 처리 예시

``` python
try:
    num = int(input('100을 나눌 값을 입력하시오: '))
    print(100 / num)
except (ValueError, ZeroDivisionError):
    print('제대로 입력하라고')


try:
    num = int(input('100을 나눌 값을 입력하시오: '))
    print(100 / num)
except ValueError:
    print('숫자를 입력해')
except ZeroDivisionError:
    print('0으로는 나눌 수 없어')
except:
    print('알 수 없는 에러가 발생했습니다.')
```

<br>

> `else & finally`

``` python
try:
    x = int(input('숫자를 입력하세요: '))
    y = 10 / x
except ZeroDivisionError:
    print('0으로 나눌 수 없습니다.')
except ValueError:
    print('유효한 숫자가 아닙니다.')
else:
    print(f'결과: {y}')
finally:
    print('프로그램이 종료되었습니다.')
```

<br>

> 예외 처리 주의사항

- 내장 예외의 상속 계층 구조 주의

    - 내장 예외 클래스는 상속 계층 구조를 가지기 때문에 except 절로 분기 시 `반드시 하위 클래스를 먼저 확인`할 수 있도록 작성해야 함

    - 참고 자료

        [python 공식 문서 - 내장 예외](https://docs.python.org/ko/3/library/exceptions.html#exception-hierarchy)



    - 문제 상황 예제
        ``` python
        try: # 문제 상황
            num = int(input('100으로 나눌 값을 입력하시오 : '))
            print(100 / num)
        except BaseException:
            print('숫자를 넣어주세요.')
        except ZeroDivisionError:
            print('0으로 나눌 수 없습니다.')
        except:
            print('에러가 발생하였습니다.')


        try: # 해결
            num = int(input('100으로 나눌 값을 입력하시오 : '))
            print(100 / num)
        except ZeroDivisionError:
            print('0으로 나눌 수 없습니다.')
        except BaseException:
            print('숫자를 넣어주세요.')
        except:
            print('에러가 발생하였습니다.')
        ```

    - 위와 같이 작성하면 코드는 2번째 except 절에 이후로 도달하지 못함

    - BaseException 클래스의 하위 클래스 중 하나인 ZeroDivisionError 클래스에 대한 except 절을 실행하기 위해서는 스크립트 내에 ZeroDivisionError를 먼저 작성해야 함

<br>

> 예외 객체 다루기: `키워드 as`

- `예외 객체` : 예외가 발생했을 때 예외에 대한 정보를 담고 있는 객체

- except 블록에서 예외 객체를 받아 상세한 예외 정보를 활용 가능

    ``` python
    my_list = []

    try:
        number = my_list[1]
    except IndexError as error:
        # list index out of range가 발생했습니다.
        print(f'{error}가 발생했습니다.')
    ```

<br>

> `try - except`와 `if - else`

- 함께 사용 가능한 구문임을 기억

    ``` python
    try:
    x = int(input('숫자를 입력하세요: '))
    if x < 0:
        print('음수는 허용되지 않습니다.')
    else:
        print('입력한 숫자:', x)
    except ValueError:
        print('오류 발생')
    ```

<br>

> `EAFP` & `LBYL`

- 예외 처리와 값 검사에 대한 2가지 접근 방식

- `EAFP(Easier to Ask for Forgivenesss than Permission)`

    - 예외 처리를 중심으로 코드를 작성하는 접근 방식 (try - except)

- `LBYL(Look Before You Leap)`

    - 값 검사를 중심으로 코드를 작성하는 접근 방식 (if - else)

<br>

| EAFP | LBYL |
| :-----: | :---: |
| `일단 실행`하고 예외를 처리 | 실행하기 전에 `조건을 검사` |
| 코드를 실행하고 예외가 발생하면 예외 처리를 수행 | 코드 실행 전에 조건문 등을 사용하여 예외 상황을 미리 검사하고, 예외 상황을 피하는 방식 |
| 코드에서 예외가 발생할 수 있는 부분을 미리 예측하여 대비하는 것이 아니라, `예외가 발생한 후에 예외를 처리` | 코드가 좀 더 `예측 가능한 동작`을 하지만, 코드가 더 길고 복잡해질 수 있음 | 
| 예외 상황을 `예측하기 어려운 경우`에 유용 | 예외 상황을 `미리 방지하고 싶을 때` 유용 | 

<br>

``` python
my_dict = {'key': 'value'}

# EAFP (Easier to Ask for Forgiveness than Permission)
try:
    result = my_dict['key']
    print(result)
except KeyError:
    print('Key가 존재하지 않습니다.')


# LBYL (Look Before You Leap)
if 'key' in my_dict:
    result = my_dict['key']
    print(result)
else:
    print('Key가 존재하지 않습니다.')
```