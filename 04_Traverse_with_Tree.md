# 1. Traverse : 순회
## 1) 순회 란?
- Tree 구조의 각 노드를 한 번씩만 거쳐서 모든 경로의 노드를 방문하는 것을 의미한다.
- 규칙 : 각 노드는 한 번만 방문한다.

## 2) 순회 알고리즘의 종류
- pre-order traverse : 전위 순회 알고리즘
	- 부모 노드에서 왼쪽 자식 노드 -> 오른쪽 자식 노드 순으로 방문한다.
	- 루트 노드 -> 왼쪽 서브트리(왼쪽 -> 오른쪽) -> 오른쪽 서브트리(왼쪽 -> 오른쪽)
	```
	A -> B -> D -> E -> C-> F -> G
	```
- in-order traverse : 중위 순회 알고리즘
	- 왼쪽 자식 노드에서 시작하여 부모 노드를 방문한 뒤 오른쪽 자식 노드를 방문한다.
	- 왼쪽 서브트리(왼쪽->부모->오른쪽) -> 루트노드 -> 오른쪽 서브트리(왼쪽->부모->오른쪽)
	```
	D -> B -> E -> A -> F -> C -> G
	```
- post-order traverse : 후위 순회 알고리즘
	- 왼쪽 자식 노드에서 시작하여 오른쪽 자식 노드를 방문한 뒤 부모 노드를 방문한다.
	- 왼쪽 서브트리(왼쪽->오른쪽->부모)->오른쪽 서브트리(왼쪽->오른쪽->부모)->루트노드
	```
	D -> E -> B -> F -> G -> C -> A
	```
- level-order traverse : 단계순위 순회 알고리즘
	- Tree 의 상위 레벨에서 하위 레벨로 이동하면서 각 레벨의 노드를 왼쪽부터 방문한다.
	- 루트노드 -> 자식노드(왼쪽->오른쪽) -> 자식노드(왼쪽->오른쪽)
	```
	A -> B -> C -> D -> E -> F -> G
	```
## 3) 순회 알고리즘 구현
```
### 순회 알고리즘 생성
class Node :
    def __init__(self, data) :
        self.data = data
        self.left = None
        self.right = None

root = None
def init_traverse() :
    global root
    new_node = Node("A")          ### 노드A 생성
    root = new_node               ### 노드A 를 루트 노드로 저장
    new_node = Node("B")          ### 노드B 생성
    root.left = new_node          ### 노드B 를 루트 노드의 왼쪽 노드로 저장
    new_node = Node("C")          ### 노드C 생성
    root.right = new_node         ### 노드C 를 루트 노드의 오른쪽 노드로 저장
    new_node_1 = Node("D")        ### 노드D 와 노드E 생성
    new_node_2 = Node("E")
    node = root.left              ### node 변수를 노드B 로 저장
    node.left = new_node_1        ### 노드D 를 노드B 의 왼쪽 자식 노드로 저장
    node.right = new_node_2       ### 노드C 를 노드B의 오른쪽 자식 노드로 저장

    new_node_1 = Node("F")        ### 노드F 와 노드G 를 생성
    new_node_2 = Node("G")
    node = root.right             ### node 변수를 노드C 로 저장
    node.left = new_node_1        ### nodeF 를 노드C 의 왼쪽 자식 노드로 저장
    node.right = new_node_2       ### nodeG 를 노드C 의 오른쪽 자식 노드로 저장
```

### 전위 순회 알고리즘 구현¶
- 함수 내부에서 재귀 호출을 사용한다.
- if node = None : return 은 현재 노드가 트리의 끝인지 아닌지를 체크 한다.
- True 이면 return 으로 함수를 반환한다.
- False 면 코드가 실행되어, 왼쪽 노드 -> 오른쪽 노드를 방문한다.

```
def preorder_traverse(node) :
    if node == None : return
    print(node.data, end=' -> ')
    preorder_traverse(node.left)
    preorder_traverse(node.right)
```

### 중위 순회 알고리즘 구현
- 함수 내부에서 재귀 호출을 사용한다.
- 노드가 트리의 끝이 아니면 왼쪽 자식 노드 -> 부모 노드 -> 오른쪽 자식 노드 순으로 방문한다.

```
def inorder_traverse(node) :
    if node == None : return
    inorder_traverse(node.left)
    print(node.data, end=' -> ')
    inorder_traverse(node.right)
```

### 후위 순회 알고리즘 구현¶
- 함수 내부에서 재귀 호출을 사용한다.
- 노드가 트리의 끝이 아니면 왼쪽 자식 노드 -> 오른쪽 자식 노드 -> 부모 노드 순으로 방문한다.

```
def postorder_traverse(node) :
    if node == None : return
    postorder_traverse(node.left)
    postorder_traverse(node.right)
    print(node.data, end=' -> ')
```

### 단계순위 순회 알고리즘 구현
- 전위, 중위, 후위 순회 알고리즘은 stack 자료구조 방식으로 함수 내부에서 재귀 호출을 사용하여 노드를 출력하였다.
- 단계순위 순회 알고리즘은 queue 자료구조 방식으로 구현한다. append 와 pop 매서드를 사용하여 먼저 들어간 데이터를 먼저 꺼내는 방식

```
### levelq 변수를 리스트로 저장
levelq = []

def levelorder_traverse(node) :
    global levelq                           ## levelq 변수 가져오기
    levelq.append(node)                     ## 현재 노드를 levelq에 저장
    while len(levelq) != 0 :                ## levelq 가 비어있는지 아닌지 체크
        visit_node = levelq.pop(0)          ## 비어있지 않으면, 현재 노드를 먼저 방문
        print(visit_node.data, end=' -> ')  ## 현재 노드 출력
        if visit_node.left != None :        ## 현재 노드의 왼쪽 자식 노드 여부 확인
            levelq.append(visit_node.left)  ## 왼쪽 자식노드를 levelq 에 저장
        if visit_node.right != None :       ## 현재 노드의 오른쪽 자식 노드 여부 확인
            levelq.append(visit_node.right) ## 오른쪽 자식노드를 levelq 에 저장
```

### 출력

```
print("순회 알고리즘 초기화")
init_traverse()
print("<preorder_traverse>")
preorder_traverse(root)
print("\n")
print("<inorder_traverse>")
inorder_traverse(root)
print("\n")
print("<postorder_traverse>")
postorder_traverse(root)
print("\n")
print("<levelorder_traverse>")
levelorder_traverse(root)
==============================================
순회 알고리즘 초기화
<preorder_traverse>
A -> B -> D -> E -> C -> F -> G

<inorder_traverse>
D -> B -> E -> A -> F -> C -> G

<postorder_traverse>
D -> E -> B -> F -> G -> C -> A

<levelorder_traverse>
A -> B -> C -> D -> E -> F -> G
```
