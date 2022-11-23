# 1. Bubble Sort Algorithm : 거품 정렬 알고리즘
## 1) 거품 정렬 알고리즘이란?
- 데이터의 각 인덱스를 처음부터 끝까지 거치면서 인접한 두 데이터를 비교하여, 큰 숫자를 맨 뒤로 보내는 정렬 방식
- 처음 검사한 데이터가 가장 큰 값이 되어 맨 뒤로 이동하고나면, 이 데이터를 제외한 나머지 데이터들을 인접한 두 가지를 순차적으로 비교하여 두 번째로 큰 수를 마지막 위치에 이동 시킨다.
- 이러한 방식으로 n-1 회를 검사하여 정렬한다.

![bubblepass](./images/bubblepass.png)

## 2) 거품 정렬 알고리즘의 장점
- 코드가 비교적 단순하다.

## 3) 거품 정렬 알고리즘의 단점
- 하나의 데이터가 마지막으로 이동하기 위해서 모든 데이터와 비교를 거쳐야한다.
- 정렬의 순서에 맞지 않은 상태로 큰 값만을 마지막으로 보내기 때문에 데이터 처리 성능이 낮다.
- 교환(swap) 보다 이동(move) 을 사용하기 때문에 정렬 과정이 복잡하다.

## 4) python 의 교환 swap
- 두 데이터를 비교하고, 어떤 조건에 따라서 두 데이터를 교환하는 경우 python 에서는 다음과 같은 원리로 이루어진다.
- 먼저 i 와 j 번째 데이터를 비교하고, 두 데이터의 자리를 교환 swap 할 경우
```
① i 번째 데이터를 temp 등 임시 저장소에 저장한다. (temp = list[i])
② 리스트의 i 번째 저장소에  리스트의 j 번째 데이터값을  저장한다. (list[i] = list[j)]
③ 마지막으로 리스트의 j 번째 저장소에 원래 i 번째에 해당한 temp 데이터를 저장한다. 
```
![swap](./images/swap.png)

## 보충 설명
- 정렬을 처음 시작할 때는 0번 째 데이터부터 시작하며, 비교 데이터의 시작은 1 번째 부터 시작하여 전체 갯수에서 시작 인덱스를 뺀 갯수까지 진행한다. 
    - 1 : 0, 1, 2, 3, ..., 9
    - 2 : 0, 1, 2, 3, ..., 8
    - 3 : 0, 1, 2, 3, ..., 7
- 비교의 기준이 되는 기준 데이터를 한 칸 앞의 데이터와 비교하여 앞의 데이터가 클 경우 자리를 바꾼 후, 기분 데이터보다 한 칸 뒤의 데이터가 다시 기준 데이터가 되어 한 칸 앞의 데이터와 다시 비교와 교환을 반복하는 방식.
- 비교를 한 칸 앞의 것하고만 하며, 기준 데이터의 위치가 뒤로 움직인다. 한 번 회전할 때 가장 큰 데이터가 배열의 마지막으로 이동하게 된다. 
- 뒤 에서부터 큰 데이터가 채워진 후 앞쪽의 데이터가 정렬된다.
- 결과적으로 버블정렬 알고리즘은 한 칸의 간격을 고정하여 데이터를 비교하며, 큰 데이터를 가장 마지막에 먼저 배치해나가는 방식이다. 따라서 한 회전시 뒷 부분은 큰 데이터로 정렬되었기 때문에 다음 회전 때마다 비교 데이터의 마지막 인덱스가 점차 줄어들게 된다. 
## 5) 코드

- 거품 정렬 알고리즘
```
compare_counter = 0
swap_counter = 0

def bubble_sort(random_list) :
    global compare_counter, swap_counter

    for start_index in range(len(random_list)) :
        for index in range(1, len(random_list) - start_index) :  ### 마지막 인덱스가 하나씩 줄어든다.
            compare_counter += 1
            if random_list[index-1] > random_list[index] :       ### 앞의 숫자와 뒤의 숫자 비교
                swap_counter += 1
                temp = random_list[index-1]                      ### 앞의 숫자가 큰 경우 swap 원리를 이용하여 교환한다.
                random_list[index-1] = random_list[index]
                random_list[index] = temp
```

- 랜덤으로 숫자 데이터 생성
```
import random 

alist = []
input_num = input("데이터수 : ")
for x in range(int(input_num)) :
    alist.append(random.randint(1, int(input_num)))
```

- 결과 출력
```
import time

print("======== 정렬 전")
print(alist)
start_time = time.time()
bubble_sort(alist)
run_time = time.time() - start_time
print("======== 정렬 후")
print(alist)
print("======== 요약")
print("정렬시간 : ", run_time)
print("비교횟수 : ", compare_counter)
print("교환횟수 : ", swap_counter)
```
```
======== 정렬 전
[15, 80, 67, 20, 33, 31, 30, 66, 12, 12, 33, 56, 24, 99, 90, 3, 91, 67, 34, 96, 68, 27, 83, 18, 6, 6, 30, 67, 60, 58, 85, 3, 84, 69, 27, 10, 85, 9, 53, 52, 99, 12, 99, 17, 88, 2, 47, 33, 78, 62, 26, 4, 57, 11, 18, 63, 69, 44, 45, 13, 19, 18, 61, 65, 29, 23, 7, 55, 59, 57, 5, 99, 29, 8, 15, 56, 27, 20, 63, 21, 21, 54, 11, 39, 11, 64, 29, 74, 23, 25, 12, 31, 30, 99, 12, 28, 99, 61, 19, 89]
======== 정렬 후
[2, 3, 3, 4, 5, 6, 6, 7, 8, 9, 10, 11, 11, 11, 12, 12, 12, 12, 12, 13, 15, 15, 17, 18, 18, 18, 19, 19, 20, 20, 21, 21, 23, 23, 24, 25, 26, 27, 27, 27, 28, 29, 29, 29, 30, 30, 30, 31, 31, 33, 33, 33, 34, 39, 44, 45, 47, 52, 53, 54, 55, 56, 56, 57, 57, 58, 59, 60, 61, 61, 62, 63, 63, 64, 65, 66, 67, 67, 67, 68, 69, 69, 74, 78, 80, 83, 84, 85, 85, 88, 89, 90, 91, 96, 99, 99, 99, 99, 99, 99]
======== 요약
정렬시간 :  0.0009953975677490234
비교횟수 :  4950
교환횟수 :  2576
```

## 5)-1 다른 코드의 예
#### pythonds 의 좀 더 간단한 코드
- 서로 비교하는 데이터의 간격은 1 칸이며, 시작 데이터를 뒤로 정한 뒤, 비교 데이터를 1부터 순차적으로 이동하여 큰 데이터를 뒤 쪽으로 교환시키는 방식이다.
- 앞의 코드와 차이점은 시작 데이터의 기준을 배열의 뒷부분으로 잡았다.
    - 9 : 0, 1, 2, 3, ..., 8
    - 8 : 0, 1, 2, 3, ..., 7
    - 7 : 0, 1, 2, 3, ..., 6
- 그러나 비교 데이터의 순서는 1부터 시작하는 것은 동일하다. 

```
def bubbleSort(alist) :
    for passnum in range(len(alist)-1, 0, -1) :   ### passnum : 9,8,7,.,,2,1 
        for i in range(passnum) :                 ### passnum 이 줄어들때마다 i 에 저장되는 값의 범위가 줄어든다. 
	    if alist[i] > alist[i+1] :
	        temp = alist[i]                   ### 조건에 맞다면, swap 방식으로 교환한다.
		alist[i] = alist[i+1]
		alist[i+1] = temp
	    
```

## 6) 버블 정렬의 단점을 보완한 short bubble sort!!
- 버블 정렬 알고리즘의 단점은 몇 번의 정렬과정에서 정렬이 끝난 경우에도 각 데이터를 비교하는 실행을 지속한다.
- 즉 모든 큰 숫자가 뒤에서부터 차례대로 정렬되어 0 번째 숫자만 남을 때까지 이 작업을 실행하는 단점이 있다.
- 이러한 단점을 보완하기 위해, 정렬이 완료되면 더이상 비교를 하지 않고 검사를 종료 시키는 코드가 있다.
- shorbubble sort 라고 한다.

## 보충 설명
- 데이터가 거의 정렬이 되어 있는 경우 비교를 멈추는 코드를 추가할 수 있다.
- 시작 데이터에서 교환을 False 로 바꿔준 뒤, 비교 코드 부분에서 앞, 뒤의 크기가 다른 경우 if 문이 시작될 때 교환을 True 로 바꿔준다. 
- 한 회전을 시작할 때 False로 시작하기 때문에 현재 회전에서 if 문을 통과하지 않는다면, 즉 앞 데이터가 뒤 데이터보다 큰 경우 없다면 정렬이 되어 있으므로 False 인 채로 회전이 끝나게 되고, 다음 회전이 시작 될때 while 문의 조건을 통과하지 못하고 종료 된다. 

```
def shortBubbleSort(alist) :
    exchanges = True                     ### 교환 실행 여부의 값을 저장하는 변수 선언
    passnum = len(alist) -1              ### passnum : 전체 데이터 길이보다 1작음, 전체 인덱스
    while passnum > 0 and exchanges :    ### exchanges 가 True 이면 하위 코드 실행.
       exchanges = False                 ### while 문의 첫번째 조건을 통과하면 exchanges 를 False 로 저장
       for i in range(passnum)           ### i : 0,1,2,3...,7
           if alist[i] > alist[i+1] :    ### i 번째와 i+1 번째 비교
	        exchanges = True         ### if 조건문 통과하면, exchanges 를 True 로 저장
		temp = alist[i]          ### i 번째 데이터가 i+1 번째 데이터 보다 크면 swap
		alist[i] = alist[i+1]   
		alist[i+1] = temp
       
       passnum = passnum -1
```

```
alist=[20,30,40,90,50,60,70,80,100,110]
shortBubbleSort(alist)
print(alist)
```

- 위의 데이터에서 처음 정렬단계에서 90 이 7 번째 자리로 교환 되고,
- 다음 검사에서 전체 데이터를 비교하는데 for 문 아래의 if 문을 통과하지 않으므로 exchanges 가 False 로 남게된다.
- 3 번째 검사의 턴에서 while 문의 조건 exchanges = True 가 성립하지 않아 검사가 종료된다.

`
# 2. Shell Sort Algorithm : 쉘 정렬 알고리즘

## 1) 쉘 정렬 알고리즘이란?
- 전체 리스트를 몇 개의 부분리스트로 나누고 각 부분리스트의 각 위치에 상응하는 값끼리 비교하여 정렬한 후, 다음 검사에서는 더 작은 수의 부분리스트로 나누어 같은 방식으로 각 부분리스트의 위치에 상응하는 값끼리 비교하여 정렬한다.
- 이 때 부분리스트를 나누는 기준을 간격(gap) 이라고하고, gap 이 1이 될때까지 실행된다.
- gap 에 의해 부분리스트가 생성되면, 각 위치에 상응하는 데이터끼리는 삽입정렬 알고리즘의 원리로 정렬된다.
- 첫번째 검사에서 부분리스트를 3개를 만들었다면, 그 다음 검사에서는 더 좁은 간격의 부분리스트 6개를 만들어 비교한다. 그 다음 검사에서는 더 좁은 간격으로 부분리스트를 생성한다.

![shellsortA](./images/shellsortA.png)
![shellsortB](./images/shellsortB.png)
![shellsortC](./images/shellsortC.png)
![shellsortD](./images/shellsortD.png)

## 2) 쉘 정렬 알고리즘의 장점 
- 삽입 정렬 알고리즘의 단점을 보완한 방식으로, 인접하지 않은 데이터의 비교후 교환시 큰 거리를 이동해야하지만, 쉘 정렬 알고리즘은 부분리스트 상에서 해당하는 위치끼리 비교-교환하므로 상대적으로 큰 값이 제 위치에 있을 확률이 높다.

## 보충 설명
- 데이터 간이 크기 비교를 할 때 데이터 전체를 특정 기준으로 분할 한뒤, 분할 된 쉘의 데이터 순서에 대응하여 비교를 한 후 교환한다. 
- 한 회수가 끝나면, 더 많은 쉘로 구분하여 각 쉘의 데이터 순서에 대응하여 비교를 한 후 교환한다.
- 데이터의 쉘의 크기가 1이 될떄까지 구분하여 각 쉘 단위로 비교를 한다.
- 쉘을 구분하는 기준은 코드마다 다를 수 있다.
    - 50개의 데이터이면 : 40, 13, 4, 1
- 쉘을 구분한 뒤 2번 쉘의 1번째 데이터와 1번 쉘의 1번째 데이터의 크기를 비교한 후 큰 것과 작은 것의 위치를 교환한다. 크기의 순서가 맞으면 교환이 없다.
- 다음은 3번째 쉘과 2번째 쉘의 1번째 데이터를 비교한다. 마찬가지로 크기를 비교한 후 큰 것과 작은 것의 위치를 교환한다. 
- 이렇게 쉘이 길이에 맞게 순차적으로 비교한 후 마지막 쉘의 단위가 데이터의 길이를 벗어나면 쉘을 더 작게 구분해준다.
- 더 작아진 쉘들을 같은 방식으로 비교한 후 교환하여 정렬해 나간다.
- 쉘의 크기가 1일 될 때까지 구분한다. 

## 3) 코드

- 쉘 정렬 알고리즘

```
compare_counter = 0
swap_counter = 0

def shell_sort(num_list) :
    global compare_counter, swap_counter
    h = 1
    while h < len(num_list) :
        h = h * 3 + 1  
    h = h // 3   ### 데이터를 3등분 하기 위한 gap 
    
    while h > 0 :
        for i in range(h) :
            s_index = i + h   ### 나누어진 부분데이터의 인덱스 40, 41, 42,...,79
            
            while s_index < len(num_list) :
                temp = num_list[s_index]
                insert_index = s_index
                compare_counter += 1
                
		### 부분리스트의 각 위치별 값을 비교.
		### 0과 40 비교 후, 0이 40보다 작으면, 80과 비교한다.
                while insert_index > (h-1) and num_list[insert_index - h] > temp : 
                    swap_counter += 1
                    num_list[insert_index] = num_list[insert_index - h]
                    insert_index = insert_index - h
                
                num_list[insert_index] = temp
                s_index = s_index + h
            
        h = h // 3    ### 첫번째 검사가 끝나면, 3부분으로 나누어진 각각의 부분 데이터를 추가로 3등분 한다.
```

- 랜덤 데이터 생성

```
import random

alist = []
input_num = input("데이터수 : ")
for x in range(int(input_num)) :
    alist.append(random.randint(1, int(input_num)))
```

- 결과 출력

```
import time

print("======== 정렬 전")
print(alist)
start_time = time.time()
shell_sort(alist)
run_time = time.time() - start_time
print("======== 정렬 후")
print(alist)
print("======== 요약")
print("정렬시간 : ", run_time)
print("비교횟수 : ", compare_counter)
print("교환횟수 : ", swap_counter)
```

```
======== 정렬 전
[52, 21, 15, 79, 90, 81, 76, 33, 51, 13, 16, 31, 28, 38, 12, 6, 53, 8, 53, 89, 54, 20, 88, 14, 93, 51, 63, 45, 28, 70, 39, 64, 4, 63, 89, 38, 63, 8, 74, 35, 19, 58, 13, 21, 35, 11, 20, 16, 61, 99, 22, 6, 59, 83, 68, 27, 63, 67, 14, 44, 41, 57, 46, 24, 76, 78, 90, 76, 84, 62, 49, 73, 10, 41, 59, 77, 71, 24, 54, 95, 59, 52, 95, 98, 79, 82, 53, 66, 51, 85, 8, 35, 94, 99, 9, 34, 40, 72, 27, 30]
======== 정렬 후
[4, 6, 6, 8, 8, 8, 9, 10, 11, 12, 13, 13, 14, 14, 15, 16, 16, 19, 20, 20, 21, 21, 22, 24, 24, 27, 27, 28, 28, 30, 31, 33, 34, 35, 35, 35, 38, 38, 39, 40, 41, 41, 44, 45, 46, 49, 51, 51, 51, 52, 52, 53, 53, 53, 54, 54, 57, 58, 59, 59, 59, 61, 62, 63, 63, 63, 63, 64, 66, 67, 68, 70, 71, 72, 73, 74, 76, 76, 76, 77, 78, 79, 79, 81, 82, 83, 84, 85, 88, 89, 89, 90, 90, 93, 94, 95, 95, 98, 99, 99]
======== 요약
정렬시간 :  0.0009970664978027344
비교횟수 :  342
교환횟수 :  457
```

## 4) 다른 코드의 예
- 데이터를 부분리스트로 나누는 함수와 나누어진 부분리스트들의 데이터를 비교-교환하는 함수로 만들었다.
- 데이터가 검색을 진행을 마칠 때마다, 더 작은 수의 gap 으로 나누어지는 것을 출력해서 보여준다.

## 보충 설명
- 쉘의 사이즈를 결정하는 함수와 이것을 기준으로 각 쉘의 순서데로 비교하는 함수로 만들어진다.
- 첫번째함수는 쉘 사이즈를 정한뒤, 반복문을 통해 쉘을 끝으로 하는 숫자를 반환한다. 이렇게 반환된 숫자는 하나의 쉘의 인덱스를 의미한다. 
- 반복문이 실행되면 데이터 비교 함수를 호출하여, 전체 배열과 쉘의 인덱스 값과 쉘 사이즈를 아규먼트로 보낸다.
- 데이터 비교 함수가 실행되면, 반복문을 통해서 현재 쉘에 대한 인덱스가 주어진 반복문의 옵션에 따라서 반환된다.
	- 배열의 길이가 20이고 현재 쉘사이즈가 10 인경우, 10, 11, 12, 13, ... , 19
- 이렇게 반화되는 값은 배열의 인덱스가 되고, 현재 값과 현재 위치를 지칭한다.
- 다음 while 문에서 현재 위치 10과 이보다 쉘 사이즈 10 만큼 작은 위치인 0의 데이터의 크기를 비교하고, 작은 인덱스의 데이터가 클 경우 현재 인덱스의 값과 자리를 교환한다.
	- 10 과 0, 11 과 1, 12 와 2, ... 19와 9
- 데이터 비교 과정에서 작은 인덱스의 값이 더 작다면 현재 인덱스에 처음 비교의 시작이었던 현재값을 저장한다.
- 쉘 사이즈 10의 비교가 끝나면 (10~19), 첫번째 함수에서 다시 쉘 사이즈를 절반으로 줄인 값을 반환하고 이 값을 기준으로 다시 데이터 비교함수를 호출 한다.
- 데이터 비교함수에서 파라미터로 받은 값을 가지고 다시 각 쉘의 순서대로 데이터를 비교한 후 큰 것과 작은 것의 자리를 교환한다.
	- 5, 10, 15 / 6, 11, 16 / 7, 12, 17 / ... / 9, 14, 19
	- 0, 5, 10 / 1, 6, 11 / 2, 7, 12 /   ... /  4, 9, 14
```
def shellsort(alist) :
    sublistcount = len(alist) // 2
    while sublistcount > 0 :
        for startposition in range(sublistcount) :
            gapinsertionSort(alist, startposition, sublistcount)
            
        print("After increments of size", sublistcount,"\n","The list is : ","\n",alist)
        print("\n")
        
	sublistcount = sublistcount // 2
        
compare_counter = 0
swap_counter = 0

def gapinsertionSort(alist, start, gap) :
    global compare_counter, swap_counter
    for i in range(start+gap, len(alist), gap) :
        currentvalue = alist[i]
        position = i
        compare_counter += 1
        while position >= gap and alist[position-gap] > currentvalue :
            swap_counter += 1
            alist[position] = alist[position-gap]
            position = position-gap
            
        alist[position] = currentvalue
```

- 결과 출력
```
After increments of size 25 
 The list is :  
 [28, 23, 1, 5, 3, 12, 10, 8, 28, 8, 4, 12, 27, 3, 33, 6, 4, 35, 2, 3, 19, 8, 7, 41, 2, 30, 25, 35, 33, 23, 18, 47, 19, 47, 24, 43, 36, 41, 10, 50, 11, 16, 40, 49, 13, 37, 40, 24, 41, 25]


After increments of size 12 
 The list is :  
 [2, 3, 1, 5, 3, 12, 2, 3, 13, 8, 4, 12, 27, 23, 10, 6, 4, 16, 10, 8, 19, 8, 7, 24, 28, 25, 25, 35, 11, 23, 18, 47, 19, 37, 24, 41, 36, 30, 33, 50, 33, 35, 40, 49, 28, 47, 40, 43, 41, 41]


After increments of size 6 
 The list is :  
 [2, 3, 1, 5, 3, 12, 2, 3, 10, 6, 4, 12, 10, 8, 13, 8, 4, 16, 18, 23, 19, 8, 7, 23, 27, 25, 19, 35, 11, 24, 28, 30, 25, 37, 24, 35, 36, 41, 28, 47, 33, 41, 40, 47, 33, 50, 40, 43, 41, 49]


After increments of size 3 
 The list is :  
 [2, 3, 1, 2, 3, 10, 5, 3, 12, 6, 4, 12, 8, 4, 13, 8, 7, 16, 10, 8, 19, 18, 11, 19, 27, 23, 23, 28, 24, 24, 35, 25, 25, 36, 30, 28, 37, 33, 33, 40, 40, 35, 41, 41, 41, 47, 47, 43, 50, 49]


After increments of size 1 
 The list is :  
 [1, 2, 2, 3, 3, 3, 4, 4, 5, 6, 7, 8, 8, 8, 10, 10, 11, 12, 12, 13, 16, 18, 19, 19, 23, 23, 24, 24, 25, 25, 27, 28, 28, 30, 33, 33, 35, 35, 36, 37, 40, 40, 41, 41, 41, 43, 47, 47, 49, 50]
```

#### 쉘의 각 데이터들  비교 과정을 확인 
```
def shellsort(alist) :
    sublistcount = len(alist) // 2
    while sublistcount > 0 :
        for startposition in range(sublistcount) :
            gapinsertionSort(alist, startposition, sublistcount)
            
        #print("After increments of size", sublistcount,"\n","The list is : ","\n",alist)
        #print("\n")
        
	print("==========="
	sublistcount = sublistcount // 2
        
compare_counter = 0
swap_counter = 0

def gapinsertionSort(alist, start, gap) :
    global compare_counter, swap_counter
    for i in range(start+gap, len(alist), gap) :
        currentvalue = alist[i]
        position = i
	
	print("now gap size :", gap, "now position :", position, "position-gap :", position-gap)
	
        compare_counter += 1
        while position >= gap and alist[position-gap] > currentvalue :
            swap_counter += 1
            alist[position] = alist[position-gap]
            position = position-gap
            
        alist[position] = currentvalue
```
```
now gap size : 10 now position : 10 position-gap : 0
now gap size : 10 now position : 11 position-gap : 1
now gap size : 10 now position : 12 position-gap : 2
now gap size : 10 now position : 13 position-gap : 3
now gap size : 10 now position : 14 position-gap : 4
now gap size : 10 now position : 15 position-gap : 5
now gap size : 10 now position : 16 position-gap : 6
now gap size : 10 now position : 17 position-gap : 7
now gap size : 10 now position : 18 position-gap : 8
now gap size : 10 now position : 19 position-gap : 9
=========
now gap size : 5 now position : 5 position-gap : 0
now gap size : 5 now position : 10 position-gap : 5
now gap size : 5 now position : 15 position-gap : 10
now gap size : 5 now position : 6 position-gap : 1
now gap size : 5 now position : 11 position-gap : 6
now gap size : 5 now position : 16 position-gap : 11
now gap size : 5 now position : 7 position-gap : 2
now gap size : 5 now position : 12 position-gap : 7
now gap size : 5 now position : 17 position-gap : 12
now gap size : 5 now position : 8 position-gap : 3
now gap size : 5 now position : 13 position-gap : 8
now gap size : 5 now position : 18 position-gap : 13
now gap size : 5 now position : 9 position-gap : 4
now gap size : 5 now position : 14 position-gap : 9
now gap size : 5 now position : 19 position-gap : 14
=========
now gap size : 2 now position : 2 position-gap : 0
now gap size : 2 now position : 4 position-gap : 2
now gap size : 2 now position : 6 position-gap : 4
now gap size : 2 now position : 8 position-gap : 6
now gap size : 2 now position : 10 position-gap : 8
now gap size : 2 now position : 12 position-gap : 10
now gap size : 2 now position : 14 position-gap : 12
now gap size : 2 now position : 16 position-gap : 14
now gap size : 2 now position : 18 position-gap : 16
now gap size : 2 now position : 3 position-gap : 1
now gap size : 2 now position : 5 position-gap : 3
now gap size : 2 now position : 7 position-gap : 5
now gap size : 2 now position : 9 position-gap : 7
now gap size : 2 now position : 11 position-gap : 9
now gap size : 2 now position : 13 position-gap : 11
now gap size : 2 now position : 15 position-gap : 13
now gap size : 2 now position : 17 position-gap : 15
now gap size : 2 now position : 19 position-gap : 17
=========
now gap size : 1 now position : 1 position-gap : 0
now gap size : 1 now position : 2 position-gap : 1
now gap size : 1 now position : 3 position-gap : 2
now gap size : 1 now position : 4 position-gap : 3
now gap size : 1 now position : 5 position-gap : 4
now gap size : 1 now position : 6 position-gap : 5
now gap size : 1 now position : 7 position-gap : 6
now gap size : 1 now position : 8 position-gap : 7
now gap size : 1 now position : 9 position-gap : 8
now gap size : 1 now position : 10 position-gap : 9
now gap size : 1 now position : 11 position-gap : 10
now gap size : 1 now position : 12 position-gap : 11
now gap size : 1 now position : 13 position-gap : 12
now gap size : 1 now position : 14 position-gap : 13
now gap size : 1 now position : 15 position-gap : 14
now gap size : 1 now position : 16 position-gap : 15
now gap size : 1 now position : 17 position-gap : 16
now gap size : 1 now position : 18 position-gap : 17
now gap size : 1 now position : 19 position-gap : 18
=========
```


## 참고 사이트
https://gmlwjd9405.github.io/2018/05/08/algorithm-shell-sort.html
https://ratsgo.github.io/data%20structure&algorithm/2017/11/07/shellsort/
https://runestone.academy/runestone/books/published/pythonds/SortSearch/TheShellSort.html

