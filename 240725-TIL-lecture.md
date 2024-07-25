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

### 2) 내장 함수 `super()` ----- 여기부터 수정
---

> `클래스 Class` (= 데이터 타입​)

- 파이썬에서 `타입`을 표현하는 방법

- 객체를 생성하기 위한 설계도

- 데이터와 기능을 함께 묶는 방법을 제공


<br>
<br>


### 3) `에러`와 `예외`
---
클래스를 정의하기 위해서는 가장 먼저 `class` 키워드를 사용한다. 또한 다른 함수 정의와 구분하기 위해 `Pascal Case` 방식으로 클래스명을 작성한다.

``` python
'Pascal Case 방식': 대문자로 시작하며, snake_case의 underscore 대신 다시 대문자를 사용 (= Upper Camel Case)
```

<br>

> 클래스 정의

<br>
<br>

### 4) 예외 처리: `try` - `except`
---

### ✔ 인스턴스 메서드 `Instance Methods`
---

- 핵심 요약

> Most Common

> Must have self parameter