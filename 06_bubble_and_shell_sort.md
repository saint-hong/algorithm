
bubblepass.png	shellsortB.png	shellsortD.png
shellsortA.png	shellsortC.png	swap.png


# 1. Bubble Sort Algorithm : 거품 정렬 알고리즘
## 1) 거품 정렬 알고리즘이란?
- 데이터의 각 인덱스를 처음부터 끝까지 거치면서 인접한 두 데이터를 비교하여, 큰 숫자를 맨 뒤로 보내는 정렬 방식
- 처음 검사한 데이터가 가장 큰 값이 되어 맨 뒤로 이동하고나면, 이 데이터를 제외한 나머지 데이터들을 인접한 두 가지를 순차적으로 비교하여 두 번째로 큰 수를 마지막 위치에 이동 시킨다.
- 이러한 방식으로 n-1 회를 검사하여 정렬한다.

![bublepass](./images/bubbleapss.png)

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

## 코드

- 랜덤으로 숫자를 선택하여 만든 데이터 생성
```
import random
import copy

if __name__ == '__main__' :
    lst = []
    input_n = input("데이터 수 : ")
    for i in range(int(input_n)) :
        lst.append(random.randint(0, int(input_n)))
    copy_lst = copy.copy(lst)
```

- 거품 정렬 알고리즘
```
compare_counter = 0
swap_counter = 0

def bubble_sort(random_list) :
    global compare_counter, swap_counter

    for start_index in range(len(random_list)) :
        for index in range(1, len(random_list) - start_index) :
            compare_counter += 1
            if random_list[index-1] > random_list[index] :
                swap_counter += 1
                temp = random_list[index-1]
                random_list[index-1] = random_list[index]
                random_list[index] = temp
```

- 출력
```
import time

print("정렬 전")
print(lst)

start_time = time.time()
bubble_sort(lst)
running_time = time.time() - start_time
print("\n")
print("정렬 후")
print(lst)
print("\n")
print("데이터 수 : {}".format(int(input_n)))
print("정렬 시간 : {}".format(running_time))
print("비교 횟수 : {}".format(compare_counter))
print("교환 횟수 : {}".format(swap_counter))
==================================================
정렬 전
[33, 77, 71, 76, 29, 41, 77, 40, 31, 15, 13, 89, 64, 27, 18, 18, 42, 45, 12, 7, 30, 68, 63, 67, 2, 28, 46, 41, 70, 9, 89, 14, 11, 9, 75, 95, 74, 61, 24, 63, 68, 88, 52, 47, 89, 76, 59, 50, 77, 54, 50, 99, 6, 41, 72, 97, 47, 34, 14, 6, 3, 11, 96, 49, 12, 89, 25, 33, 97, 65, 34, 49, 75, 66, 27, 1, 100, 56, 80, 19, 75, 91, 94, 13, 30, 60, 74, 76, 58, 55, 63, 52, 96, 36, 15, 38, 39, 39, 54, 79]


정렬 후
[1, 2, 3, 6, 6, 7, 9, 9, 11, 11, 12, 12, 13, 13, 14, 14, 15, 15, 18, 18, 19, 24, 25, 27, 27, 28, 29, 30, 30, 31, 33, 33, 34, 34, 36, 38, 39, 39, 40, 41, 41, 41, 42, 45, 46, 47, 47, 49, 49, 50, 50, 52, 52, 54, 54, 55, 56, 58, 59, 60, 61, 63, 63, 63, 64, 65, 66, 67, 68, 68, 70, 71, 72, 74, 74, 75, 75, 75, 76, 76, 76, 77, 77, 77, 79, 80, 88, 89, 89, 89, 89, 91, 94, 95, 96, 96, 97, 97, 99, 100]


데이터 수 : 100
정렬 시간 : 0.0009951591491699219
비교 횟수 : 4950
교환 횟수 : 2256
```
# 2. Shell Sort Algorithm : 쉘 정렬 알고리즘

## 코드

- 쉘 정렬 알고리즘
```
compare_counter_2 = 0
swap_counter_2 = 0

def shell_sort(num_list) :
    global compare_counter_2, swap_counter_2
    h = 1

    while h < len(num_list) :
        h = h * 3 + 1
    h = h // 3

    while h > 0 :
        for i in range(h) :
            s_index = i + h
            while s_index < len(num_list) :
                temp = num_list[s_index]
                insert_index = s_index
                compare_counter_2 += 1
                while insert_index > (h-1) and num_list[insert_index - h] > temp :
                    swap_counter_2 += 1
                    num_list[insert_index] = num_list[insert_index - h]
                    insert_index = insert_index - h

                num_list[insert_index] = temp
                s_index = s_index + h

            h = h // 3
```

- 출력
```
print("정렬 전")
print(copy_lst)
start_time_2 = time.time()
bubble_sort(copy_lst)
running_time_2 = time.time() - start_time_2
print("\n")
print("정렬 후")
print(copy_lst)
print("\n")
print("데이터 수 : {}".format(int(input_n)))
print("정렬 시간 : {}".format(running_time_2))
print("비교 횟수 : {}".format(compare_counter_2))
print("교환 횟수 : {}".format(swap_counter_2))
=================================================
정렬 전
[52, 68, 38, 45, 29, 24, 25, 3, 38, 21, 6, 48, 73, 32, 61, 86, 73, 90, 13, 51, 67, 98, 37, 74, 99, 41, 14, 77, 80, 18, 73, 85, 12, 68, 26, 62, 36, 17, 72, 56, 76, 17, 98, 81, 56, 16, 21, 94, 46, 58, 83, 51, 16, 25, 20, 85, 26, 41, 34, 98, 74, 32, 9, 57, 10, 64, 76, 30, 40, 32, 56, 43, 72, 87, 23, 88, 80, 61, 8, 48, 99, 94, 60, 82, 14, 27, 15, 68, 81, 92, 66, 94, 60, 59, 99, 7, 67, 71, 50, 85]


정렬 후
[3, 6, 7, 8, 9, 10, 12, 13, 14, 14, 15, 16, 16, 17, 17, 18, 20, 21, 21, 23, 24, 25, 25, 26, 26, 27, 29, 30, 32, 32, 32, 34, 36, 37, 38, 38, 40, 41, 41, 43, 45, 46, 48, 48, 50, 51, 51, 52, 56, 56, 56, 57, 58, 59, 60, 60, 61, 61, 62, 64, 66, 67, 67, 68, 68, 68, 71, 72, 72, 73, 73, 73, 74, 74, 76, 76, 77, 80, 80, 81, 81, 82, 83, 85, 85, 85, 86, 87, 88, 90, 92, 94, 94, 94, 98, 98, 98, 99, 99, 99]


데이터 수 : 100
정렬 시간 : 0.001993894577026367
비교 횟수 : 0
교환 횟수 : 0
```










