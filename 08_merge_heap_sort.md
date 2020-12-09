# 1. Merge Sort Algorithm

## 2). 병합 정렬 알고리즘이란?

## 3). 병합 정렬 알고리즘의 특징

- 장점

- 단점

## 4) Merge Sort Algorithm 1

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
