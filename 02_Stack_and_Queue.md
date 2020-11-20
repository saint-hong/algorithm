# 1. Stack : 스택
## 1) 스택 이란?
- 스택 자료구조는 프로그래밍에서 자주 쓰이는 자료구조.
- 찬장에 그릇을 쌓는 형태, 마지막에 쌓은 그릇이 제일 먼저 꺼내어지는 것과 같다.
```
LIFO : Last In First Out : 마지막에 들어간 것이 처음으로 나온다.
```

# 2. Queue : 큐
## 1) 큐 란?
- 스택과 함께 프로그래밍에서 기본적인 자료구조로 많이 쓰인다.
- 극장 매표소에 줄을 선 형태, 먼저 줄을 선 사람이 먼저 들어갈 수 있다.
```
FIFO : First In First Out : 먼저 들어간 것이 먼저 나온다.
```

## 2) 큐를 파이썬 코드로 구현
- 리스트에 저장된 데이터를 insert() 와 pop() 를 이용해 큐의 방식을 구현해 볼 수 있다.
- 그러나 리스트 데이터 타입은 무작위 접근(random access) 에 최적화된 구조이므로, insert와 pop 으로 순서를 정하는 것은 성능을 저하시킬 수 있다.

```
### insert 함수를 이용하여 첫번째 자리에 데이터를 삽입하고, pop(0) 을 이용해 첫번째 데이터를 꺼낸다.
queue = [7,8,9]
queue.insert(0, 6)
queue.insert(0, 5)
queue.insert(0, 4)
print(queue.pop(0))
print(queue.pop(0))
print(queue.pop(0))
print(queue)
========================================
4
5
6
[7, 8, 9]
```

## 3) deque 패키지 사용
- deque : double-ended queue
- collections 모듈의 deque 패키지를 사용할 수 있다.
- left 매서드를 사용하면 데이터의 왼쪽부터 채우거나, 꺼낼 수 있다.

```
from collections import deque

queue_2 = deque([4,5,6])
queue_2.append(7)
queue_2.append(8)
print(queue_2)
========================================
deque([4, 5, 6, 7, 8])
```
```
### pop.left() 를 사용하면 왼쪽부터 데이터를 꺼낼 수 있다.
print("현재 데이터 : ", queue_2)
print("꺼낸 데이터 : ", queue_2.popleft())
print("남아있는 데이터 : ", queue_2)
print("꺼낸 데이터 : ", queue_2.popleft())
print("남아있는 데이터 : ", queue_2)
========================================
현재 데이터 :  deque([4, 5, 6, 7, 8])
꺼낸 데이터 :  4
남아있는 데이터 :  deque([5, 6, 7, 8])
꺼낸 데이터 :  5
남아있는 데이터 :  deque([6, 7, 8])
```
```
### appendleft() 를 사용하면 왼쪽부터 데이터를 넣을 수 있다.
queue_2.appendleft(3)
queue_2.appendleft(2)
print("현재 데이터 : ", queue_2)
========================================
현재 데이터 :  deque([2, 3, 6, 7, 8])
```
## 4) Queue 클래스 사용
- queue 모듈의 Queue 클래스를 사용하여 구현할 수 있다.
- deque 패키지와 달리 방향성이 없다.
- 데이터 추가 : put()
- 데이터 꺼내기 : get()

```
from queue import Queue

### put 으로 데이터 추가
queue_3 = Queue()
queue_3.put(3)
queue_3.put(2)
queue_3.put(1)
========================================
### get 으로 데이터 꺼내기
### 먼저 들어간 순서데로 출력된다. 3 -> 2-> 1
print(queue_3.get())
print(queue_3.get())
print(queue_3.get())
========================================
3
2
1
```
