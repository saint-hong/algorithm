# 1. Heap Sort Algorithm

## 1) 힙 정렬 알고리즘 이란?

- 완전이진트리 구조의 특징을 1차원 배열로 변환하여 정렬하는 알고리즘
    - 완전이진트리 : 한 노드에 최대 두 개의 자식노드를 가진다. 마지막 레벨을 제외한 모든 레벨에 노드들이 꽉 채워져 있다.

- 힙 정렬의 속성
    - max heap : 각 노드의 값은 자식노드의 값보다 크거나 같다.
    - min heap : 각 노드의 값은 자식노드의 값보다 작거나 같다.

![binaryheap_min_max](./images/binaryheap_min_max.png)

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

![binaryheap_max_1](./images/binaryheap_max_1.png)

## 2) 힙 정렬 알고리즘의 특징
- 장점 :
    
- 단점 :
    
## 3) max heap sort algorithm code 1

```
import random
from random import randint

def left_node(idx=None) :
    return ((idx + 1) << 1) - 1  # 왼쪽자식 노드의 인덱스를 반환한다.

def right_node(idx=None) :
    return ((idx + 1) << 1)      # 오른쪽자식 노드의 인덱스를 반환한다.

def up_heap(mylist=None, idx=None, heap_size=None) :
    l_node = left_node(idx)      # 왼쪽자식 노드의 인덱스 호출
    r_node = right_node(idx)     # 오른쪽자식 노드의 인덱스 호출

    if l_node <= heap_size and mylist[l_node] > mylist[idx] :   # 현재노드와 왼쪽자식노드를 비교, 큰 값의 인덱스를 largest 에 저장
        largest = l_node
    else :
        largest = idx
    if r_node <= heap_size and mylist[r_node] > mylist[largest] :   # 오른쪽자식 노드와 위에서 저장된 largest를 비교한 후 largest 리셋.
        largest = r_node
    if largest != idx :                                     # largest 가 현재 인덱스가 아니라면, 즉 현재노드가 자식노드보다 작다면.
        mylist[idx], mylist[largest] = mylist[largest], mylist[idx]   # 큰 값이 있는 자식노드와 현재노드의 값을 바꾼다.
        up_heap(mylist, largest, heap_size)                           # 바뀐 자리의 값을 다시 자식노드들과 비교한다.

def build_heap(mylist=None) :
    heap_size = len(mylist) - 1
    for i in reversed(range(len(mylist) // 2)) :  # 배열의 중간위치의 인덱스에서 역순으로 출력. 4,3,2,1,0
        up_heap(mylist, i, heap_size)             # 배열의 중간위치에 해당하는 노드부터 상위레벨로 올라가면서 이진트리구조를 정렬시킨다.

def heap_sort(heap=None) :
    tmp_arry = list()                             # 이진트리의 루트노드의 값을 저장할 공간을 정의한다.
    for i in range(len(heap)) :                   # 배열의 길이만큼,
        tmp_arry.append(heap.pop(0))              # 힙 구조의 첫 번째 데이터, 즉 이진트리의 루트노드의 데이터를 저장하고 삭제.
        up_heap(heap, 0, len(heap) - 1)           # 가장 큰 숫자가 차례로 제거되면서 이진트리를 반복해서 만든다. 점차 데이터는 줄어든다.
    return tmp_arry                               # 루트노드, 즉 가장 큰 숫자를 차례대로 저장하면 데이터의 정렬이 완료된다.
```

- 랜덤 리스트 생성
```
data = []
input_n = input("data : ")
data = [random.randint(1, 100) for i in range(int(input_n))]
print(data)

===== <print> =====

data : 50
[47, 21, 73, 4, 76, 1, 51, 41, 1, 27, 68, 25, 20, 59, 68, 66, 83, 47, 98, 68, 100, 63, 16, 1, 87, 18, 74, 13, 52, 61, 62, 12, 44, 76, 76, 32, 45, 59, 16, 2, 33, 41, 90, 18, 17, 10, 85, 68, 59, 67]
```

- 데이터 배열을 이진트리의 속성에 맞게 재배열 (부모노드 > 자식노드)
```
build_heap(data)
```

- 이진트리의 배열을 내림차순으로 정렬
```
sorted_data = heap_sort(data)
print(sorted_data)

===== <print> =====

[100, 98, 90, 87, 83, 76, 85, 76, 76, 68, 73, 74, 68, 68, 67, 66, 63, 68, 59, 61, 59, 62, 59, 52, 51, 20, 47, 47, 44, 41, 41, 33, 45, 32, 27, 25, 16, 4, 21, 18, 18, 16, 17, 13, 12, 10, 1, 2, 1, 1]
```

## 3)-1 코드 탐색
- 비트 연산자를 사용하여 현재 노드의 좌,우 자식노드의 인덱스를 구한다.
- 10 진법의 숫자를 2 진법의 데이터 전환하고, >>, << 연산자를 사용하면 데이터를 변형할 수 있다.
```
print("parents_child node index")
for i in range(10) :
    print("p_node :", i, "left_child :", ((i + 1) << 1) -1, "right_child :", (i + 1) << 1)

===== <print> =====

parents_child node index
p_node : 0 left_child : 1 right_child : 2
p_node : 1 left_child : 3 right_child : 4
p_node : 2 left_child : 5 right_child : 6
p_node : 3 left_child : 7 right_child : 8
p_node : 4 left_child : 9 right_child : 10
p_node : 5 left_child : 11 right_child : 12
p_node : 6 left_child : 13 right_child : 14
p_node : 7 left_child : 15 right_child : 16
p_node : 8 left_child : 17 right_child : 18
p_node : 9 left_child : 19 right_child : 20
```

- 역순으로 출력하기
```
for test in reversed(range(5)) :
    print(test)

===== <print> =====

4
3
2
1
0
```

## 4) max heap sort algorithm 2
- https://github.com/TheAlgorithms/Python/blob/master/sorts/heap_sort.py
```
def heapify(unsorted, index, heap_size) :
    largest = index              # 현재 인덱스는 배열의 중간위치부터 시작.
    left_index = 2 * index + 1   # 왼쪽자식노드의 인덱스 산출
    right_index = 2 * index + 2  # 오른쪽자식노드이 인덱스 산출

    if left_index < heap_size and unsorted[left_index] > unsorted[index] :  # 자식노드와 현재노드의 값을 비교하여 큰 값을 largest 에 저장.
        largest = left_index
    if right_index < heap_size and unsorted[right_index] > unsorted[largest] :  # 위에서 비교하여 저장한 largest 를 오른쪽자식 노드와 비교. 위에서 index 가 left 보다 컸다면, right 와도 비교해야한다. 위에서 left 가 컸다면 right 와 비교하여 largest 값을 결정하면, index 가 어디에 위치해야하는지가 명확해진다.
        largest = right_index
    if largest != index :     # 위에서 비교한 결과 현재노드가 값이 컸다면, largest = index 로 if문 탈출, 바뀌었다면, 값의 위치를 바꾼다.
        unsorted[largest], unsorted[index] = unsorted[index], unsorted[largest]
        heapify(unsorted, largest, heap_size)

def heap_sort(unsorted) :
    n = len(unsorted)

    for i in range(n // 2 - 1, -1, -1) :  # 배열의 중간값 노드부터~루트노드까지 옮기면서 max heap 구조로 만든다.
        heapify(unsorted, i, n)

    for i in range(n - 1, 0, -1) :  # 배열의 갯수를 줄여가면서, 첫번째 데이터와 마지막 데이터의 값을 바꾼다. 루트노드와 리프노드 값을 바꾸어 heapify 를 반복한다. 0 제외.
        unsorted[0], unsorted[i] = unsorted[i], unsorted[0]
        heapify(unsorted, 0, i)     # 이 반복에서 정렬이 이루어진다.
    return unsorted
```

- 랜덤리스트 생성
```
from random import randint

lst = []
input_n = input("data : ")
lst = [randint(1, 999) for x in range(int(input_n))]
print(lst)

===== <print> =====

data : 10
[881, 324, 584, 578, 617, 610, 414, 521, 660, 637]
```

- 데이터 정렬
```
heap_sort(lst)

===== <print> =====

[324, 414, 521, 578, 584, 610, 617, 637, 660, 881]
```

## 4)-1 코드탐색

- 역순으로 출력
- 배열의 -1 번째는 마지막 데이터, 순서를 -1 로 하면 역으로 출력 해준다.
```
for test in range(10//2-1, -1, -1) :
    print(test)


===== <print> =====
4
3
2
1
0
```

## 5) min heap sort algorithm code
- https://runestone.academy/runestone/books/published/pythonds/Trees/BinaryHeapImplementation.html
- pythonds 모듈에서 제공하는 binary heap 패키지를 사용한다.
    - BinaryHeap() : 새로운 바이너리 힙 생성
    - insert(k) : 힙에 새로운 데이터 추가
    - findMin() : 가장 작은 데이터를 반환하고, 힙에 그대로 남겨둔다.
    - delMin() : 가장 작은 데이터를 반환하고, 힙에서 지운다.
    - isEmpty() : 힙이 비어있다면 True 를, 비어있지않다면 False 를 반환한다.
    - size() : 힙의 길이를 반환한다.
    - buildHeap(list) : 데이터에서 새로운 힙을 만든다.

```
from pythonds.trees import BinHeap

bh = BinHeap()   # BinHeap 클래스 호출
bh.insert(5)     # 리스트에 데이터 삽입
bh.insert(10)
bh.insert(35)
bh.insert(11)
bh.insert(3)

print(bh.delMin()) # 루트노드의 위치에 가장 작은 데이터를 출력
print(bh.delMin())
print(bh.delMin())
print(bh.delMin())
print(bh.delMin())

===== <print> =====

3
5
10
11
35
```

- 모듈의 함수를 python code 로 구현
```
class BinHeap :
    def __init__(self) :                        # 생성자 함수로 바이너리 힙 구현
        self.heapList = [0]                     # 힙리스트에 0을 저장. 배열의 데이터 저장은 1부터 시작.
        self.currentSize = 0                    # 힙의 크기를 추적할 때 사용된다.

    def insert(self, k) :                       # 바이너리힙에 데이터를 추가하기 위한 함수.
        self.heapList.append(k)                 # 배열의 끝, 즉 이진트리의 마지막 노드에 추가.
        self.currentSize = self.currentSize + 1
        self.percUp(self.currentSize)           # 이진트리의 속성에따라 추가된 데이터를 재배열.
    
    # min heap 의 속성대로 작은 것을 상위 노드로 옮기면서 배열을 정렬하는 함수.
    # 부모노드가 p 라면, left는 2p, right는 2p+1 # 자식노드 기준으로 부모노드는 2로 나눈 몫이 된다.
    def percUp(self, i) :
        while i // 2 > 0 :                      # 현재 노드 i 의 부모 인덱스는 2로 나눈 몫이된다.
            if self.heapList[i] < self.heapList[i//2] :     # 현재 노드와 부모노드 비교.
                tmp = self.heapList[i//2]       # 현재 노드가 부모노드보다 작으면 swap.
                self.heapList[i//2] = self.heapList[i]
                self.heapList[i] = tmp
            i = i // 2                          # 부모노드의 부모노드를 계산하고 다시 while 문 실행.

    def percDown(self, i) :
        while (i*2) <= self.currentSize :       # i 의 left 가 전체길이보다 작거나 같아야함.
            mc = self.minChild(i)               # i 의 left와 right 중에서 작은 것을 반환.
            if self.heapList[i] > self.heapList[mc] : # i 와 작은 것을 비교하고,
                tmp = self.heapList[i]                # 큰 것은 아래로, 작은 것은 상위의 노드로 올려준다.
                self.heapList[i] = self.heapList[mc]
                self.heapList[mc] = tmp
            i = mc                              # 크기비교에서 자리가 바뀐 현재 i를 다시 자식노드와 비교한다.

    # 현재 노드의 좌우 자식노드 중 작은 것의 인덱스를 반환하는 함수.
    # i*2 : leftchild, i*2+1 : rightchild
    def minChild(self, i) :
        if i*2+1 > self.currentSize :            # i 의 right 가 전체 길이보다 크면 안된다.
            return i*2                           # right 가 전체 길이보다 크면 left 를 반환한다.
        else :                                   # right 가 전체 길이보다 작으면,
            if self.heapList[i*2] < self.heapList[i*2+1] :   # left와 right 를 비교.
                return i*2                       # 작은 것의 인덱스를 반환한다.
            else :
                return i*2+1
                
    # 루트노드에 해당하는 데이터를 삭제하고, 리프노드의 데이터로 대체해주는 함수
    def delMin(self) :
        retval = self.heapList[1]                # 배열의 1번이 루트노드에 해당한다.
        self.heapList[1] = self.heapList[self.currentSize] # 루트노드와 리프노드를 swap.
        self.currentSize = self.currentSize -1   # 배열길이가 하나 작아진다.
        self.heapList.pop()                      # 배열에서 마지막 데이터를 꺼내고 삭제.
        self.percDown(1)                         # 새로운 루트노드를 기준으로 다시 재배열한다.
        return retval                            # 재배열이 끝난 배열의 루트 노드를 반환한다.

    # 데이터 배열을 이진트리의 속성에 맞게 재배열해주는 함수 
    def buildHeap(self, alist) :
        i = len(alist) // 2                      # 배열의 앞에 0을 추가하므로 1이 루트노드이고, 배열의 중앙에 위치한 노드를 기준으로 이진트리를 구성한다.
        self.currentSize = len(alist)            # 전체길이가 현재 사이즈에 저장된다.
        self.heapList = [0] + alist[:]           # 배열의 앞에 0을 추가. 배열과 이진트리의 노드의 위치를 같게해주는 효과. 배열의 1이 루트노드이다.
        while (i>0) :                            # 이진트리의 기본속성에 맞게 모든 레벨에 노드가 있어야한다.
            self.percDown(i)                     # 이진트리를 min heap 의 속성에 맞게 배열한다.
            i = i - 1                            # i 의 부모노드를 반복해서 재배열한다.
        return self.heapList
```

- 랜덤리스트 생성
```
from random import randint

lst = []
lst = [randint(1, 999) for x in range(10)]
print(lst)

===== <print> =====

[122, 18, 240, 363, 18, 808, 217, 666, 984, 24]
```

- BinHeap 클래스 호출
```
bh = BinHeap()
```

- 랜덤리스트를 이진트리에 맞개 배열
- 배열의 앞자리에 0을 추가하여, 부모노드와 자식노드의 인덱스를 구하기 쉽게 처리한다.
```
print(bh.buildHeap(lst))

===== <print> =====

[0, 18, 18, 217, 363, 24, 808, 240, 666, 984, 122]
```

- 루트노트에 들어가는 가장 작은 데이터를 출력
- 루트노드의 데이터를 반환하면서 heaplist 에서는 삭제된다.
- 루트노드의 자리에 리프노드의 데이터가 이동하게된다.
```
for j in range(3) :
    print(bh.delMin())

print("current heaplist : ", bh.heapList)
print("current size : ", bh.currentSize)

===== <print> =====

18
18
24
current heaplist :  [0, 122, 363, 217, 666, 984, 808, 240]
current size :  7
```

- 현재 배열에 데이터를 삽입
- 삽입하게되면 percdown 함수가 실행되어 이진트리를 재정렬 한다.
- 재정렬한 이진트리에서 delMin 함수를 실행하면, 루트노드에 저장된 가장 작은 값을 반환해준다.
```
bh.insert(500)
bh.insert(768)
bh.insert(365)
print("current heaplist : ", bh.heapList)

===== <print> =====

current heaplist :  [0, 122, 363, 217, 500, 365, 808, 240, 666, 768, 984]
```

```
print("====before sorted")
print(bh.heapList)

sorted_lst = []
for j in range(10) :
    sorted_lst.append(bh.delMin())

print("====after sorted")
print(sorted_lst)

===== <print> =====

====before sorted
[0, 122, 363, 217, 500, 365, 808, 240, 666, 768, 984]

====after sorted
[122, 217, 240, 363, 365, 500, 666, 768, 808, 984]
```
