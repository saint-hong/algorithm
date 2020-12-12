# 1. Heap Sort Algorithm

## 1) 힙 정렬 알고리즘 이란?

- 완전이진트리 구조의 특징을 1차원 배열로 변환하여 정렬하는 알고리즘
    - 완전이진트리 : 한 노드에 최대 두 개의 자식노드를 가진다. 마지막 레벨을 제외한 모든 레벨에 노드들이 꽉 채워져 있다.

- 힙 정렬의 속성
    - max heap : 각 노드의 값은 자식노드의 값보다 크거나 같다.
    - min heap : 각 노드의 값은 자식노드의 값보다 작거나 같다.
    
- heapify : 주어진 데이터를 이진트리화 했을 때, 힙 정렬의 속성을 만족하도록 하는 연산.
    - max heap 일 경우 부모노드의 값을 자식노드와 비교하여 큰 값과 작은 값의 위치를 바꾸는 과정.
    - 같은 레벨의 노드들은 값의 크기가 어느쪽이 크든 상관 없다.

- insert : 힙의 자료구조에 새로운 값을 삽입하는 방식으로 부모노드가 자식노드보다 값이 크거나 같다는 조건을 기준으로 재정렬하는 과정.
    - 마지막 레벨이 가장 왼쪽 자식노드에 새로운 값을 넣는다.
    - 새로운 값을 부모노드와 비교하여 큰 경우 자리를 바꿔준다.
    - 형제노드는 이미 max heap 조건에 맞춘 것이기때문에 부모노드와 비교해도 된다.
    - 아래서 위로 heapify 하는 과정

- delete : 힙의 자료구조에서 어떤 값을 삭제할 때 쓰는 방식으로 부모노드가 자식노드보다 값이 크거나 같다는 조건을 기준으로 재정렬 하는 과정.
    - 삭제하려는 값의 노드에 이진트리의 가장 마지막 레벨의 오른쪽 노드 값을 옮긴다.
    - 새로 옮겨진 값을 자식노드들과 비교하여 재정렬한다.
    - 위에서 아래로 heapify 하는 과정

- build heap : 주어진 데이터를 max heap 의 구조로 바꾸기 위한 처리과정.
    - 데이터의 index 순서데로 이진트리의 각 노드에 배치한다고 가정.
    - 전체 데이터 길이를 2로 나눈 몫에 해당하는 노드, 즉 배열의 중간에 위치한 데이터부터 heapify 를 시작하면, 이진트리의 성질에 의해 모든 값들을 한 번씩 비교할 수 있게 된다.
    - 중간 데이터부터 시작하여 같은 레벨의 노드의 데이터를 자식레벨과 비교하여 위치를 조정한다.
    - 같은 레벨의 조정이 끝나면 상위 레벨의 노드들을 자식노드들과 비교하여 위치를 조정한다.

## 2) 힙 정렬 알고리즘의 특징
- 장점 :
    
- 단점 :
    
## 3) heap sort algorithm code 1

```
import random
from random import randint

def left_node(idx=None) :
    return ((idx + 1) << 1) - 1  # 왼쪽자식 노드의 인덱스를 반환한다.

def right_node(idx=None) :
    return ((idx + 1) << 1)      # 오른쪽자식 노드의 인덱스를 반환한다.

def up_heap(mylist=None, idx=None, heap_size=None) :
    l_node = left_node(idx)  # idx = 4, l_node = 9
    r_node = right_node(idx) # idx = 4, r_node = 10

    if l_node <= heap_size and mylist[l_node] > mylist[idx] : # 9 <= 9, mylist[9] = 448, mylist[4] = 8
        largest = l_node   # 9
    else :
        largest = idx
    if r_node <= heap_size and mylist[r_node] > mylist[largest] : # 10 <= 9, largest = l_node 9
        largest = r_node
    if largest != idx :   # largest = 9 idx = 4
        mylist[idx], mylist[largest] = mylist[largest], mylist[idx] # 8, 448 = 448, 8
        up_heap(mylist, largest, heap_size)

def build_heap(mylist=None) :
    heap_size = len(mylist) - 1   # len(mylist) = 10, heap_size = 9
    for i in reversed(range(len(mylist) // 2)) :  # range(5)
        up_heap(mylist, i, heap_size)  # i = 4, 3, 2, 1, 0, heap_size = 9

def heap_sort(heap=None) :
    tmp_arry = list()
    for i in range(len(heap)) :
        tmp_arry.append(heap.pop(0))
        up_heap(heap, 0, len(heap) - 1)
    return tmp_arry
```
