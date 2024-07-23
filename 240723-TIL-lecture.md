# 240723 - Python 06: Data Structure 2
> ## Index
> 
> 1) 비시퀀스 데이터 구조 ① `딕셔너리` 메서드
> 2) 비시퀀스 데이터 구조 ② `세트` 메서드
> 3) 비시퀀스 데이터 구조 ③ `세트 집합` 메서드
> 4) `Set`, `Dictionary`와 `해시 테이블`
> 5) 파이썬 문법 규격 `EBNF`
> ---

<br>

### 1) 비시퀀스 데이터 구조 ① `딕셔너리` 메서드
---
`딕셔너리 Dictionary`는 고유한 항목들_중복되지 않는 Key들_의 정렬되지 않은 컬렉션이다.
- 특징: `순서X` `반복X` `키/값(쌍)`
- 메서드
  | 메서드 | 설명 |
  | :-----: | :---: |
  | D.clear() | 딕셔너리의 모든 키/값 쌍을 제거 |
  | `D.get(key[,default])` | D[key]와 같은 기능으로 key를 통해 value 호출 (단 키가 없을 시 `None` 또는 `기본(default) 값` 반환) |
  | `D.keys()` | Key를 모은 객체 반환 |
  | `D.values()` | Value를 모은 객체 반환 |
  | `D.items()` | 키/값 쌍을 모은 객체 반환 (`Tuple` 형태이므로 `변수 2개`로 반복문 언패킹) |
  | `D.pop(key[,default])` | key를 제거하고 연결됐던 값을 반환 (단 키가 없을 시 `오류 발생` 또는 `기본(default) 값` 반환) |
  | D.setdefault(k) | Key K와 연결된 값 반환 |
  | D.setdefault(k, v) | Key k가 없을 경우 v를 값으로 하는 키 k를 추가하고 `v 반환` |
  | D.update([other]) | Key가 겹치는 경우 `other list` 혹은 입력된 `여러 인자의 값`으로 기존 값을 덮어쓰고, 기존에 없던 Key라면 새로 추가 |

<br>

``` python
# clear
person = {'name': 'Alice', 'age': 25}
person.clear()
print(person)


# get
person = {'name': 'Alice', 'age': 25}
print(person.get('name'))
print(person.get('country'))
print(person.get('country', 'Unknown'))
# print(person['country']) # KeyError: 'country'


# keys
person = {'name': 'Alice', 'age': 25}
print(person.keys()) # dict_keys(['name', 'age'])
for item in person.keys(): # 리스트 형태 # 형변환 없이 자체 반복 가능
    print(item) # key 출력
# name
# age


# values
person = {'name': 'Alice', 'age': 25}
print(person.values()) # dict_values(['Alice', 25])
for item in person.values(): # 리스트 형태 # 형변환 없이 자체 반복 가능
    print(item)
# Alice
# 25


# items
person = {'name': 'Alice', 'age': 25}
print(person.items()) # dict_items([('name', 'Alice'), ('age', 25)])
for key, value in person.items(): # 튜플 리스트 형태 # 임시 변수 2개로 언패킹
    print(key, value)
# name Alice
# age 25


# pop
person = {'name': 'Alice', 'age': 25}
print(person.pop('name')) # Alice
# print(person.pop('address')) # KeyError: 'address'
print(person.pop('address', 'Unknown')) # Unknown
print(person) # {'age': 25} # key 'Alice'가 pop되어 사라짐


# setdefault
person = {'name': 'Alice', 'age': 25}
print(person.setdefault('country', 'Korea')) # Korea # 없어도 반환
print(person) # {'name': 'Alice', 'age': 25, 'country': 'Korea'} # 자동 추가


# update
person = {'name': 'Alice', 'age': 25}
other_person = {'name': 'Jane', 'gender': 'Female'}

person.update(other_person)
print(person) # {'name': 'Jane', 'age': 25, 'gender': 'Female'}

person.update(age=100, country='Korea')
print(person) # {'name': 'Jane', 'age': 100, 'gender': 'Female', 'country': 'Korea'}

# other_person을 사용해 person을 update했다고 해도 메모리 주소 상이
# person을 이후 변화시켜도 update는 복사와 다르므로 other_person의 변화 X
```

<br>
<br>

### 2) 비시퀀스 데이터 구조 ② `세트` 메서드
---
`세트 Set` 역시 고유한 항목들의 정렬되지 않은 컬렉션이다.
- 특징: `순서X` `반복X` `중복X`
- 메서드
  | 메서드 | 설명 |
  | :-----: | :---: |
  | `s.add(x)` | 세트 s에 항목 x를 추가, 이미 x가 있다면 변화 없음 |
  | s.clear() | 세트 s의 모든 항목을 제거 |
  | `s.remove(x)` | 세트 s에서 항목 x를 제거, x가 없다면 에러 발생 |
  | s.pop() | 세트 s에서 `해시 테이블 내 임의의 항목`을 반환하고, 해당 항목을 제거 |
  | s.discard(x) | 세트 s에서 항목 x를 제거, x가 없다면 에러 없이 넘어감 |
  | s.update(iterable) | 세트 s에 다른 iterable 요소를 추가 |

<br>

``` python
# add
my_set = {'a', 'b', 'c', 1, 2, 3} # 순서 X # 임의의 위치
my_set.add(4)
print(my_set)

# 실행할 때마다 순서가 달라짐
# {1, 2, 3, 4, 'b', 'c', 'a'}
# {1, 'b', 3, 2, 4, 'c', 'a'}

# 중복이 없으므로 add하더라도 겹치는 요소 발생 X
my_set.add(4)
print(my_set) # {1, 2, 3, 'b', 'a', 4, 'c'}


# clear
my_set = {'a', 'b', 'c', 1, 2, 3}
my_set.clear()
print(my_set) # set()


# remove
my_set = {'a', 'b', 'c', 1, 2, 3}
my_set.remove(2)
print(my_set) # {1, 'a', 3, 'b', 'c'}
# my_set.remove(10)
# print(my_set) # KeyError: 10 # 없는 Key 제거 불가


# pop
my_set = {'a', 'b', 'c', 1, 2, 3}
# 순서가 없을 때 리스트는 맨 끝, 딕셔너리는 키에 따른 값을 제거
# set에서의 pop은 임의의 항목을 제거하여 반환
element = my_set.pop()
print(element) # 빠르게 반복 시 빠지는 요소가 달라짐 # 이유는? ▼ 참고의 '해시 함수' 확인

# discard
my_set = {'a', 'b', 'c', 1, 2, 3}
my_set.discard(2) 
print(my_set) # {1, 3, 'a', 'c', 'b'}
my_set.discard(10) # 없는 것을 빼도 오류 발생 X
print(my_set.discard(10)) # None


# update
my_set = {'a', 'b', 'c', 1, 2, 3}
my_set.update([1, 4, 5])
print(my_set) # {1, 2, 3, 'b', 4, 5, 'a', 'c'}
```

<br>
<br>


### 3) 비시퀀스 데이터 구조 ③ `세트 집합` 메서드
---
`세트 Set`는 중복을 허용하지 않는다는 점에서 집합 간의 수식 계산이 가능하다. 다음은 세트의 집합 메서드들이다.
- 집합 메서드
  | 메서드 | 설명 | 연산자 |
  | :-----: | :---: | :---: |
  | set1.difference(set2) | set1에는 들어있지만 set2에는 없는 항목으로 세트를 생성 후 반환 | set1 - set2 |
  | set1.intersection(set2) | set1과 set2 모두 들어있는 항목으로 세트를 생성 후 반환 | set1 & set2 |
  | set1.issubset(set2) | set1의 항목이 모두 set2에 들어있으면 True를 반환 (아닐 시 False 반환) | set1 <= set2 |
  | set1.issuperset(set2) | set1이 set2의 항목을 모두 포함하면 True를 반환 (아닐 시 False 반환) | set1 >= set2 |
  | set1.union(set2) | set1 또는 set2에(혹은 둘 다) 들어있는 항목으로 세트를 생성 후 반환 | set1 | set2 |

<br>

``` python
set1 = {0, 1, 2, 3, 4}
set2 = {1, 3, 5, 7, 9}
set3 = {0, 1}

print(set1.difference(set2)) # {0, 2, 4}
print(set1.intersection(set2)) # {1, 3}
print(set1.issubset(set2)) # False
print(set3.issubset(set1)) # True
print(set1.issuperset(set2)) # False
print(set1.union(set2)) # {0, 1, 2, 3, 4, 5, 7, 9}
```

<br>
<br>

### 4) `Set`, `Dictionary`와 `해시 테이블`
---

### ✔ 해시 테이블 `Hash Table`
---
- 해시 함수를 사용하여 변환한 값을 `색인(index)`으로 삼아 `키(key)와 데이터(value)`를 저장하는 자료 구조
- 해시 테이블 자체는 `순서`가 존재하나, 파이썬 재실행 시마다 달라지므로 `인정 X`
- 데이터를 효율적으로 저장하고 검색하기 위해 사용

<br>

> 해시 테이블 원리
- `해시 함수`를 통해 `키`를 `해시 값`으로 변환하고, 이 해시 값을 `인덱스`로 사용하여 데이터를 저장하거나 검색
- 파이썬 환경이 바뀌며 해시 함수를 재구성할 때마다 `값이 바뀜`

<br>

> 해시 (Hash)
- 임의의 크기를 가진 데이터(key)를 고정된 크기의 `고유한 값(index, 색인)`으로 변환하는 것
- 데이터를 고유하게 식별하는 일종의 `지문`과 같은 역할 수행
- 파이썬에서는 해시 함수를 사용하여 데이터를 `정수` 형태의 해시 값으로 변환

<br>

> 해시 함수 (Hash function)
- 임의의 길이의 데이터를 입력받아 고정된 길이의 `임의의 데이터(해시 값)`를 출력하는 함수
  - 주로 해시 테이블 자료 구조에 사용
  - 매우 빠른 데이터 검색을 위한 컴퓨터 소프트웨어에서 유용하게 사용

<br>

> `set의 요소` & `dictionary의 키`와 `해시 테이블`의 관계
- 파이썬에서 set의 요소와 dictionary의 키는 해시 테이블을 이용하여 중복되지 않는 고유한 값을 저장
- `세트 내의 각 요소`
  - 해시 함수를 통해 해시 값으로 변환되고, 이 해시 값을 기반으로 해시 테이블에 저장
- `딕셔너리의 키`
  - 키는 고유해야 하므로, 키를 해시 함수를 통해 해시 값으로 변환하여 해시 테이블에 저장
  - 딕셔너리의 키는 매우 빠른 탐색 속도를 제공하며, 중복된 값을 허용하지 않음

<br>

> 파이썬에서의 해시 함수
- 파이썬에서 해시 함수의 동작 방식은 `객체의 타입`에 따라 달라짐
- 정수와 문자열은 서로 다른 타입이며, 이들의 해시 값을 계산하는 방식도 다름
- `정수`
  - 같은 정수는 항상 `같은 해시 값`을 가짐
  - 해시 테이블에 정수를 저장할 떄 효율적인 방법
  - 예를 들어, hash(1)과 hash(2)는 항상 서로 다른 해시 값을 갖지만, hash(1)은 항상 동일한 해시 값을 갖게 됨
  - 따라서 파이썬을 여러 번 재실행해도 정수는 같은 해시 값과 순서를 보임
  - 그러나 set, dictionary에 정수만 존재해도 순서가 있다고 볼 수 없음

- `문자열`
  - 문자열은 `가변적`인 길이를 갖고 있음
  - 문자열에 포함된 각 문자들의 유니코드 코드 포인트 등을 기반으로 해시 값 계산
  - 이로 인해 문자열의 해시 값은 실행 시마다 다르게 계산됨

<br>

---

### 정수와 문자열의 `해시 함수 영향` 예시
---
``` python
# 정수
my_set = {3, 2, 1, 9, 100, 4, 87, 39, 10, 52}
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set.pop())
print(my_set)


# 문자열
my_str_set = {'a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j'}
print(my_str_set.pop())
print(my_str_set.pop())
print(my_str_set.pop())
print(my_str_set.pop())
print(my_str_set.pop())

print(hash(1))
print(hash(1))
print(hash('a'))
print(hash('a'))

print(hash(1))
print(hash(1.0))
print(hash('1'))
print(hash((1, 2, 3)))
```
<br>

> `set의 pop() 메서드`의 결과와 `해시 테이블`의 관계
- set의 pop()에서 임의의 요소를 제거하고 반환
- 실행할 때마다 다른 요소를 얻는다는 의미에서의 무작위가 아니라 `임의`라는 의미에서 무작위
  - By "arbitrary" the docs don't mean "random" - python 공식 문서
- 해시 테이블에 나타나는 순서대로 반환하는 것
- `해시 테이블의 순서와 자료 구조상의 순서​를 동일시하면 안 됨`

<br>

> `hashable`
- hash() 함수의 인자로 전달해서 결과를 반환받을 수 있는 객체
- **대부분의** 불변형 데이터 타입은 hashable
- 단, tuple의 경우 불변형이지만 해시 불가능한 객체를 참조할 때는 tuple 자체의 해시도 불가능

<br>

> `hashable`과 `불변성` 간의 관계
- 해시 테이블의 키는 `불변`해야 함 (객체 생성 후 값의 변경이 불가해야 함)
- 불변 객체는 해시 값이 변하지 않으므로 동일한 값에 대해 일관된 해시 값 유지 가능
- 단, hash 가능하다 `!=` 불변하다

<br>

> `가변형` 객체가 `hashable`하지 않은 이유
- 해시 테이블의 `무결성 유지 불가`
  - 값이 변경될 수 있기 때문에 동일한 객체에 대한 해시 값이 변경될 가능성 존재
- 해시 값의 `일관성 유지 불가`
  - 가변형 객체가 변경되면 해시 값이 변경되기 때문에, 같은 객체에 대한 서로 다른 해시 값이 반환될 수 있음

<br>

``` python
TypeError: unhashable type: 'list'
print(hash((1, 2, [3, 4])))
TypeError: unhashable type: 'list'
print(hash([1, 2, 3]))
TypeError: unhashable type: 'list'
my_set = {[1, 2, 3], 1, 2, 3, 4, 5}
TypeError: unhashable type: 'set'
my_dict = {{3, 2}: 'a'}

# 전체 에러 발생
```

<br>

> `hashable` 객체가 필요한 이유
1. `해시 테이블 기반 자료 구조` 사용
   - set의 요소와 dict의 key
   - 중복 값 방지
   - 빠른 검색과 조회

2. `불변성`을 통한 일관된 해시 값

3. `안전성`과 `예측 가능성` 유지

<br>
<br>

### 5) 파이썬 문법 규격 `EBNF`
---

- `BNF(Backus-Naur Form)`
  - 프로그래밍 언어의 문법을 표현하기 위한 표기법

- `EBNF(Extended Backus-Naur Form)`
  - BNF를 확장한 표기법
  - `메타 기호`를 추가하여 더 간결하고 표현력이 강해진 형태
  - 서로 다른 프로그래밍 언어, 데이터 형식, 프로토콜 등의 문법을 통일하여 정의하기 위해 사용

<br>

  | 메타 기호 | 의미 |
  | :-----: | :---: |
  | [] | 선택적 요소 |
  | {} | &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0번 이상 반복&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |
  | () | 그룹화 |

<br>
<br>

### 참고 링크
---
[More Dictionary Method - Python 3.9.19 documentation](https://docs.python.org/3/library/stdtypes.html#dict)