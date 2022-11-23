# 1. Stack : 스택

## 1) 스택 이란?
- 스택 자료구조는 프로그래밍에서 자주 쓰이는 자료구조.
- 찬장에 그릇을 쌓는 형태, 마지막에 쌓은 그릇이 제일 먼저 꺼내어지는 것과 같다.
- 컴퓨터 시스템 내부에서 자료를 처리할 떄 유용하게 쓰이는 방식이다.

```
LIFO : Last In First Out : 마지막에 들어간 것이 처음으로 나온다.
```
## 2) stack code 1
- pythonds 모듈을 설치하면 stack 패키지를 사용할 수 있다.

```
pip install pythonds
```

- stack 패키지에 들어있는 기능을 구현
```
class Stack :
    def __init__(self) :
        self.items = []

    def isEmpty(self) :     # stack 에 데이터가 들어있는지 확인
        return self.items == []

    def push(self, item) :  # stack 에 데이터를 저장
        self.items.append(item)

    def pop(self) :         # stack 에 저장 된 데이터를 꺼내고 삭제. 가장 최근에 저장된 데이터.
        return self.items.pop()

    def peek(self) :        # stack 의 마지막 데이터를 꺼냄.
        return self.items[len(self.items)-1]

    def size(self) :        # stack 의 길이를 반환.
        return len(self.items)
```
- 출력

```
s = Stack()            # 클래스 Stack 호출
print(s.isEmpty())     # stack 의 데이터 저장 여부 확인
==================
True
```

```
s.push(10)             # stack 에 push 함수를 사용하여 데이터를 저장
s.push(5)
s.push('code')
s.push(True)
print(s.items)         # stack 에 저장 된 데이터 출력
==================
[10, 5, 'code', True]
```

```
print(s.pop())         # stack 에 저장 된 데이터의 마지막 것을 배내고 삭제
print(s.pop())
==================
True
code

print(s.items)         # 현재 stack 의 데이터 출력
==================
[10, 5]
```
## 3) stack code 2
- pythonds 의 stack 패키지를 사용하지 않은 경우

```
def push(item) :
    stack.append(item)

def pop() :
    return stack.pop()
```
```
stack = []
push(1)
push(2)
push(3)
push(4)
print("현재 스택의 모습")
print(stack)
====================
현재 스택의 모습
[1, 2, 3, 4]
```
```
while stack :            # stack 이 False 가 될 때까지 pop로 데이터를 출력
    print("POP -> {}".format(pop()))
====================
POP -> 4
POP -> 3
POP -> 2
POP -> 1
```

## 4) balanced parenthesis problem 
- 프로그래밍 언어에서 잘 만들어진 괄호와 잘 못만들어진 괄호를 구별하는 문제가 자주 인용된다.
- stack 의 기능을 사용하여 열린 괄호와 닫힌 괄호의 짝이 맞는지 검증해 본다.

```
from pythonds.basic import Stack

def parChecker(symbolString) :
    s = Stack()                        # Stack 정의
    balanced = True                    # 괄호의 열고 닫힘이 잘 되었는지 평가하기 위한 변수
    index = 0                          # 파라미터에 적용할 데이터의 순서

    while index < len(symbolString) and balanced : # 파라미터의 길이가 0 보다 크고, 밸런스 변수가 True 일 경우 통과
        symbol = symbolString[index]   # 파라미터의 index 데이터를 symbol 변수에 저장
        if symbol == "(" :             # 이 symbol 이 "(" 열린 기호이면, 통과
            s.push(symbol)             # "(" 기호를 stack 에 넣고, if 문을 나와 index + 1 가 실행되고 다시 while 문 진행
        else :                         # 위에서 symbol 이 "(" 아니면 else 문 통과
            if s.isEmpty() :           # stack 에 열린 괄호 기호가 push 됐는지 판단.
                balanced = False       # stack 이 비어있다면 열린 괄호가 없다는 의미로 밸런스 변수를 False 로 저장
            else :                     # stack 이 비어있지않다면 열린 괄호가 있으므로 처음에 하나를 빼낸다. 이 의미는 위의 else 문에서 닫힌 괄호를 판단했기때문에 짝이 맞다는 것.
                s.pop()

        index = index + 1              # if 문을 통해 열린,닫힌 괄호의 짝을 판단하고 index 를 계속 추가한 상황. while 문에서 파라미터의 길이보다 index 가 크면 while 문을 통과하지 않고 아래 코드 실행.

    if balanced and s.isEmpty() :      # 밸런스가 True 인 상황은, 닫힌 괄호가 symbol 에 저장된 시점까지 열린괄호가 짝으로 들어 있다는 뜻. s.isEmpty() 가 True 인 상황은, 닫힌 괄호가 나올 때마다 열린 괄호를 pop 으로 지웠기때문에, 짝이 다 맞다는 의미.
        return True
    else :                             # 밸런스 변수가 False 인 경우는, 닫힌 괄호가 symbol 저장될 떄까지 stack 에 열린괄호가 없는 상황. s.isEmpty() 가 False 인 경우는 닫힌 괄호가 나왔을때 stack 에 열린괄호가 없으므로 짝이 맞지 않는 것.
        return False
```
- 코드 실행
```
print(parChecker('((()))'))
====================
True

print(parChecker('(()()(((())))'))
====================
False
```

## 5) balanced symbols (a general case)
- 위의 괄호 검증 문제를 일반적인 상황으로 확대시켜 볼 수 있다.
- 여러가지 괄호 기호가  짝이 잘 맞는지, 타입과 함께 검증할 수 있다.
- matches 함수를 만들어 심볼들의 타입을 비교할 수 있다.
```
from pythonds.basic import Stack

def parChecker_2(symbolString) :
    s = Stack()
    balanced = True
    index = 0
    
    while index < len(symbolString) and balanced :
        symbol = symbolString[index]
        if symbol in "[{(" :
            s.push(symbol)
        else :
            if s.isEmpty() :
                balanced = False
            else :
                top = s.pop()
                if not matches(top, symbol) :  # matches 함수를 호출하여, 현재 symbol에 저장된 기호와 stack 에서 빼낸 기호가 같은 타입인지 판단한다.
                    balanced = False
        index = index + 1
        
    if balanced and s.isEmpty() :
        return True
    else :
        return False
    
def matches(open, close) :                     # 인덱스의 번호로 타입을 확인하는 방식의 함수
    opens = "[{("                              # opens 와 closers 에 기호의 타입이 같은 것을 같은 위치에 놓는다. 
    closers = "]})"
    return opens.index(open) == closers.index(close)    # .index(open) 은 opens 의 일치하는 기호의 index 를 출력한다. 
```
- 코드 실행
```
print(parChecker_2('{({([][])}())}'))
print(parChecker_2('[{()]'))
=====================
True
False
```
# 2. Queue : 큐

## 1) 큐 란?
- 스택과 함께 프로그래밍에서 기본적인 자료구조로 많이 쓰인다.
- 새로운 데이터가 들어가면 한 쪽 끝인 front로 가고, 뒤에 들어온 데이터는 반대쪽 끝인 rear 에 있게 된다.
- 새로운 데이터가 들어오면 rear 에 있던 먼저 들어온 것이 front 로 이동한다.
- 데이터 컬렉션에 가장 오래 들어있던 데이커가 front 에 있게 된다.
- 이러한 자료구조를 "FIFO" 라고 부른다.  
    - First In First Out : 먼저 들어간 것이 먼저 나온다.
    - First-come- First-served : 선착순, 이라고 부르기도 한다.
    
- 극장 매표소에 줄을 선 형태, 먼저 줄을 선 사람이 먼저 들어갈 수 있다. 
- 회사에서 여러대의 컴퓨터가 연결된 프린터기는 큐 방식으로 인쇄물을 처리한다.
- 컴퓨터의 운영 체제는 여러가지 큐를 사용하여 컴퓨터 내의 프로세스를 처리한다.


## 2) 큐를 파이썬 코드로 구현
- 리스트에 저장된 데이터를 insert() 와 pop() 를 이용해 큐의 방식을 구현해 볼 수 있다.
- 그러나 리스트 데이터 타입은 무작위 접근(random access) 에 최적화된 구조이므로, insert와 pop 으로 순서를 정하는 것은 성능을 저하시킬 수 있다.

- 코드 1
``
class Queue :
    def __init__(self) :
        self.items = []

    def isEmpty(self) :
        return self.items == []

    def enqueue(self, item) :            # queue 에 데이터를 저장. .insert(0, item) 으로 0번째 인텍스에 저장.
        self.items.insert(0, item)

    def dequeue(self) :
        return self.items.pop()

    def size(self) :
        return len(self.items)`
``
- Queue 클래스를 호출하고 함수를 실행
```
q = Queue()

q.enqueue(4)
q.enqueue('dog')
q.enqueue(True)
```
```
print(q.size())
print(q.isEmpty())
print(q.items)
print(q.dequeue())
print(q.dequeue())
print(q.items)
============================
3
False
[True, 'dog', 4]
4
dog
[True]
```

- 코드 2
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
