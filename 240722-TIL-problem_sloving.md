### ✔ 예습 시 작성 코드
---
``` python
word = 'Hello python'

word_up = word.upper() # 전부 대문자로
word_low = word.lower() # 전부 소문자로
word_title = word.title() # 각 단어 첫 글자만 대문자, 나머지는 소문자로
word_cap = word.capitalize() # 전체 중 맨 첫 글자만 대문자, 나머지는 소문자로

print(word) # Hello python # 원래 문자는 영향 X
print(word_up) # HELLO PYTHON
print(word_low) # hello python
print(word_title) # Hello Python
print(word_cap) # Hello python


# word.replace(old, new[, count]) # []는 선택 인자
word_re1 = word.replace('o', 'O', 2) # count 입력받은 개수만큼 변경
word_re2 = word.replace('o', 'O', 1)
print(word_re1) # HellO pythOn
print(word_re2) # HellO python


# word.strip([chars])
hey = 'heyHow old are you?hey'
heyhey = hey.strip('hey') # 공백 혹은 지정한 문자 제거
print(heyhey) # How old are you?



my_list = ['l', 'i', 'k', 'e', 'y', 'o', 'u']

# my_list.extend(iterable)
your_list = ['I']
our_list = your_list.extend(my_list)
print(your_list) # ['I', 'l', 'i', 'k', 'e', 'y', 'o', 'u']
print(our_list) # None # list는 mutable 객체이므로 자체가 바뀜


# your_list.insert(i, x)
your_list.insert(1, '\'m gonna')
print(your_list) # ['I', "'m gonna", 'l', 'i', 'k', 'e', 'y', 'o', 'u']


# your_list.pop(i)
item1 = your_list.pop() # pop되는 요소 반환 # 입력 없을 시 마지막 항목 제거
print(your_list) # pop된 결과 고유 반영
item2 = your_list.pop(-2) # 인덱스 지정 항목 제거
print(your_list)
# item3 = your_list.pop(:1) # 범위 지정은 불가 # SyntaxError: invalid syntax


# your_list.clear()
your_list.clear()
print(your_list) # []


# my_list.index(x)
index = my_list.index('l')
print(index) # 0 # 저장 필요

# my_list.count(x)
list_count = my_list.count('l')
print(list_count) # 1 # 저장 필요

# my_list.reverse() # 정렬 X
my_list.reverse()
print(my_list) # ['u', 'o', 'y', 'e', 'k', 'i', 'l']

# my_list.sort # 정렬 O
my_list.sort()
print(my_list) # ['e', 'i', 'k', 'l', 'o', 'u', 'y']
```

<br>
<br>

### ✔ 실습 시 `새로 배운 점`
---
#### `reversed()`
- 파이썬 내장 함수 reversed()
- `list`와 `tuple`, `string`과 같은 시퀀스 타입에 사용 가능
- 객체의 값으로 `값`을 반환 `list() 필요`
- 반환된 값은 다른 메서드로도 표현 가능
---

``` python
my_list = ['내', '힘', '들', '다']
print(list(reversed(my_list)))
# ['다', '들', '힘', '내']
print(reversed(my_list))
# <list_reverseiterator object at 0x0000020F278BBFD0>

def reverse_string(word):
    reversed_word = reversed(word)
    list = []
    for reverse in reversed_word:
        list.append(reverse)
    result = ''.join(list)
    return result

result = reverse_string("Hello, World!")
print(result)  # !dlroW ,olleH
```