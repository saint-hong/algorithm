# 1. Merge Sort Algorithm

## 2) 병합 정렬 알고리즘이란?
- 존 폰 노이만이 만든 정렬 알고리즘으로, 테입 드라이브의 데이터 저장 방식을 닮았다.
- 분할 정복(divide and conquer) 알고리즘의 한 종류이다.
    - 분할 정복 방법은, 어떤 문제를 해결하기 위해 2개의 작은 문제로 분리하고, 각각을 해결한 뒤, 결과를 모아서 최초의 문제를 해결하는 방식을 말한다.
    - 알고리즘에서는 재귀호출을 사용한다.
    
- 정렬 과정 
1) 이미 정렬되어 있는 데이터의 그룹 혹은 묶음들을 하나로 합치는 과정을 통해 정렬을 완료한다.
2) 데이터를 절반으로 나눈다.
3) 각 부분으로 다시 절반으로 나눈다. 이 과정을 재귀호출을 통해 반복하여, 각 부분이 1개의 데이터를 이룰 때까지 반복한다. 이렇게 나누어진 각 부분을 run 이라고 한다.

![mergesortA](./images/mergesortA.png)    


4) 각각의 run 을 다시 합치는데(merge), 이때 정렬을 하면서 합쳐진다. 
5) 1개 -> 2개 -> 4개 -> 8개 의 run 들이 각각 합쳐진다.
6) 마지막 2개의 run 이 남으면, 각 run 은 이미 merge 를 반복하면서 정렬이 된 상태이다. 
7) 왼쪽 run과 오른쪽 run 의 첫 번째 데이터끼리 크기를 비교하여, 작은 값을 새로운 리스트에 저장하고, 해당 run 에서는 제거한다.
8) 왼쪽, 오른쪽 run 의 데이터가 더 이상 비교를 할 수 없을 때까지 반복한다.
9) 작은 값 순서로 저장 된 새로운 리스트를 반환한다.

![mergesortB](./images/mergesortB.png) 
    
```
<summary>
제일 작은 크기가 될 떄가지 나누고 -> 합치면서 정렬하고 -> 2 부분이 되면 작은 수 순서대로 쌓는다.

- 1 부터 2의 배수로 하나의 run 에 들어가는 데이터 수를 늘려서 병합하는 과정을 반복한 후,
- 하나의 run 의 크기가 원래 데이터의 절반이 되었을 때, 2개의 run 의 각 데이터를 비교하여 
- 작은 수 순서로 새로운 리스트에 저장하고 반환한다.
```
- 3 way 방식과 2 way 방식이 있다.
    - 3 way 는 3개의 조각으로 2 way 는 2개의 조각으로 나눈다.

## 3) 병합 정렬 알고리즘의 특징

- 장점 : 정렬 속도가 빠르다. 
    - 퀵 정렬 알고리즘과 비슷한 성능이다. 퀵 정렬이나 병합 정렬이나 분할 정복 방법과 재귀 호출 방법을 사용하기 때문이다.
    - 분할 하는데 걸리는 시간은 log2N 이고, 합치는데 걸리는 시간은 O(N) 이다.
    - 따라서 병합정렬 알고리즘의 성능은,
    ```
    O(N*log2N)
    ```

- 단점
    - 데이터가 최악의 상태인 경우에는 속도가 저하된다. 
    - 별도의 데이터 공간을 사용하기 때문에 공간 효율성은 떨어진다. 
    - 이를 해결하기 위해 연결 리스트를 사용하기도 한다.

## 4) Merge sort algorithm code 1

```
from math import log10
from random import randint

def merge_sort(mylist) :
    if len(mylist) <= 1 : return mylist
    half = len(mylist) // 2
    left_list = merge_sort(mylist[:half])
    right_list = merge_sort(mylist[half:])
    merged_list = []

    while len(left_list) > 0 and len(right_list) > 0 :
        if left_list[0] > right_list[0] :
            merged_list.append(right_list[0])
            right_list.pop(0)
        else :
            merged_list.append(left_list[0])
            left_list.pop(0)
    if len(left_list) > 0 : merged_list += left_list
    if len(right_list) > 0 : merged_list += right_list
    return merged_list
```
- 랜덤으로 난수 생성
```
lst = [randint(1, 99999) for i in range(20)]
print(lst,end=",")

=============================

[2542, 2770, 34308, 46369, 987, 39805, 50674, 90934, 53895, 8720, 87810, 20750, 2070, 95435, 43711, 99024, 61891, 4017, 61190, 46687]
```
- 정렬
```
sorted_lst = merge_sort(lst)
print(sorted_lst)

==============================

[987, 2070, 2542, 2770, 4017, 8720, 20750, 34308, 39805, 43711, 46369, 46687, 50674, 53895, 61190, 61891, 87810, 90934, 95435, 99024]
```
## 4) Merge Sort Algorithm 2
- https://ratsgo.github.io/data%20structure&algorithm/2017/10/03/mergesort/

```
def merge_sort(list) :
    if len(list) <= 1 :
        return list
    mid = len(list) // 2
    leftlist = list[:mid]
    rightlist = list[mid:]
    leftlist = merge_sort(leftlist)
    rightlist = merge_sort(rightlist)
    return merge(leftlist, rightlist)

def merge(left, right) :
    result = []
    while len(left) > 0 or len(right) > 0 :
        if len(left) > 0 and len(right) > 0 :
            if left[0] <= right[0] :
                result.append(left[0])
                left = left[1:]
            else :
                result.append(right[0])
                right = right[1:]
        elif len(left) > 0 :
            result.append(left[0])
            left = left[1:]
        elif len(right) > 0 :
            result.append(right[0])
            right = right[1:]
    return result
```
- 랜덤으로 난수 생성 후 정렬
```
lst = [randint(1, 99999) for i in range(10)]
print(lst)

============================================

[64298, 24037, 43412, 70207, 41299, 98774, 18574, 55555, 56175, 95179]
```
```
merge_sort(lst)

============================================

[18574, 24037, 41299, 43412, 55555, 56175, 64298, 70207, 95179, 98774]
```
## 5) Merge Sort Algorithm 3
- https://runestone.academy/runestone/books/published/pythonds/SortSearch/TheMergeSort.html

```
def mergeSort(alist) :
    print("Splitting", alist)
    if len(alist) > 1 :
        mid = len(alist) // 2
        lefthalf = alist[:mid]
        righthalf = alist[mid:]

        mergeSort(lefthalf)
        mergeSort(righthalf)

        i=0
        j=0
        k=0
        while i < len(lefthalf) and j < len(righthalf) :
            if lefthalf[i] <= righthalf[j] :
                alist[k] = lefthalf[i]
                i = i + 1
            else :
                alist[k] = righthalf[j]
                j = j + 1
            k = k + 1

        while i < len(lefthalf) :
            alist[k] = lefthalf[i]
            i = i + 1
            k = k + 1

        while j < len(righthalf) :
            alist[k] = righthalf[j]
            j = j + 1
            k = k + 1
    print("Merging ", alist)
```
- 랜덤으로 난수 생성
```
alist = [random.randint(1, 100) for i in range(10)]
print(alist)

===================================================

[49, 18, 23, 73, 2, 13, 61, 87, 88, 41]
```

- 정렬
```
mergeSort(alist)

==================================================

Splitting [49, 18, 23, 73, 2, 13, 61, 87, 88, 41]
Splitting [49, 18, 23, 73, 2]
Splitting [49, 18]
Splitting [49]
Merging  [49]
Splitting [18]
Merging  [18]
Merging  [18, 49]
Splitting [23, 73, 2]
Splitting [23]
Merging  [23]
Splitting [73, 2]
Splitting [73]
Merging  [73]
Splitting [2]
Merging  [2]
Merging  [2, 73]
Merging  [2, 23, 73]
Merging  [2, 18, 23, 49, 73]
Splitting [13, 61, 87, 88, 41]
Splitting [13, 61]
Splitting [13]
Merging  [13]
Splitting [61]
Merging  [61]
Merging  [13, 61]
Splitting [87, 88, 41]
Splitting [87]
Merging  [87]
Splitting [88, 41]
Splitting [88]
Merging  [88]
Splitting [41]
Merging  [41]
Merging  [41, 88]
Merging  [41, 87, 88]
Merging  [13, 41, 61, 87, 88]
Merging  [2, 13, 18, 23, 41, 49, 61, 73, 87, 88]
```

## 참고 사이트
```
https://ratsgo.github.io/data%20structure&algorithm/2017/10/03/mergesort/
https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html
https://runestone.academy/runestone/books/published/pythonds/SortSearch/TheMergeSort.html
```
