# 1. Binary Search Algorithm

## 1) 이진 검색 알고리즘
- 정렬 된 데이터 배열에서 특정 데이터를 검색하는 방법으로, 절반씩 나누어 검색하는 방식이다.
- 순차 검색 알고리즘은 주어진 데이터 배열의 처음에서 끝까지 차례로 비교하며 검색하는 방식으로 간단하다. 그러나 데이터가 많아질 경우 성능이 떨어지는 단점이 있다.
- 이진 검색 알고리즘은 순차 검색 알고리즘만큼 간단하면서 성능이 더 좋다는 장점이 있다.

## 2) 실행 방식 
- 정렬 알고리즘으로 데이터의 배열을 정렬한다.
- 정렬 된 데이터 배열의 가운데에 해당하는 인덱스를 설정한다.
- 가운데 인덱스의 값과 검색할 데이터 값을 비교한 후, 검색할 데이터 값이 작으면 검색할 부분을 가운데 인덱스를 기준으로 왼쪽 부분으로 바꾼다.
- 검색할 데이터의 값이 가운데 인덱스 값보다 크면, 검색할 부분으로 가운데 인덱스를 기준으로 오른쪽 부분으로 바꾼다.
- 이러한 방식을 반복하면서 검색할 데이터의 값이 위치하는 인덱스가 나올 때까지 실행한다.

## 3) Binary Search Algorithm code

- 정렬 알고리즘으로 데이터 배열을 정렬 해준다. 
- 퀵 정렬 알고리즘 
```
global counter

### 정렬 알고리즘으로 데이터 배열을 정렬한다.

def swap(x, i, j) :
    x[i], x[j] = x[j], x[i]

def pivotFirst(alist, lmark, rmark) :
    pivot_val = alist[lmark]
    pivot_idx = lmark

    while lmark <= rmark :
        while lmark <= rmark and alist[lmark] <= pivot_val :
            lmark += 1
        while lmark <= rmark and alist[rmark] >= pivot_val :
            rmark -= 1
        if lmark <= rmark :
            swap(alist, lmark, rmark)
            lmark += 1
            rmark -= 1
    swap(alist, pivot_idx, rmark)
    return rmark

def quicksort(alist, pivotmethod=pivotFirst) :
    def _qsort(alist, first, last) :
        if first < last :
            splitpoint = pivotmethod(alist, first, last)
            _qsort(alist, first, splitpoint-1)
            _qsort(alist, splitpoint+1, last)

    _qsort(alist, 0, len(alist)-1)
```

- 정렬 된 배열에서 특정 데이터 값을 검색한다.
```

def binary_search(search_list, search_data) :
    global counter

    ### first 와 last 변수를 설정하고, 이 사이의 구간에서 특정 데이터를 찾는다.
    first = 0
    last = len(search_list) - 1

    ### first 가 last 보다 작거나 같다는 조건을 설정한다. first 는 증가하고 last 는 감소하므로 두 변수의 크기가 역전되면 while 문을 통과하지 못한다.
    while first <= last :
        idx = (first + last) // 2   ### idx 는 first 와 last 범위의 가운데로 설정.
        counter += 1

        ### idx 는 first 와 last 의 가운데이며, idx 를 검색할 데이터와 반복 비교하면서 first 와 last 의 위치가 바뀌면서 idx 도 바뀌게 된다.
        if search_list[idx] == search_data :
            print("{item} found at position {i}".format(item=search_data, i=idx))
            return True
        ### 처음 idx 는 전체 배열의 가운데이며, 이 idx 의 값이 검색 값과 다르면 elif 의 조건을 순차적으로 통과하며, first 는 1씩 증가하고, last 는 1씩 감소한다.
        elif search_list[idx] > search_data :
            last = idx - 1
        elif search_list[idx] < search_data :
            first = idx + 1
        else :
            print("{item} not found in the list".format(item=search_data))
            return False
```

- 코드 실행
- 랜덤 리스트 생성 후 퀵 알고리즘으로 정렬
```
from random import randint

if __name__ == "__main__" :
    data = []
    counter = 0
    input_num = input("전체 데이터의 수 : ")
    data = [randint(1, 100) for x in range(int(input_num))]

print("<정렬 후>")
quicksort(data)
print(data)

=====<print>====

전체 데이터의 수 : 50
<정렬 후>
[1, 3, 4, 4, 5, 6, 9, 10, 16, 17, 17, 23, 25, 26, 26, 27, 28, 29, 31, 33, 37, 38, 38, 41, 42, 44, 45, 51, 52, 55, 59, 60, 60, 61, 63, 65, 67, 71, 72, 74, 74, 76, 77, 80, 84, 90, 90, 94, 96, 99]
```

- 정렬 한 데이터를 이진 검색 알고리즘을 사용하여 59 라는 임의의 수를 검색
- 데이터 배열에서 59 값의 위치값을 반환하도록 한다.
```
msg = binary_search(data, 59)
if msg == True :
    print("총 {} 번의 비교만으로 {} 을 검색하였습니다.".format(counter, 59))
print(msg)

=====<print>====

59 found at position 30
총 3 번의 비교만으로 59 을 검색하였습니다.
True
```
### 4) Binary Search Algorithm 2
- 재귀적 방법을 사용한 이진 검색 알고리즘
- 기준 인덱스를 정하는 방식만 재귀적으로 바뀌고 다른 방식은 위의 코드와 동일하다.

```
def binary_search_recursive(search_list, search_data) :
    global counter
    first = 0
    last = len(search_list) - 1

    if len(search_list) == 0 :
        print("{item} not found in the list".format(item=search_data))
    else :
        idx = (first + last) // 2
        counter += 1
        if search_data == search_list[idx] :
            print("{item} found at position {i}".format(item=search_data, i=idx))
            return True
        ### 이 부분에서 재귀 호출을 실행하여, 검색할 데이터 값과 동일한 값의 인덱스가 나올 때까지 리스트의 범위를 좁혀 나간다.
	else :
            if search_list[idx] < search_data :
                return binary_search_recursive(search_list[idx+1:], search_data)
            else :
                return binary_search_recursive(search_list[:idx], search_data)
```
