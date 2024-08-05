# APS(Algorithm Problem Solving)
### Array 2.

<br>

### 2차원 배열의 선언

- 1차원 리스트를 묶어 놓은 리스트

- 2차원 이상의 다차원 리스트는 차원에 따라 index를 선언

- 2차원 리스트의 선언

    - 세로 길이(행의 개수), 가로 길이(열의 개수) 필요

- Python에서는 데이터 초기화를 통해 변수 선언과 초기화 가능

``` python
arr = [[0, 1, 2, 3] , [4, 5, 6, 7]]  # 2행 4열의 2차원 리스트
```
``` python
# 생성 예시
N = int(input)
arr = [list(map(int, input().split())) for _ in range(N)]
# 리스트를 반복하여 다시 리스트화
# 3
# 1 2 3
# 4 5 6
# 7 8 9

N = int(input())
arr = [list(map(int, input())) for _ in range(N)]
# 붙어서 들어오는 경우
# 3
# 123
# 456
# 789
```

<br>

- `배열 순회`

    - n × m 배열의 n * m 개의 모든 원소를 빠짐없이 조사하는 방법

<br>

- `행 우선 순회` (이동 방향 →)

    ``` python
    # i 행의 좌표
    # j 열의 좌표
    for i in range(n): # 행
        for j in range(m): # 열
            f(array[i][j]) # 필요한 연산 수행
    ```

<br>

- `열 우선 순회` (이동 방향 ↓)

    ``` python
    # i 행의 좌표
    # j 열의 좌표
    for j in range(n): # 열
        for i in range(m): # 행
            f(array[i][j]) # 필요한 연산 수행
    ```

<br>

- `지그재그 순회`

    ``` python
    # i 행의 좌표
    # j 열의 좌표
    for i in range(n): # 행
        for j in range(m): # 열
            f(array[i][j + (m-1-2*j)*(i%2)]) # 필요한 연산 수행
            # i%2는 1 or 0
            # 1일 경우 i 다음 인덱스의 값은 m-1-j가 됨

    # i가 증가할 때 j가 감소하도록 하려면
    # i + j 값이 같도록 유지 (j와 m-1-j)
    ```
    ``` python
    # 수도 코드로 이해하기
    for i ...
        if i % 2 == 0:
            for j: 0 -> m-1
        else:
            for j: m-1 -> 0
    ```

<br>

> `델타`를 이용한 2차 배열 탐색

- 2차 배열의 한 좌표에서 `4방향의 인접 배열 요소`를 탐색하는 방법

- 인덱스 (i, j)인 칸의 상하좌우 칸 `(ni, nj)`

- 일반적으로 시계 방향 순 0, 1, 2, 3

``` python
di[] ← [0, 1, 0, -1]  #방향별로 더할 값
dj[] ← [1, 0, -1, 0]

for k: 0 -> 3
    ni <- i + di[k]
    nj <- j + dj[k]
```

|  |  | j |  |
| :---: | :---: | :-----: | :---: |
|  | (i-1, j-1) | (i-1, j+0) | (i-1, j+1) |
| **i** | (i+0, j-1) | (i+0, j+0) | (i+0, j+1) |
|  | (i+1, j-1) | (i+1, j+0) | (i+1, j+1) |

<br>

- 델타를 이용한 2차 배열 탐색

    - 2차 배열의 한 좌표에서 4방향의 인접 배열 요소를 탐색하는 방법

    ``` python
    arr[0...N-1][0...N-1] # N X N 배열
    di[] ← [0, 1, 0, -1]
    dj[] ← [1, 0, -1, 0]
    for i : 0 -> N-1
        for j : 0 -> N-1 :
            for k in range(4):
                ni ← i + di[k]
                nj ← j + dj[k]
                if 0 <= ni < N and 0 <= nj < N # 유효한 인덱스면
                    f(arr[ni][nj])
    ```

<br>
<br>

### 2차원 배열의 활용

> 전치 행렬

- `대각선을 기준`으로 반대편과 값을 바꾸는 행렬

- `i, j의 크기`에 따라 접근하는 원소 비교 (N X N 행렬)

    - `i < j`

        | 0 | 1 | 2 | j |
        | :---: | :---: | :---: | :---: |
        | **1** |  | O | O |
        | **2** |  |  | O |
        | **i** |  |  |  |

    - `i == j`

        | 0 | 1 | 2 | j |
        | :---: | :---: | :---: | :---: |
        | **1** | O |  |  |
        | **2** |  | O |  |
        | **i** |  |  | O |

    - `i > j`

        | 0 | 1 | 2 | j |
        | :---: | :---: | :---: | :---: |
        | **1** |  |  |  |
        | **2** | O |  |  |
        | **i** | O | O |  |

    - `2-i == j` (이때의 2 = N)

        | 0 | 1 | 2 | j |
        | :---: | :---: | :---: | :---: |
        | **1** |  |  | O |
        | **2** |  | O |  |
        | **i** | O |  |  |

<br>

``` python
# i : 행의 좌표, len(arr)
# j : 열의 좌표, len(arr[0])
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]] # 3*3 행렬

for i in range(3):
    for j in range(3):
        if i < j: # 두 번 바뀌지 않도록 조건 부여
            arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```
``` python
# N X N인 경우
for i in range(N):
    for j in range(N):
        if ...
```

<br>
<br>

> 부분집합의 합(Subset Sum) 문제

- 부분집합의 수

    - 집합의 원소가 n개일 때 `공집합 포함 2**n개`

- 유한 개의 정수로 이루어진 집합의 부분집합 중에서 그 집합의 원소 총 합이 0이 되는 경우가 있는지 알아내는 문제

    - Ex. 집합 [-7, -3, -2, 5, 8]에서 [-3, -2, 5]는 이 집합의 부분집합이면서 (-3)+(-2)+5 = 0이므로 참

- 각 원소가 부분집합에 포함되었는지를 loop 이용하여 확인하고 부분집합을 생성하는 방법

``` python
bit = [0, 0, 0, 0]
for i in range(2):
    bit[0] = i  # 0번 원소
    for j in range(2):
        bit[1] = j  # 1번 원소
        for k in range(2):
            bit[2] = k  # 2번 원소
            for l in range(2):
                bit[3] = l  # 3번 원소
                print_subset(bit)  # 생성된 부분집합 출력
```

<br>

> 비트 연산자

- `&` : 비트 단위로 AND 연산

    - `i & (1 << j)` : i의 j번째 비트가 1인지 아닌지 검사

- `|` : 비트 단위로 OR 연산

- `<<` : 피연산자의 비트 열을 왼쪽으로 이동

    - `1 << n` : 2n 즉, 원소가 n개일 경우의 모든 부분집합의 수 의미

- `>>` : 피연산자의 비트 열을 오른쪽으로 이동

<br>

> 보다 간결한 부분집합 생성법 (Python 코드 예시)

``` python
arr = [3, 6, 7, 1, 5, 4]

n = len(arr)  # n : 원소의 개수

for i in range(1<<n):  # 1<<n : 부분집합의 개수
    for j in range(n):  # 원소의 수만큼 비트를 비교
        if i & (1<<j):  # i의 j번 비트가 1인 경우
            print(arr[j], end=", ")  # j번 원소 출력
    print()
print()
```

<br>

> 연습 문제 1-1

- 부분집합의 합 문제 구현하기

    - 10개의 정수를 입력받아 부분집합의 합이 0이 되는 것이 존재하는지 계산하는 함수를 작성해 보자.

    - 입력
        ```
        -7, -5, 2, 3, 8, -2, 4, 6, 9
        ```

---

> 연습 문제 1-2

- 5 X 5 2차원 배열에 25개의 숫자를 저장하고, 각 요소에 대해서 인접한 요소와의 차의 절댓값의 합을 구하시오.

- 25개의 요소에 대해 모두 조사하여 총 합을 구하시오.

``` python
N = int(input())
arr = [list(map(int, input().split())) for _ in range(N)]

di = [0, 1, 0, -1]
dj = [1, 0, -1, 0]

total = 0
for i in range(N):
    for j in range(N):  # N X N 배열의 모든 원소에 대해
        s = 0           #원소의 인접한 요소와의 차의 절댓값의 합
        # i, j 원소의 4방향 원소에 대해
        for k in range(4):
            ni = i + di[k]
            nj = j + dj[k]
            if 0 <= ni < N and 0 <= nj < N:
                s += abs(arr[i][j] - arr[ni][nj])
        total += s
print(total)
```

<br>
<br>


### 검색 (Search)

- 저장되어 있는 자료 중에서 원하는 항목을 찾는 작업

- 목적하는 탐색 키를 가진 항목을 찾는 것

    - 탐색 키 `Search Key` : 자료를 구별하여 인식할 수 있는 키

- 검색의 종류

    - 순차 검색 `Sequential Search` : 순서대로 찾는 것

    - 이진 검색 `Binary Search` : 찾고자 하는 자료의 중간부터 찾는 것

    - 해쉬 `Hash` : 고유한 위치 값을 찾는 것

<br>

> 순차 검색(Sequential Search)

- 일렬로 되어 있는 자료를 순서대로 검색하는 방법

- 가장 간단하고 직관적인 검색 방법

- 배열이나 연결 리스트 등 순차 구조로 구현된 자료 구조에서 원하는 항목을 찾을 때 유용함

- 알고리즘이 단순하여 구현이 쉬우나, 검색 대상의 수가 많을수록 수행 시간이 급격히 증가하여 비효율적

- 2가지 Case

    - 정렬되어 있지 않은 경우

    - 정렬되어 있는 경우

---

- `정렬되어 있지 않은 경우`

    - 검색 과정

        - 첫 번째 원소부터 순서대로 검색 대상과 키 값이 같은 원소가 있는지 비교하며 탐색

        - 키 값이 동일한 원소를 찾으면 그 원소의 인덱스를 반환 *끝까지 검색됨 주의

        - 자료 구조의 마지막에 이를 때까지 찾지 못하면 검색 실패 (-1 반환 *인덱스 아님 주의)

        - 찾고자 하는 원소의 순서에 따라 비교 횟수가 결정됨

        - 첫 번째 원소를 찾을 때는 1번, 두 번째 원소를 찾을 때는 2번 비교, ...

        - 정렬되지 않은 자료에서 순차 검색의 평균 비교 횟수 = (1/n)*(1+2+3+...+n) = `(n+1)/2`

    - 시간 복잡도

        - `O(n)`

        ``` python
        def sequential_search(a, n, key)
            i <- 0
            # while문 종료 조건 1: i == n (배열 끝)
            # while문 종료 조건 2: a[i] == key (키 발견)
            while i < n and a[i] != key:
                i <- i+1
            if i <- n : return i
            else : return -1
        ```
        ``` python
        for i in range(n):
            if a[i] == key:
                return i
        return -1
        ```

---

- `정렬되어 있는 경우`

    - 검색 과정

        - 자료가 오름차순으로 정렬된 상태에서 검색을 실시한다고 가정

        - 자료를 순차적으로 검색하면서 키 값을 비교

        - 원소의 키 값이 검색 대상의 키 값보다 크면 찾는 원소가 없다는 것이므로 검색 종료

        - 찾고자 하는 원소의 순서에 따라 비교 회수가 결정됨

        - 정렬이 되어 있으므로, 검색 실패를 반환하는 경우 평균 비교 회수가 반으로 감소

    - 시간 복잡도
    
        - `O(n)`

        ``` python
        def sequential_search2(a, n, key)
            i <- 0
            # 단축평가 고려하여 and 양 옆 순서 주의
            # 항상 인덱스 평가 우선
            while i < n and a[i] < key:
                i <- i+1
            if i < n and a[i] == key:
                return i
            else:
                return -1
        ```
        ``` python
        for i : 0 -> n-1
            if a[i] == key:
                return i
            elif a[i] > key:
                return -1
        return -1
        ```

<br>

> 이진 검색(Binary Search)

- 자료의 가운데에 있는 항목의 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행

- 목적 키를 찾을 때까지 이진 검색을 순환적으로 반복 수행

- 검색 범위를 반으로 줄여 가면서 보다 빠르게 검색 수행

- 이진 검색을 하기 위해서는 자료가 정렬된 상태여야 함

- 구현

    - 검색 범위의 시작점과 종료점을 이용하여 검색을 반복 수행

    - 이진 검색의 경우, 자료에 삽입이나 삭제가 발생했을 때 배열의 상태를 항상 정렬 상태로 유지하는 추가 작업 필요

    ``` python
    def binarySearch(a, n, key):
        start = 0
        end = n-1
        while start <= end: # 남은 원소가 하나라도 남아 있으면
            mid <- (start + end) // 2
            if a[mid] == key: # 검색 성공
                return true # or return middle
            elif a[mid] > key:
                end = middle - 1
            else:
                start = middle + 1
        return false # 검색 실패
    ```

<br>

> 재귀 함수 이용

- 아래와 같이 재귀 함수를 이용하여 이진 검색 구현 가능

``` python
def binarySearch2(a, low, high, key):
    if low > high: # 검색 실패
        return False
    else:
        middle = (low + high) // 2
        if key == a[middle]: # 검색 성공
            return True
        elif key M < a[middle]
            return binarySearch2(a, low, middle-1, key)
        elif a[middle] < key:
            return binarySearch2(a, middle+1, high, key)

```

- 원본 데이터 배열과 별개로 배열 인덱스를 추가할 경우

    - 상대적으로 크기가 작은 인덱스 배열을 정렬하므로 속도가 빠름

- 인덱스 (index)

    - Database에서 유래한 용어로, 테이블에 대한 동작 속도를 높여 주는 자료 구조

    - Database 분야가 아닌 곳에서는 Look up table 등의 용어 사용

    - 인덱스 저장에 필요한 디스크 공간은 보통 테이블을 저장하는 것에 필요한 공간보다 작음

    - 인덱스는 테이블의 다른 세부 항목 없이 키-필드만 보유하기 때문

    - 대량의 데이터 정렬의 반복과 프로그램의 반응이 느려지는 성능 저하 문제의 해결책

    - Database 인덱스는 이진탐색 트리 구조에 해당

<br>

> 선택 정렬(Selection Sort)

- 주어진 자료들 중 가장 작은 값의 원소부터 차례대로 선택하여 위치를 교환하는 방식

- 정렬 과정 (오름차순 기준)

    - 주어진 리스트 중에서 최솟값 탐색

    - 맨 앞이 최솟값이라 가정하고, min_idx = 0으로 시작

    - 차례대로 접근하여 if a[min_idx] > a[i]: min_idx = i 작업 반복

    - 최소값을 리스트의 맨 앞에 위치한 값과 교환 → 인덱스 활용 *값과 묶어서 인덱스 저장할 필요 X

    - 맨 처음 위치를 제외한 나머지 리스트를 대상으로 위 과정 반복

    - 기준 위치가 한 칸 뒤로 밀림 *기준 위치의 범위는 (0 -> n-2)

    - 맨 앞이 최솟값이라 가정하고, min_idx = 1로 시작

    - 차례대로 접근하여 if a[min_idx] > a[i]: min_idx = i 작업 반복

    - 미정렬 원소가 하나 남은 상황에서는 마지막 원소가 가장 큰 값을 갖게 되므로 실행 종료

- 시간 복잡도

    - O(n**2)
    
    - 장점: 쉬운 코드
    
    - 단점: 높은 시간 복잡도

``` python
def selectionSort(a, n):
    for i in range(n-1):
        min_idx = i
        for j in range(i+1, n):
            if a[min_idx] > a[j]:
                min_idx = j
        a[i], a[min_idx] = a[min_idx], a[i]
```

<br>

> 선택 정렬
``` python
# arr = 정렬 대상, n = 원소 개수(크기)
def selection_sort(arr, n):
    # 주어진 구간에 대해 기준 위치 i를 정하고
    for i in range(n-1): # n-2개까지 탐색하므로 range(n-1)
        min_idx = i # 최소값 위치를 기준 위치로 가정
        for j in range(i+1, n): # 남은 원소에 대해 실제 최소값 위치 검색
            if arr[min_idx] > arr[j]:
                min_idx = j
            arr[i], arr[min_idx] = arr[min_idx], arr[i] # 구간의 최소값을 기준 위치로 이동(교환)

a = [2, 7, 5, 3, 4]
b = [4, 3, 2, 1]
selection_sort(a, len(a))
selection_sort(b, len(b))

print(a) # [2, 4, 3, 5, 7]
print(b) # [1, 2, 3, 4]
```

<br>

> 셀렉션 알고리즘(Selection Algorithm)

- 저장되어 있는 자료로부터 k번쨰로 큰 혹은 작은 원소를 찾는 방법

- 최솟값, 최댓값, 혹은 중간값을 찾는 알고리즘을 의미하기도 함
선택 과정

- 정렬 알고리즘을 이용하여 자료 정렬

- 원하는 순서에 있는 원소 가져오기

- k번째로 작은 원소를 찾는 알고리즘 (예시)

    - 1번부터 k번까지 작은 원소들을 찾아 배열의 앞으로 이동시키고, 배열의 k번째 반환

    - k가 비교적 작을 때 유용하며 O(kn)의 수행 시간을 필요로 함

``` python
def select(arr, k):
    for i in range(0, k):
        min_idx = i
        for j in range(i+1, len(arr)):
            if arr[min_idx] > arr[j]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr[k-1]
```