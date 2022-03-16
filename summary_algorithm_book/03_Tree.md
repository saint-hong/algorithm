# 1. Tree
## 1) Tree 구조란 ?
- 트리 구조는 프로그래밍 언어와 상관없이 가장 많이 쓰이는 자료구조이다.
- 트리는 노드와 링크를 이용한 자료구조이다. (연결리스트와 다르다.)
- 일상 생활에서도 트리 구조를 찾아볼 수 있다.
     - 가족의 족보, 회사의 조직도 등
     - Tree 구조를 "족보 알고리즘" 이라고 기억하면 좋다.
- 구성 :
     - 노드와 노드들을 연결하는 링크로 구성되어 있다.
- 루트 노드가 반드시 존재한다.
- 부모 노드는 반드시 하나만 존재해야 한다.
- 루트 노드를 제외한 나머지 노드들은 여러개의 그룹으로 나눌 수 있으며, 그 그룹도 하나의 트리가 된다.

## 2) Tree 구조의 용어들
- root : 가장 상위의 노드
- parent node : 부모 노드 : 자신 보다 상위에 있는 노드
- child node : 자식 노드 : 자신 보다 하위에 있는 노드
- leaf node : 리프 노드 : 최하위의 노드
- sibling node : 형제 노드 : 같은 부모 노드를 갖는 노드들
- level : 루트 노드에서 특정 노드까지 찾아가는 데 거치는 총 노드의 수
- height : 트리 구조에서 가장 큰 레벨. 즉 루트 노드에서 리프 노드까지의 노드 수
- hepth : 경로의 길이
- 차수 : 서브 트리의 갯수. 그룹화한 노드들의 갯수
- 이진트리 : 차수가 2개 이하인 트리 구조

## 3) 이진트리의 종류
- 이진트리는 자식 노드가 2개만 존재한다. 서브 트리가 2개 이하여야 한다.
- 구현이 간단한 장점이 있다.
- full binary tree : 정 이진 트리
- perfect binary tree : 포화 이진 트리
- complete binary tree : 완전 이진 트리
- balancde binary tree : 균형 이진 트리
- degenerate tree : 변질 트리

# 2. 트리의 순회(Traverse) 알고리즘
## 1) 순회 알고리즘이란 ?
- 트리구조는 다른 자료구조보다 자료를 저장하거나 검색하는 방법이 간단한 장점이 있다. (메모리의 효율적 활용)
- 트리구조 내의 순회는 "각 노드들을 한번씩만 방문하여 전체 노드들을 거치는 것"을 말한다.
- 이진 트리에서 각 노드들을 순회하는 방법을 알고리즘으로 구현해 보자.

## 2) 종류
- pre-order traverse : 전위 순회 : 루트 노드를 시작으로 왼쪽의 노드들을 방문한뒤 오른쪽의 노드들을 방문하는 방식
     - A -> B -> D -> E -> C -> F -> E
- in-order traverse : 중위 순회 : 왼쪽 자식 노드를 방문하고 부모 노드를 방문한 후 다시 오르쪽 자식 노드를 방문하는 방식
     - D -> B -> E -> A -> F -> C -> G (왼쪽 서브 트리 -> 루트 노드 -> 오른쪽 서브 트리)
- post-order traverse : 후위 순회 : 왼쪽 자식 노드 방문, 오른쪽 자식 노드 방문, 마지막에 부모 노드 방문하는 방식
     - D -> E -> B -> F -> G -> C -> A
- level-order traverse : 루트 노드부터 레벨의 순서대로 방문하는 방식
     - A -> B -> C -> D -> E -> F -> G

## 3) 순회 알고리즘
- 전위 순회, 중위 순회, 후위 순회 알고리즘은 stack 구조로 만들고, 단계순위 순회 알고리즘은 Queue 구조로 만든다.
- 함수내에서 함수를 다시 호출하는 재귀호출 방식으로 간편하게 만들 수 있다.
- 그러나 코드의 실행과정은 간단하지만은 않다.

```
# 트리에서 사용할 노드 (Node) 클래스의 선언
class Node :
    def __init__(self, data) :
        self.data = data
        self.left = None   ### 부모 노드의 왼쪽 방향
        self.right = None  ### 부모 노드의 오른쪽 방향

root = Nonea

# 트리의 초기화
def init_tree() :
    global root
    new_node = Node("A")
    root = new_node          ### node_A 가 Tree의 루트 노드이다. (시작점)
    new_node = Node("B")
    root.left = new_node     ### node_B 는 node_A 의 왼쪽 자식 노드
    new_node = Node("C")
    root.right = new_node    ### node_C 는 node_A 의 오른쪽 자식 노드
    new_node_1 = Node("D")
    new_node_2 = Node("E")
    node = root.left         ### node_B 가 부모 노드가 된다.
    node.left = new_node_1   ### node_D 는 node_B 의 왼쪽 자식 노드
    node.right = new_node_2  ### node_E 는 node_B 의 오른쪽 자식 노드

    new_node_1 = Node("F")
    new_node_2 = Node("G")
    node = root.right        ### node_C 가 부모 노드가 된다.
    node.left = new_node_1   ### node_F 는 node_C 의 왼쪽 자식 노드
    node.right = new_node_2  ### node_G 는 node_C 의 오른쪽 자식 노드
```
### 전위 순회 알고리즘
- 구조
```
if 문
print(현재 노드)
재귀호출(왼쪽 노드)
재구호출(오른쪽 노드)
```

```
def preorder_traverse(node) :
    if node == None : return       ### 노드가 트리의 끝 인지 아닌지 체크, 끝이 아니라면 아래 코드 실행
    print(node.data, end=' -> ')   ### 현재 노드의 데이터 출력, 여기에서 노드는 부모 노드.
    preorder_traverse(node.left)   ### 재귀 호출 : 부모 노드의 왼쪽 자식 노드
    preorder_traverse(node.right)  ### 재귀 호출 : 부모 노드의 오른쪽 자식 노드
```
### 중위 순회 알고리즘¶
- 구조
```
if 문
재귀호출(왼쪽 노드)
print(현재 노드)
재구호출(오른쪽 노드)
```

```
def inorder_traverse(node) :
    if node == None : return
    inorder_traverse(node.left)
    print(node.data, end=' -> ')
    inorder_traverse(node.right)
```

### 후위 순회 알고리즘
- 구조
```
if 문
재귀호출(왼쪽 노드)
재구호출(오른쪽 노드)
print(현재 노드)
```
```
def postorder_traverse(node) :
    if node == None : return
    postorder_traverse(node.left)
    postorder_traverse(node.right)
    print(node.data, end=' -> ')
```
### 단계순위 순회 알고리즘
- Queue 자료 구조 방식으로 되어 있다. (FIFO : 먼저 들어간 것이 먼저 나온다)
- 트리의 제일 위에서부터 아래 노드까지 단계별로 순회하는 거라서 간단해 보이지만 오히려 다른 순회 알고리즘 보다 좀더 복잡하다.
- 구조
```
while 문
levelq 리스트에 노드 저장
visit_node 변수선언
print(visi_node)
자식 노드 꺼내기
visit_node 의 왼쪽 노드 저장
visit_node 의 오른쪽 노드 저장
```

```
levelq = []

def levelorder_traverse(node) :
    global levelq
    levelq.append(node)
    while len(levelq) != 0 :
        ## visit
        visit_node = levelq.pop(0)
        print(visit_node.data, end=' -> ')
        ## child put
        if visit_node.left != None :
            levelq.append(visit_node.left)   ### 노드 A 의 왼쪽 노드인 노드 B가 levelq 에 저장된다.
        if visit_node.right != None :        
            levelq.append(visit_node.right)  ### 노드 A 의 오른쪽 노드인 노드 C가 levelq 에 저장된다. [B, C] 가 다시 while 문에서 실행.
```

### 순회 알고리즘 출력
```
init_tree()
print("<Preorder Traverse>")
preorder_traverse(root)
print("\n")
print("<Inorder Traverse>")
inorder_traverse(root)
print("\n")
print("Postorder Traverse")
postorder_traverse(root)
print("\n")
print("<Levelorder Traverse>")
levelorder_traverse(root)
print("\n")
================================
<Preorder Traverse>
A -> B -> D -> E -> C -> F -> G 

<Inorder Traverse>
D -> B -> E -> A -> F -> C -> G 

Postorder Traverse
D -> E -> B -> F -> G -> C -> A 

<Levelorder Traverse>
A -> B -> C -> D -> E -> F -> G 
```
