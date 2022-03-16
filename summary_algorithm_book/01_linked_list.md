# 1. Linked List (연결리스트)
## 1) 연결리스트란?
- 알고리즘의 기본구조이며, 많이 쓰인다.
- 알고리즘에서 사용하는 데이터와, 다음 노드를 가리키는 링크를 묶어서 노드로 정의함.
- 노드(Node) : 클래스에서 멤버변수로 정의하여 사용한다.
```
class Node :
     def __init__(self, data, next=None) :
          self.data = data
          self.next = next
```
- 링크(Link) : 노드가 다음 노드를 가리키는데 필요한 연결 정보
```  
node_A = Node("A")
node_B = Node("B")
node_A = node_B
```

## 2) 특징
- 연결리스트는 각각의 노드가 링크로 연결되어 있다.
- 연결리스트는 동적으로 메모리를 할당한다.
- 따라서 연결리스트의 중간에 어떤 데이터값의 노드를 연결시키거나 해제하여 삽입과 삭제가 간단하다.
- 배열(Array)와 비교하여 3가지의 특징이 있다.
```
①  시간의 효율성 : 삽입과 삭제에 필요한 위치검색과 삽입과정이 배열에 비해서 빠르다. 배열은 중간 데이터를 삭제하면 뒤의 데이터를 일일이 앞으로 당겨줘야 하지만, 연결리스트는 중간의 링크를 끊고 다시 연결해주기만 하면 된다. 
②  공간의 효율성 : 배열은 프로그램의 실행 중에 데이터를 변경시키지 못하지만, 연결리스트는 동적으로 메모리를 할당할 수 있어서 가능하다.
③  코드의 효율성 : 연결리스트는 포인터와 구조체로 되어 있어 배열의 인덱스 기능보다 상대적으로 코드가 복잡하게 보인다.
```
## 3) 연결리스트의 삽입과 삭제 알고리즘
### 연결리스트 예시
```
class Node :
    def __init__(self, data, next=None) :

        ### Node는 data와 next 멤버변수를 갖는다. data에는 data정보가 next에는 link정보가 저장된다.
        self.data = data
        self.next = next

def init_list() :
    global node_A

    ### node_A ~ node_D 까지 클래스를 호출하여 선언한다.
    node_A = Node("A")
    node_B = Node("B")
    node_C = Node("C")
    node_D = Node("D")

    ### 각각 노드의 next 변수에 다음 노드를 연결시킨다.
    node_A.next = node_B
    node_B.next = node_C
    node_C.next = node_D

def print_list() :
    global node_A
    node = node_A
    while node :
        print(node.data)
        node = node.next # node_A.next = node_B
    print
```

- 출력
```
### data 값이 순차적으로 출력된다.
init_list()
print_list()
A
B
C
D
```

### 연결리스트의 삽입 알고리즘
- A -> B -> D -> E 의 연결리스트 중간에 C 를 삽입
- 중요한 점은 C -> D 를 먼저 연결하고, B 와 C 를 연결 해야한다. 순서가 바뀌면 연결이 안된다.
```
class Node :
    def __init__(self, data, next=None) :
        self.data = data
        self.next = next

def init_list() :
    global node_A
    node_A = Node("A")
    node_B = Node("B")
    node_D = Node("D")
    node_E = Node("E")
    node_A.next = node_B
    node_B.next = node_D
    node_D.next = node_E

def print_list() :
    global node_A
    node = node_A
    while node :
        print(node.data)
        node = node.next # node_A.next = node_B
    print
```

### 연결리스트 중간에 데이터를 삽입하는 알고리즘
```
def insert_node(data) :
    global node_A
    new_node = Node(data) ### data = "C" 삽입
    node_P = node_A
    node_T = node_A

    while node_T.data <= data :   ### node_T.data = "A", data = "C"
        node_P = node_T           ### node_P = node_B
        node_T = node_T.next      ### node_T.next = node_B

    ### node_T.data = "D" 이면 아래 코드가 실행되어, new_node.next 가 node_D 가된다.
    ### node_P.next = node_C 가 되므로, node_A -> node_B -> node_C -> node_D 가 된다.
    new_node.next = node_T        ### node_T.data 가 D 이면 실행된다. new_node.data = "C", new_node.next = node_T = node_D
    node_P.next = new_node        ### node_P.next = node_C
```

- 출력
```
print("연결 리스트의 초기화 후")
init_list()
print_list()
print("노드 C를 추가한 후")
insert_node("C")
print_list()
================================
연결 리스트의 초기화 후
A
B
D
E
노드 C를 추가한 후
A
B
C
D
E
```

### 연결리스트의 삭제 알고리즘
```
def delete_node(del_data) :
    global node_A
    pre_node = node_A
    next_node = pre_node.next                 ### pre_node.next = node_B

    ### pre_node.data = "A", del_data = "A" 일 경우 이 조건문이 실행된다.
    if pre_node.data == del_data :
        node_A = next_node
        del pre_node
        print("delete_1")
        return

    ### next_node = node_B, del_data 가 A 가 아닌 경우 이 반복문이 실행된다.
    while next_node :
        if next_node.data == del_data :        ### "B", "D"
            pre_node.next = next_node.next     ### del_data 가 "C" 이면, pre_node.next (pre_nede = node_B) 가 node_D 를 링크하게 된다.
            del next_node
            print("delete_2")
            break
        pre_node = next_node                   ### pre_node = node_B
        next_node = next_node.next             ### noext_node = node_C
```

- 출력
```
print("연결리스트 초기화")
init_list() ### 연결리스트 초기화
print_list()
print("노드 C를 추가한 후")
insert_node("C")
print_list()
print("노드 D를 삭제한 후")
delete_node("B")
print_list()
================================
연결리스트 초기화
A
B
D
E
노드 C를 추가한 후
A
B
C
D
E
노드 D를 삭제한 후
delete_2
A
C
D
E
```

# 2. 이중 연결 리스트
## 2) 이중 연결 리스트란 ?
- 단일 연결 리스트는 노드의 링크가 한 방향으로만 향한다.
- 이중 연결 리스트는 노드의 링크가 양 방향으로 향한다.
```
A -> B -> C -> D -> C -> B -> A
```

## 3) 이중 연결 리스트의 삽입과 삭제 알고리즘
- 단일 연결 리스트와 코드는 비슷하고 prev 멤버 변수가 추가된다.

### 삽입 알고리즘
```
class Node :
    def __init__(self, data, next=None, prev=None) :
        self.data = data
        self.next = next
        self.prev = prev

def init_list() :
    global node_A
    node_A = Node("A")
    node_B = Node("B")
    node_D = Node("D")
    node_E = Node("E")

    ### 이중 연결 리스트의 링크 정의 : prev 가 추가 됨
    node_A.next = node_B
    node_B.next = node_D
    node_B.prev = node_A
    node_D.next = node_E
    node_D.prev = node_B
    node_E.prev = node_D

    ### 삽입 알고리즘
def insert_node(data) :
    global node_A
    new_node = Node(data)
    node_P = node_A
    node_T = node_A
    while node_T.data <= data :
        node_P = node_T
        node_T = node_T.next
    new_node.next = node_T     ### 새로 추가 된 node_C 를 node_D 에 링크
    node_P.next = new_node     ### node_B 를 node_C 에 링크
    new_node.prev = node_P     ### node_C 의 prev 를 node_B 에 링크
    node_T.prev = new_node     ### node_D 의 prev 를 node_C 에 링크

def print_list() :
    global node_A
    node = node_A
    while node :
        print(node.data)
        node = node.next
    print
```

- 출력 : C 가 추가 되었다.
```
print("연결 리스트 초기화")
init_list()
print_list()
print("노드 C의 추가 후")
insert_node("C")
print_list()
================================
연결 리스트 초기화
A
B
D
E
노드 C의 추가 후
A
B
C
D
E
```

### 삭제 알고리즘
```
def delete_node(del_data) :
    global node_A
    pre_node = node_A
    next_node = pre_node.next
    next_next_node = next_node.next
    
    ### 삭제할 데이터가 A 인 경우 실행
    if pre_node.data == del_data :
        node_A = next_node
        del pre_node
        return
    
    ### 삭제할 데이터가 A 가 아닌 경우 실행
    while next_node :
        if next_node.data == del_data :
            next_next_node = next_node.next
            pre_node.next = next_node.next
            next_next_node.prev = next_node.prev
            del next_node
            break
        pre_node = next_node                   ### pre_node 는 node_B
        next_node = next_node.next             ### noext_node = node_C 가 되며 while 문 다시 실행.
```

- 출력 : D 가 삭제 되었다.
```
print("연결 리스트 초기화")
init_list()
print_list()
print("노드 C의 추가 후")
insert_node("C")
print_list()
print("노드 D의 삭제 후")
delete_node("D")
print_list()
================================
연결 리스트 초기화
A
B
D
E
노드 C의 추가 후
A
B
C
D
E
노드 D의 삭제 후
A
B
C
E
```
