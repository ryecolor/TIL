# 240722 - Python 05: Data Structure
> ## Index
> 
> 1) `자료 구조 Data Structure`
> 2) 시퀀스 `불변` 데이터 `문자열` 메서드
> 3) 시퀀스 `가변` 데이터 `리스트` 메서드
> 4) `할당`과 `얕은 복사`, `깊은 복사`
> 5) 문자 유형 판별 메서드 `isdecimal()` `isdigit()` `isnumeric()`
> ---

<br>

### 1) `자료 구조 Data Structure`
---
컴퓨터 공학에서는 각 데이터의 효율적인 저장, 관리를 위해 구조를 나눠 놓은 것을 `자료 구조 Data Structure`라고 일컫는다. 오늘은 데이터 타입 위주의 자료 구조 영역을 살펴 보자.

<br>

### ✔ 메서드 `method`
---

- `객체`에 속한 `함수`
    - 메서드는 `클래스(class) 내부`에 정의되는 함수
    - 객체의 상태를 조작하거나 동작을 수행
    - 각 데이터 `타입별`로 다양한 기능의 메서드 존재

- `클래스 class`
  - 파이썬에서 `타입(type)`을 표현하는 방법
  - print(help(str)) 호출 시 class str(object) 출력

<br>

``` python
# 메서드 호출 방법
# 데이터 타입 객체.메서드()

# 문자열 메서드 예시
print('hello'.capitalize()) # hello

# 리스트 메서드 예시
numbers = [1, 2, 3]
numbers.append(4)
print(numbers) # [1, 2, 3 ,4]
```

<br>
<br>

### 2) 시퀀스 `불변` 데이터 `문자열` 메서드
---
### ✔ 조회/탐색 및 검증 메서드
---
> 보통 `is`가 붙은 메서드는 무엇인가 문자열 내에 존재하는지 여부를 체크하므로, 반환 값이 `True` or `False`이다.

| 메서드 | 설명 |
| :-----: | :---: |
| s.find(x) | x의 첫 번째 위치를 반환. (없으면, `-1`을 반환) |
| s.index(x) | x의 첫 번째 위치를 반환. (없으면, `오류` 발생) |
| s.isupper() | 문자열이 모두 `대문자`인지 여부 |
| s.islower() | 문자열이 모두 `소문자`인지 여부 |
| s.isalpha() | 문자열이 모두 `알파벳 문자`인지 여부 (*유니코드상 Letter로 한국어 포함, 공백 불가) |

<br>

### ✔ 조작 메서드
---
> - 문자열은 `불변(immutable)` 객체이므로 새 문자열 반환
> - [] 내부 내용은 선택 인자
> - 메서드 `Chaining` : 메서드는 이어서 사용 가능 (단, `타입`이 동일해야 하며, 앞선 메서드의 `반환 값`이 있어야 함)

| 메서드 | 설명 |
| :-----: | :---: |
| s.replace(old, new`[, count]`) | 바꿀 대상 글자를 새로운 글자로 바꿔서 반환 (`개수 지정` 가능) |
| s.strip([chars]) | 문자열의 `시작과 끝`에 있는 공백이나 특정 문자를 제거 |
| s.split(sep=None, `maxsplit`=-1) | 공백이나 특정 문자를 기준으로 분리하여 `리스트`로 반환 (`횟수` 지정 가능) |
| 'separater'.join(iterable) | 구분자로 iterable의 문자열을 연결한 문자열을 반환 |
| s.capitalize() | 가장 첫 번째 글자를 대문자로 변경 |
| s.title() | 문자열 내 띄어쓰기 기준으로 각 단어의 첫 글자는 대문자로, 나머지는 소문자로 변환 |
| s.upper() | 모두 대문자로 변경 |
| s.lower() | 모두 소문자로 변경 |
| s.swapcase() | 대↔소문자 서로 변경 |

<br>

``` python
# find
text = 'sunset'
print(text.find('n')) # 2 # 반환과 출력은 다르므로, 반환 값을 print() 함수로 출력
print(text.find('z')) # -1 # 포함하지 않는 요소이므로 -1 반환

# index
print(text.index('n')) # 2
# print(text.index('z')) # 포함하지 않는 요소이므로 에러 발생 # ValueError: substring not found

# isupper
string1 = 'HI HOW ARE YOU'
string2 = 'Hi how are you'
print(string1.isupper()) # True
print(string2.isupper()) # False

# islower
print(string1.islower()) # False
print(string2.islower()) # False

# isalpha
string1 = 'HelloMello'
string2 = '123hello123'
print(string1.isalpha()) # True # 공백도 불가
print(string2.isalpha()) # False

# replace
text = 'Hello, world! world world'
text_01 = text.replace('world', 'python') # 지정 없을 시 개수 제한 X
print(text_01) # Hello, python! python python
text_02 = text.replace('world', 'python', 1) # 지정 있을 시 개수만큼 변경
print(text_02) # Hello, python! world world

# strip
text = '  Hello, world!  '
text_03 = text.strip()
print(text_03)

# split # 구분자로 문자열 분리하여 리스트 반환
text = 'Hello, world!'
words = text.split(',')
print(words) # ['Hello', ' world!'] # 분리 기준 제시 가능
words_2 = text.split()
print(words_2) # ['Hello,', 'world!'] # 기준 없을 시 공백으로 분리

# join # '구분자'.join(iterable) # split과 반대
words = ['Hello', 'world!']
new_text = '-'.join(words)
print(new_text) # Hello-world!


# capitalize
text = 'heLLo, woRld!'
new_text = text.capitalize()
print(new_text) # Hello, world! # 앞 글자 대문자, 나머지 소문자

# title
new_text_2 = text.title()
print(new_text_2) # Hello, World! # 공백 기준으로 단어마다 앞 글자 대문자, 나머지 소문자

# upper
new_text_3 = text.upper()
print(new_text_3) # HELLO, WORLD!

# lower
new_text_4 = text.lower()
print(new_text_4) # hello, world!

# swapcase
new_text_5 = text.swapcase()
print(new_text_5) # HEllO, WOrLD!
```


<br>
<br>


### 3) 시퀀스 `가변` 데이터 `리스트` 메서드
---

### ✔ 값 추가 및 삭제 메서드
---
| 메서드 | 설명 |
| :-----: | :---: |
| L.append(x) | 리스트 마지막에 항목 x를 추가 |
| `L.extend(m)` | iterable m의 모든 항목들을 리스트 끝에 추가 (+=과 같은 기능) |
| L.insert(i, x) | 리스트 인덱스 i에 항목 x를 삽입 |
| L.remove(x) | 리스트 가장 왼쪽에 있는 항목 첫 번째 x를 제거 (x가 없을 경우 에러 발생) |
| L.pop() | 리스트 `가장 오른쪽`에 있는 항목(마지막)을 `반환` 후 제거 |
| L.pop(i) | 리스트의 인덱스 `i`에 있는 항목을 `반환` 후 제거 |
| L.clear() | 리스트의 모든 항목 삭제 |

<br>

### ✔ 탐색 및 정렬 메서드
---
| 메서드 | 설명 |
| :-----: | :---: |
| L.index(x) | 리스트에서 첫 번째로 일치하는 항목 x의 `인덱스`를 `반환` |
| L.count(x) | 리스트에서 항목 x의 `개수`를 `반환` |
| L.reverse() | 원본 리스트의 순서를 역순으로 변경 (`정렬 X`) |
| L.sort() | 원본 리스트를 오름차순으로 `정렬` (매개변수 `reverse=True` 이용 가능) |

<br>

``` python
# 문자열과 달리 리스트는 원본 자체의 조작 가능
# 문자열 immutable, 리스트 mutable

# append
my_list = [1, 2, 3]
my_list.append(4)
print(my_list) # [1, 2, 3, 4]
print(my_list.append(4)) # None # append 함수는 리턴 값 없음


# extend
my_list = [1, 2, 3]
my_list.extend([4, 5, 6])
print(my_list) # [1, 2, 3, 4, 5, 6] # extend는 리스트를 풀어서 넣음
# my_list.extend([4], [5]) # TypeError: list.extend() takes exactly one argument (2 given)
# my_list.extend(7)
# print(my_list) # TypeError: 'int' object is not iterable
my_list.append([7, 8, 9])
print(my_list) # [1, 2, 3, 4, 5, 6, [7, 8, 9]] # append는 리스트를 그대로 넣음
# my_list.append([4], [5]) # # TypeError: list.append() takes exactly one argument (2 given)

# insert(i, x)
my_list = [1, 2, 3]
my_list.insert(1, 5)
print(my_list) # [1, 5, 2, 3]

# remove
my_list = [1, 2, 3, 2, 5, 2]
my_list.remove(2)
print(my_list) # [1, 3, 2, 5, 2] # 첫 번째 값만 지움

# pop # 반환 값이 존재
my_list = [1, 2, 3, 4, 5]
item1 = my_list.pop()
print(item1) # 5
print(my_list) # [1, 2, 3, 4]
item2 = my_list.pop(0)
print(item2) # 1
print(my_list) # [2, 3, 4]

# clear
my_list = [1, 2, 3]
my_list.clear()
print(my_list) # []

# index
my_list = [1, 2, 3]
index = my_list.index(2)
print(index) # 1 # 첫 번째로 일치하는 항목의 인덱스 반환

# count
my_list = [1, 2, 2, 3, 3, 3]
count = my_list.count(3)
print(count) # 3

# reverse
my_list = [1, 3, 2, 8, 1, 9]
my_list.reverse()
print(my_list) # [9, 1, 8, 2, 3, 1] # 원본을 뒤집은 그대로 출력
print(my_list.reverse()) # None # reverse() 함수의 반환 값은 없음

# sort
my_list = [3, 2, 100, 1]
my_list.sort()
print(my_list) # [1, 2, 3, 100]

# sort(내림차순 정렬)
my_list.sort(reverse=True) # 내장된 매개변수 reverse = False이므로 True로 변경
print(my_list) # [100, 3, 2, 1]
```

<br>
<br>

### 4) `할당`과 `얕은 복사`, `깊은 복사`
---

### ✔ 데이터 타입과 복사
---
- 파이썬에서는 데이터의 분류에 따라 복사의 방법과 결과가 달라짐
- `가변` 데이터 타입과 `불변` 데이터 타입에 따라 다르게 취급 필요

<br>

- `할당 Assignment`
  - `가변` 데이터인 경우 문제 발생
  - 할당 연산자 `=`를 통한 복사는 해당 객체에 대한 `객체 참조를 복사`
  - 동일한 객체를 참조할 경우, 객체 주소의 변경 시 결과 값이 함께 변화
  ``` python
  a = [1, 2, 3, 4] # 가변 데이터
  b = a
  b[0] = 100

  print(a) # [100, 2, 3, 4] # 영향 O
  print(b) # [100, 2, 3, 4]
  ```
  ---
<br>

- `얕은 복사 Shallow copy`
  - `불변` 데이터인 경우의 `얕은 복사`
  ``` python
  a = [1, 2, 3, 4] # 불변 데이터
  b = a
  b[0] = 100

  print(a) # [100, 2, 3, 4] # 영향 O
  print(b) # [100, 2, 3, 4]
  ``` 

<br>

  - `가변` 데이터인 경우의 `얕은 복사`
    - `슬라이싱`을 통해 새로운 리스트 생성
    - 얕은 복사 `copy()` 함수 사용
    ``` python
    a = [1, 2, 3] # 가변 데이터
    b = a[:] # 얕은 복사 1 # 슬라이싱을 통해 a와 같은 값만 복사한 새로운 리스트 생성
    c = a.copy() # 얕은 복사 2 # copy() 함수 사용

    b[0] = 100
    c[0] = 999

    print(a) # [1, 2, 3] # 영향 X
    print(b) # [100, 2, 3]
    print(c) # [999, 2, 3]
    ```
 
 <br>

 - 얕은 복사의 `한계`
   - 리스트 내 리스트와 같이 `중첩된 요소`에 여전히 영향 존재
    ``` python
    a = [1, 2, [3, 4, 5]]
    b = a[:]

    b[0] = 999
    b[2][1] = 100
    print(a) # [1, 2, [3, 100, 5]] # 중첩된 요소는 영향 O
    print(b) # [999, 2, [3, 100, 5]]
    ```
    ![image_shallow_copy](https://postfiles.pstatic.net/MjAyNDA3MjJfMTM1/MDAxNzIxNjEyODIwODM2.3wEzkVvj2OQGEd2iZDbVdQItO2i8sHoWbeglBSLMS94g.Be3x-DCTVyP52uDqFtKlk_W3PcaVcC59xJjhUGWKyvEg.PNG/image.png?type=w773)
---

<br>

  - 얕은 복사의 한계를 극복하는 `깊은 복사 Deep copy`
    - copy 모듈의 `deepcopy()` 메서드 사용
    ``` python
    import copy # copy() 메서드 X 별개의 모듈 O

    a = [1, 2, [3, 4, 5]]
    b = copy.deepcopy(a)

    b[2][1] = 100
    print(a) # [1, 2, [3, 4, 5]] # 중첩된 부분도 영향 X
    print(b) # [1, 2, [3, 100, 5]]
    ```

<br>

- `'while' statement`
    - 주어진 `조건이 참(True)인 동안` 코드를 반복해서 실행
    - 조건식이 `거짓(False)이 될 때까지` 반복
    - `사용자 입력`에 따른 반복: 특정 입력 값에 대한 종료 조건 활용
    ``` python
    while True:
        print("집에 가자!")
    ```

<br>
<br>

### 5) 문자 유형 판별 메서드 `isdecimal()` `isdigit()` `isnumeric()`
---

- `isdecimal()`
  - 문자열이 모두 숫자 문자(0~9)로만 이루어져 있어야 True
- `isdigit()`
  - isdecimal()과 비슷하지만, 유니코드 숫자도 인식 ('①'도 숫자로 인식)
- `isnumeric()`
  - isdigit()과 유사하지만, 몇 가지 추가적인 유니코드 문자들을 인식
  - 분수, 지수, 루트 기호도 숫자로 인식

<br>

![img_method](https://postfiles.pstatic.net/MjAyNDA3MjJfMjMy/MDAxNzIxNjEzMzU5Njc3.9PWuEgvCZTHmtI0CyKZC5lr_2ZdwFWKYXSmVkpAQyd4g.e60z5_cU3ggucgTuUskNdcNKqMH0LpJvvhPtiL9LI3Mg.PNG/image.png?type=w773)

``` python
# isdecimal() : 가장 엄격한 기준을 적용, 오직 일반적인 십진수 숫자(0-9)만 True로 인식
print("isdecimal() 메서드 예시:")
print("'12345'.isdecimal():", '12345'.isdecimal())
print("'123.45'.isdecimal():", '123.45'.isdecimal())
print("'-123'.isdecimal():", '-123'.isdecimal())
print("'Ⅳ'.isdecimal():", 'Ⅳ'.isdecimal())
print("'½'.isdecimal():", '½'.isdecimal())
print("'²'.isdecimal():", '²'.isdecimal())
print()

# isdigit() : 일반 숫자뿐만 아니라 지수 표현(²)도 True로 인식
print("isdigit() 메서드 예시:")
print("'12345'.isdigit():", '12345'.isdigit())
print("'123.45'.isdigit():", '123.45'.isdigit())
print("'-123'.isdigit():", '-123'.isdigit())
print("'Ⅳ'.isdigit():", 'Ⅳ'.isdigit())
print("'½'.isdigit():", '½'.isdigit())
print("'²'.isdigit():", '²'.isdigit())
print()

# isnumeric() : 일반 숫자, 로마 숫자, 분수, 지수 등 다양한 형태의 숫자 표현을 True로 인식
print("isnumeric() 메서드 예시:")
print("'12345'.isnumeric():", '12345'.isnumeric())
print("'123.45'.isnumeric():", '123.45'.isnumeric())
print("'-123'.isnumeric():", '-123'.isnumeric())
print("'Ⅳ'.isnumeric():", 'Ⅳ'.isnumeric())
print("'½'.isnumeric():", '½'.isnumeric())
print("'²'.isnumeric():", '²'.isnumeric())
```