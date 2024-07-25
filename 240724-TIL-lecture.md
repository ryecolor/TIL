# 240724 - Python 07: OOP 1
> ## Index
> 
> 1) 객체 지향 프로그래밍 `OOP`
> 2) `클래스`와 `객체`, `인스턴스`
> 3) 클래스 `정의` 및 `구조`
> 4) 파이썬 메서드 : `클래스 메서드` `인스턴스 메서드` `스태틱 메서드`
> 5) 보조 메서드 : `매직 메서드` `데코레이터`
> ---

<br>

### 1) 객체 지향 프로그래밍 `OOP`
---
프로그래밍 패러다임은 `절차 지향` 방식에서 `객체 지향` 방식으로 변화하였다. 각각의 방식의 특징과 차이에 대해 알아보자.

<br>

> ① 절차 지향 프로그래밍 `Procedural Programming, PP`

- 프로그램을 `데이터`와 `절차`로 구성하는 방식의 프로그래밍 패러다임

- 코드의 순차적인 흐름과 함수 호출에 의해 프로그램이 진행

- `데이터`와 해당 데이터를 처리하는 `함수(절차)`가 분리되어 있으며, `함수 호출의 흐름`이 중요

- '실제로 `실행되는 내용`이 무엇인가'가 중요

- 데이터를 다시 재사용하기보다 처음부터 끝까지 `실행되는 결과물`이 중요한 방식

<br>

---

<br>

> ② 객체 지향 프로그래밍 `Object Oriented Programming, OPP`

- 등장 배경: `소프트웨어 위기 (Software Crisis)`

  - `하드웨어의 발전`으로 컴퓨터 계산 용량과 문제의 복잡성이 급격히 증가함에 따라 소프트웨어에 발생한 충격

- `데이터`와 해당 데이터를 조작하는 `메서드`를 `​하나의 객체`​로 묶어 관리하는 방식

- 함수보다 `데이터`가 중요해진 프로그래밍 패러다임

<br>

---

<br>

> ③ 절차 지향 vs. 객체 지향

| 절차 지향 (PP) | 객체 지향 (OPP) |
| :-----: | :---: |
| `데이터`와 해당 데이터를 처리하는 `함수(절차)`가 `분리`되어 있는 형태의 프로그래밍 패러다임 | `데이터`와 해당 데이터를 처리하는 `메서드(메시지)`를 `하나의 객체(클래스)`로 묶음 |
| 함수 호출의 흐름이 중요 | 객체 간 상호작용과 메시지 전달이 중요 |


<br>
<br>

### 2) `클래스`와 `객체`, `인스턴스`
---

> `클래스 Class` (= 데이터 타입​)

- 파이썬에서 `타입`을 표현하는 방법

- 객체를 생성하기 위한 설계도

- 데이터와 기능을 함께 묶는 방법을 제공

<br>

> `객체 Object`

- 클래스에서 정의한 것을 토대로 `메모리에 할당된 것`

- `속성(변수)`과 `행동​(메서드)`으로 구성된 모든 것

- `객체 (Object)` = `속성(Attribute)` + `기능(Method)`

  - `타입(type)` : 어떤 연산자(*operator*)와 조작(*method*)이 가능한가?

  - `속성(attribute)` : 어떤 상태(데이터)를 가지는가?

  - `조작법(method)` : 어떤 행위(함수)를 할 수 있는가?

<br>

> `인스턴스 Instance`

- 클래스의 속성과 행동을 기반으로 생성된 개별 객체

- 가수 (클래스) → 아이유, BTS, ... (객체)

  ``` python
  IU는 '객체'다. (O)
  IU는 '인스턴스'다. (X)
  IU는 '가수의 인스턴스'다. (O, 관계적 명시 중요)
  ```

<br>

### "하나의 `객체(Object)`는 특정 타입의 `인스턴스(instance)`이다."

<br>
<br>


### 3) 클래스 `정의` 및 `구조`
---
클래스를 정의하기 위해서는 가장 먼저 `class` 키워드를 사용한다. 또한 다른 함수 정의와 구분하기 위해 `Pascal Case` 방식으로 클래스명을 작성한다.

``` python
'Pascal Case 방식': 대문자로 시작하며, snake_case의 underscore 대신 다시 대문자를 사용 (= Upper Camel Case)
```

<br>

> 클래스 정의

``` python
# class 클래스명
class MyClass:
  number_of_people = 0 # 클래스 변수 (= 클래스 속성)
  class_name = '2반'

  # 클래스 내 모든 함수는 인스턴스 메서드

  # 생성자(클래스) 메서드
  def __init__(self, name): # self = 인스턴스
    #초기 값 필요
    self.name = name # 인스턴스.인스턴스 변수명 = 함수의 매개변수명
    MyClass.number_of_people += 1 # 함수 내에서 클래스 변수 사용 시 클래스명.클래스 변수

  def hello(self): # 인스턴스 메서드
    return f'{self.name}이 입실하였습니다.'
```

<br>

> 인스턴스 생성 및 활용

``` python
# 인스턴스 생성

  # 생성자 메서드에서 인스턴스 self만 요구할 경우
  yejin = MyClass()

  # 생성자 메서드에서 별도의 초기 값 요구할 경우 (Ex. self, age)
  yejin = MyClass(25)


# 메서드 호출

  # 호출 형식
  yejin.메서드()

  # 호출 예시
  print(yejin.hello()) # yejin이 입실하였습니다.


# 속성(변수) 접근
yejin.attribute
  
  # 속성 확인
  print(yejin.class_name) # '2반'

  # 인스턴스 속성(변수)
  print(yejin.age) # 25 # yejin만 가지는 인스턴스 변수
```

<br>
<br>

> 클래스 구성 요소

- 클래스 구조

  - `생성자 메서드`
    - 객체를 생성할 때 자동으로 호출되는 특별한 메서드 (매직 메서드의 한 종류)
    - `__init__`이라는 이름의 메서드로 정의되며, 객체의 초기화를 담당
    - 생성자 함수를 통해 인스턴스를 생성하고 필요한 초기 값을 설정

  - `인스턴스 변수`
    - 인스턴스(객체)마다 별도로 유지되는 변수
    - 인스턴스마다 독립적인 값을 가지며, 인스턴스가 생성될 때마다 초기화됨

  - `클래스 변수` (= 클래스 속성)
    - 클래스 내부에 선언된 변수 (메서드에 속해 있지 않음)
    - 클래스로 생성된 모든 인스턴스들이 공유하는 변수

  - `인스턴스 메서드`
    - 각각의 인스턴스에서 호출할 수 있는 메서드
    - 인스턴스 변수에 접근하고 수정하는 등의 작업을 수행

<br>

> 인스턴스 변수와 클래스 변수

- 클래스 변수 활용

  - 인스턴스가 생성될 때마다 클래스 변수가 늘어나도록 설정 가능

  - `class.class_variable`로 클래스 변수 참조 가능

  - 인스턴스 변수 `class.class_variable`를 따로 정의할 경우, 클래스 변수에 영향을 미치지는 못함

<br>
<br>

### 4) 파이썬 메서드 : `인스턴스 메서드` `클래스 메서드` `스태틱 메서드`
---

### ✔ 인스턴스 메서드 `Instance Methods`
---

- 핵심 요약

> Most Common

> Must have self parameter

> No decorator needed

> Can be accessed through object (instance of Class)

---

<br>

- 클래스로부터 생성된 각 인스턴스에서 호출할 수 있는 메서드

- 인스턴스의 상태를 조작하거나 동작을 수행

- 구조

  - 반드시 첫 번째 매개변수로 `인스턴스 자신(self)`을 전달받음
  
  - self는 매개변수 이름일 뿐이며 다른 이름으로 설정 가능하나, 그대로 사용할 것을 강력히 권장

  ``` python
  class MyClass:
    # (def __init__ 생략)
    def instance_method(self, arg1, ...):
      # self = 인스턴스 메서드를 호출할 인스턴스 자신
      pass
  ```

<br>

- `self` 동작 원리

  - `'hello'.upper()` == `str.upper('hello')`

  ``` python
   upper 메서드를 사용해 문자열 'hello'를 대문자로 변경하는 'hello'.upper()는 str.upper('hello')를 객체 지향 방식의 메서드로 단축하여 호출하는 표현이다.

   실제 파이썬 내부 동작의 진행 방식을 살펴보면 str 클래스가 upper 메서드를 호출하여 첫 번째 인자로 문자열 인스턴스를 입력한 것과 같다. 문자열 객체가 단순히 어딘가의 함수로 들어가는 인자로 활용되는 내부 방식보다, 앞선 단축형 호출은 '객체 스스로 메서드를 호출하여 코드를 동작시키는 객체 지향적인 표현'이다.
  ```

<br>

- 생성자 메서드 `Constructor Methods`

  - 인스턴스 메서드 중 하나

  - 인스턴스 객체가 생성될 때 자동으로 호출되는 메서드

  - 인스턴스 변수들의 초기 값을 설정

  ``` python
  class Person:
    def __init__(self, name): # 생성자 메서드
        self.name = name
        print('인스턴스가 생성되었습니다.')

    def greeting(self):
        print(f'안녕하세요. {self.name}입니다.')

  person1 = Person('지민') # 인스턴스가 생성되었습니다.
  person1.greeting() # 안녕하세요. 지민입니다.
  ```

<br>
<br>

### ✔ 클래스 메서드 `Class Methods`
---

- 핵심 요약

> Doesn't need self parameter

> Need cls as parameter

> Need decorator @classmethod

> Can be accessed directly through the class. Don't need instance of class.

---

<br>

- 클래스가 호출하는 메서드

- 클래스 변수를 조작하거나 클래스 레벨의 동작을 수행

- 구조

  - `@classmethod` 데코레이터를 사용하여 정의

  - 호출 시, 첫 번째 인자로 `해당 메서드를 호출하는 클래스(cls)`​가 전달됨

  - cls는 매개변수 이름일 뿐이며 다른 이름으로 설정 가능하나, 그대로 사용할 것을 강력히 권장

  ``` python
  class Person:
    count = 0

    def __init__(self, name):
        self.name = name
        Person.count += 1

    @classmethod # 메서드 정의
    def number_of_population(cls):
        print(f'인구 수는 {cls.count}입니다.')

  person1 = Person('iu')
  person2 = Person('BTS')

  # 인구 수는 2입니다. # 메서드 실행 결과
  Person.number_of_population() # 메서드 실행
  ```

<br>
<br>

### ✔ 스태틱(정적) 메서드 `Static Methods`
---

- 핵심 요약

> Doesn't need self parameter

> Doesn't need self or cls as parameter

> Need decorator @staticmethod

> Can only access variables passed as argument.

> Static method cannot be accessed through class or it's instance.

---

<br>

- 클래스와 인스턴스와 상관없이 `독립적으로 동작`하는 메서드

- 주로 클래스와 관련이 있지만 인스턴스와 `상호작용이 필요하지 않은 경우`에 사용

- 구조

  - `@staticmethod` 데코레이터를 사용하여 정의

  - 호출 시 필수적으로 작성해야 할 매개변수가 없음

  - 즉, 객체 상태나 클래스 상태를 수정할 수 없으며 `단지 기능(행동)만을 위해 사용`

    - 단순히 문자열을 조작하는 기능을 제공하는 메서드 예시

    ``` python
    class StringUtils:
    @staticmethod
    def reverse_string(string):
        return string[::-1]

    @staticmethod
    def capitalize_string(string):
        return string.capitalize()

    text = 'hello, world'

    reversed_text = StringUtils.reverse_string(text)
    print(reversed_text) # dlrow ,olleh

    capitalized_text = StringUtils.capitalize_string(text)
    print(capitalized_text) # Hello, world
    ```

<br>
<br>

### ✔ 메서드 정리
---

> 인스턴스 메서드
- 인스턴스의 상태를 변경하거나, 해당 인스턴스의 특정 동작을 수행

> 클래스 메서드
- 인스턴스의 상태에 의존하지 않는 기능을 정의
- 클래스 변수를 조작하거나 클래스 레벨의 동작을 수행

> 스태틱 메서드
- 클래스 및 인스턴스와 관련이 없는 일반적인 기능을 수행

<br>

> 누가 어떤 메서드를 사용해야 할까?
- 클래스
  - 클래스 메서드
  - 스태틱 메서드

- 인스턴스
  - 인스턴스 메서드

``` python
클래스와 인스턴스 둘 다 '모든 메서드를 호출 가능'하다. 그러나 각자의 메서드는 OOP 패러다임에 따라 명확한 목적에 따라 설계된 것이기 때문에 클래스와 인스턴스 각각 올바른 메서드만 사용해야 한다.'할 수 있다 != 써도 된다'임을 기억하자.
```

<br>
<br>

### 5) 보조 메서드 : `매직 메서드` `데코레이터`
---

> 인스턴스와 클래스 간 `이름공간`

- 클래스를 정의하면, 클래스와 해당하는 이름공간 생성

- 인스턴스를 만들면, 인스턴스 객체가 생성되고 `독립적인 이름공간` 생성

- 인스턴스에서 특정 속성에 접근하면, `인스턴스 → 클래스` 순으로 탐색

---

![image](https://postfiles.pstatic.net/MjAyNDA3MjNfMjM5/MDAxNzIxNzM1OTE3MzA0.b-jA3rqpVVax106tel-mTAK16AokjU5UFlc-jxyn5rAg.uqjgS2nOm6atL7omfNsZCg4thclfUyF54f7iBwodC_cg.PNG/image.png?type=w773)

---

``` python
class Person:
    name = 'unknown'

    def talk(self):
        print(self.name)

p1 = Person()
p1.talk() # unknown
# 인스턴스 변수가 정의되어 있지 않아 클래스 변수 unknown이 출력됨

# p2 인스턴스 변수 설정 전/후
p2 = Person()
p2.talk() # unknown
p2.name = 'Kim'
p2.talk() # Kim
# 인스턴스 변수가 정의되어 인스턴스 변수 Kim이 출력됨

print(Person.name) # unknown
print(p1.name) # unknown
print(p2.name) # Kim
# 클래스 변수 name 값이 Kim으로 변경된 것이 아님
# p2 인스턴스의 인스턴스 변수 name이 Kim으로 저장됨
```

<br>

> 독립적인 이름공간을 가지는 `이점`

- 각 인스턴스는 독립적인 메모리 공간을 가지며, 클래스와 다른 인스턴스 간에는 서로의 데이터나 상태에 `직접적인 접근이 불가능`

- 객체 지향 프로그래밍의 중요한 특성 중 하나로, 클래스와 인스턴스를 모듈화하고 각각의 객체가 독립적으로 동작하도록 보장

- 이를 통해 클래스와 인스턴스는 다른 객체들과의 상호작용에서 서로 충돌이나 영향을 주지 않으면서 독립적으로 동작할 수 있음

- 코드의 가독성, 유지 보수성, 재사용성을 높이는 것에 도움을 줌

<br>

<br>

### ✔ 매직 메서드 `Magic Methods`
---

- 인스턴스 메서드 중 하나로, 특정 상황에 `자동으로 호출`되는 메서드

- `Double underscore(__)`가 있는 메서드는 특수한 동작을 위해 만들어진 메서드

- 스페셜 메서드 혹은 매직 메서드라고 불림

- 종류

  - __str__(self)
  - __len__(self)
  - __lt__(self, other)
  - __le__(self, other)
  - __eq__(self, other)
  - __gt__(self, other)
  - __ge__(self, other)
  - __ne__(self, other)
  - ...

<br>

### ✔ 데코레이터 `Decorator`
---

- 다른 함수의 코드를 유지한 채로 수정하거나 확장하기 위해 사용되는 함수

- `Double underscore(__)`가 있는 메서드는 특수한 동작을 위해 만들어진 메서드

- 데코레이터 정의

``` python
def my_decorator(func):
    def wrapper():
        # 함수 실행 전에 수행할 작업
        print('함수 실행 전')
        # 원본 함수 호출
        result = func()
        # 함수 실행 후에 수행할 작업
        print('함수 실행 후')
        return result
    return wrapper
```

<br>

- 데코레이터 사용

``` python
@my_decorator
def my_function():
    print('원본 함수 실행')

my_function()
```

<br>
<br>

### "`절차 지향`과 `객체 지향`은 대조되는 개념이 아니다."

``` python
객체 지향은 '기존 절차 지향을 기반'으로 두고 보완하기 위해 '객체라는 개념을 도입'해 '상속', '코드 재사용성', '유지 보수성' 등의 이점을 가지는 패러다임
```