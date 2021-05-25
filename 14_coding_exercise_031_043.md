# 031. 제곱근 구하기

### 1) 접근풀이 및 조건
- 부동소수점 형태의 결과를 출력하는 제곱근을 구하는 알고리즘은 오래전부터 개발되어왔음.
- 제곱근 구하는 방법 : 개평법, 바빌로니아법
- 주로 바빌로니아법을 사용함
- 조건 :
    - 정수값을 찾는 방법 : n에서 1,3,5,7... 홀수를 빼고 다시 n에 저장했을 때 0이 되면 뺀 횟수가 n의 제곱근이 된다. 
    
```
n = n - (2*1+1)
```

### 1)-1 바빌로니아법 
- 임의의 수의 제곱근에 빠르게 수렵하는 수열을 만들어 근사값을 찾는 방법
- 임의의 자연수 N에 대한 제곱근을 찾는다고 하면 다음과 같은 식이 성립한다. 
    - $\sqrt{N}=x_{n} + \epsilon, \;\; \epsilon > 0$
    - $N={\sqrt{N}}^2={(x_{n}+\epsilon)}^2={x_{n}}^2+2x_{n}\epsilon+{\epsilon}^2$
- 오차가 작으면 오자의 제곱은 더 작아지므로 그 값을 무시하면,
    - $N \approx {x_{n}}^2 + 2x_{n}\epsilon, \;\; \epsilon \approx \dfrac{N-{x_{n}}^2}{2x_{n}}$
- 근사오차값을 이용하여 x_n 보다 더 근사된 값을 나타낼 수 있다.
    - $x_{n+1}=x_{n}+\epsilon=x_{n}+\dfrac{N-{x_{n}}^2}{2x_{n}}=\dfrac{1}{2} \cdot (x_{n} + \dfrac{N}{x_{n}})$
- 이러한 수식을 이용하여 임의의 수 N에 대한 제곱근을 구하는 방식은 다음과 같다.
    - 제곱해서 N 보다 작지만 가장 가까운 수 x0를 구한다.
    - 그 다음 근사값인 x1 을 구한다. $x_{n+1}=\dfrac{1}{2} \cdot (x_{n} + \dfrac{N}{x_{n}})$
    - 원하는 근사값이 나올때까지 반복한다.
- 뉴턴-랩슨의 절편을 구하는 방식도 결과적으로 바빌로니아법과 비슷하다.

### 2) 코드
- 정수값 찾기 : n에서 홀수 1,3,5,7,... 을 차례대로 빼면서 그 값을 n에 다시 저장할때 n이 0이 될때 홀수를 뺀 횟수가 n의 제곱근이 된다.

```
def solve(n) :
    i = 0
    while n >= 0 :
        print(n)
        n = n - (2 * i + 1)
        i += 1

    return i - 1

solve(16)

=====<print>=====

16
15
12
7
0

4
```

#### 바빌로니아법
- 임의의 수의 제곱근에 수렴하는 수열을 만들어 근사값을 찾는 방법
- <$x_{n+1} = \dfrac{1}{2}\cdot(x_{n}+\dfrac{a}{x_{n}})=\dfrac{{x_{n}}^2+a}{2x_{n}}$>

```
def solve_babil(n) :
    a = [0] * 11

    # 배열 a를 0으로 채운다
    i = 1
    while i <= n :
        a[i] = 0
        i += 1

    # i = 1,2,3,4,5,... / j = 1,2,3,4,5,... / j + i = 1,2,3,4,5... / 2,4,6,8,10,.... / 3,6,9,...
    # j 변수가 i 와 같고 두번째 while 문에서 j에 j+i 를 누적 저장하기 때문에 곱셉식 처럼 증가한다.
    # 이러한 j의 변화에 따라서 배열 a의 j번째 인덱스 값이 1 또는 0으로 조정된다.
    i = 1
    while i <= n :
        j = i
        print("======================================")
        while j <= n :
            print(j, end=" : ")
            a[j] = 1 - a[j]
            print(a)
            j = j + i
        i += 1

    # cnt 변수는 배열 a에서 1의 횟수와 같다.
    cnt = 0
    i = 1
    while i <= n :
        if a[i] == 1:
            cnt = cnt + 1
        i += 1

    return cnt
```
```
solve_babil(10)

=====<print>=====

======================================
1 : [0, 1, 0, 0, 0, 0, 0, 0, 0, 0, 0]
2 : [0, 1, 1, 0, 0, 0, 0, 0, 0, 0, 0]
3 : [0, 1, 1, 1, 0, 0, 0, 0, 0, 0, 0]
4 : [0, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0]
5 : [0, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0]
6 : [0, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0]
7 : [0, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0]
8 : [0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0]
9 : [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0]
10 : [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
======================================
2 : [0, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1]
4 : [0, 1, 0, 1, 0, 1, 1, 1, 1, 1, 1]
6 : [0, 1, 0, 1, 0, 1, 0, 1, 1, 1, 1]
8 : [0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 1]
10 : [0, 1, 0, 1, 0, 1, 0, 1, 0, 1, 0]
======================================
3 : [0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0]
6 : [0, 1, 0, 0, 0, 1, 1, 1, 0, 1, 0]
9 : [0, 1, 0, 0, 0, 1, 1, 1, 0, 0, 0]
======================================
4 : [0, 1, 0, 0, 1, 1, 1, 1, 0, 0, 0]
8 : [0, 1, 0, 0, 1, 1, 1, 1, 1, 0, 0]
======================================
5 : [0, 1, 0, 0, 1, 0, 1, 1, 1, 0, 0]
10 : [0, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1]
======================================
6 : [0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 1]
======================================
7 : [0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1]
======================================
8 : [0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1]
======================================
9 : [0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 1]
======================================
10 : [0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0]

3
```

# 032. 알파벳 순서대로 하나씩 줄여가며 출력하기 (반복문 사용)

### 1) 접근풀이 및 조건
- 알파벳 A~Z 까지를 출력하되, 뒤에서부터 하나씩 줄여가면서 출력
- 마지막에는 A 만 출력된다.
- 문자를 아스키 코드로 출력해주는 함수를 사용하면 간단해진다.
    - ord('A') = 65
    - chr(65) = 'A'
- 조건 : 
    - A~Z 까지에 해당하는 26행을 반복하여 출력한다.
    - 각 행마다 알파벳 하나씩 줄여서 출력한다.

### 2) 코드

#### 문자를 아스키코드로 변환 시켜주는 함수 : ord()

```
ord('a'), ord('A'), type(ord('A')), ord('ㄱ')

=====<print>=====

(97, 65, int, 12593)
```

#### 아스키코드를 문자로 변환 시켜주는 함수 : chr()

```
chr(12593), chr(65), chr(97)

=====<print>=====

('ㄱ', 'A', 'a')
```

#### 파이썬에 내장 된 아스키코드를 출력
- 랜덤한 숫자를 만들고 이 숫자들에 해당하는 문자를 확인

```
import random
n = [random.randint(10000, 10500) for _ in range(10)]
n

=====<print>=====

[10001, 10237, 10289, 10440, 10150, 10221, 10284, 10473, 10012, 10266]
```
```
for i in n :
    print("{} : {}".format(chr(i), ord(chr(i))))

=====<print>=====

✑ : 10001
⟽ : 10237
⠱ : 10289
⣈ : 10440
➦ : 10150
⟭ : 10221
⠬ : 10284
⣩ : 10473
✜ : 10012
⠚ : 10266
```

#### 1~1000에 해당하는 문자는 어떤 것이 있는지 확인
- 다양한 문자, 기호, 특수기호 들이 저장 되어 있다.
- 아스키코드 입력 시 syntax error 발생함

```
for i in range(1000) :
    if i % 100 == 0 :
        print("\n")
        print("{0}--- {1} ~ {2} ---{3}".format(chr(1),i, i+100,chr(2)))
    print(chr(i), end=" ")

=====<print>=====
```

#### A 의 아스키코드 확인

```
a = ord('A')
a

=====<print>=====

65
```

#### 알파벳 갯수 만큼 각 행을 출력해주는 반복문

```
a = ord('A')
count = 0

while a <= ord('Z') :
    count += 1
    print(a, chr(a), end=" ")
    a += 1

print("\n")
print(count)

=====<print>=====

65 A 66 B 67 C 68 D 69 E 70 F 71 G 72 H 73 I 74 J 75 K 76 L 77 M 78 N 79 O 80 P 81 Q 82 R 83 S 84 T 85 U 86 V 87 W 88 X 89 Y 90 Z

26
```
#### 변수 a의 증가에 따라서 b는 적어지는 반복문
- 마지막 Z의 아스키 코드에서부터 1씩 작아지게 된다.

```
b = ord('A')
while b <= ord('Z') - (70 - ord('A')) :
    print(b, end=" ")
    b += 1

=====<print>=====

65 66 67 68 69 70 71 72 73 74 75 76 77 78 79 80 81 82 83 84 85
```

### 3) 최종코드

```
def f() :
    a = ord('A')
    while a <= ord('Z') :
        b = ord('A')
        while b <= (ord('Z') - (a - ord('A'))) :     ### a가 1씩 증가하므로 a-ord('A') 는 1,2,3,4,5,... 가 된다.
            print("{}".format(chr(b)), end=" ")
            b += 1
        print()
        a += 1

if __name__ == "__main__" :
    f()

=====<print>=====

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
A B C D E F G H I J K L M N O P Q R S T U V W X Y
A B C D E F G H I J K L M N O P Q R S T U V W X
A B C D E F G H I J K L M N O P Q R S T U V W
A B C D E F G H I J K L M N O P Q R S T U V
A B C D E F G H I J K L M N O P Q R S T U
A B C D E F G H I J K L M N O P Q R S T
A B C D E F G H I J K L M N O P Q R S
A B C D E F G H I J K L M N O P Q R
A B C D E F G H I J K L M N O P Q
A B C D E F G H I J K L M N O P
A B C D E F G H I J K L M N O
A B C D E F G H I J K L M N
A B C D E F G H I J K L M
A B C D E F G H I J K L
A B C D E F G H I J K
A B C D E F G H I J
A B C D E F G H I
A B C D E F G H
A B C D E F G
A B C D E F
A B C D E
A B C D
A B C
A B
A
```
#### 역으로 출력하는 코드
- 두번째 반복문의 제어문에서 b의 범위를 하나씩 증가시켜 주도록 바꾼다.

```
def solve() :
    a = ord('A')

    while a <= ord('Z') :
        b = ord('A')
        while b <= ord('A') + (a - (ord('A'))) :
            print(chr(b), end=" ")
            b += 1

        print()
        a += 1

if __name__ == "__main__" :
    solve()

=====<print>=====

A 
A B 
A B C 
A B C D 
A B C D E 
A B C D E F 
A B C D E F G 
A B C D E F G H 
A B C D E F G H I 
A B C D E F G H I J 
A B C D E F G H I J K 
A B C D E F G H I J K L 
A B C D E F G H I J K L M 
A B C D E F G H I J K L M N 
A B C D E F G H I J K L M N O 
A B C D E F G H I J K L M N O P 
A B C D E F G H I J K L M N O P Q 
A B C D E F G H I J K L M N O P Q R 
A B C D E F G H I J K L M N O P Q R S 
A B C D E F G H I J K L M N O P Q R S T 
A B C D E F G H I J K L M N O P Q R S T U 
A B C D E F G H I J K L M N O P Q R S T U V 
A B C D E F G H I J K L M N O P Q R S T U V W 
A B C D E F G H I J K L M N O P Q R S T U V W X 
A B C D E F G H I J K L M N O P Q R S T U V W X Y 
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
```

# 033. 알파벳 순서대로 하나씩 줄여가며 출력하기 (재귀 호출 사용)

### 1) 접근풀이 및 조건
- A~Z 까지 출력하는 반복문은 유지하고, 출력범위를 정하는 반복문을 재귀호출로 사용
- 재귀호출의 제어문은 파라미터의 범위를 설정해 주면 된다.
    - if end < 'A' or end > 'Z' : 파라미터 값이 A와 Z의 범위를 넘어서면 재귀호출을 멈춘다.

### 2) 코드

```
def print_alphabet(end) :
    if end < 'A' or 'Z' < end :
        return -1

    c = ord('A')
    while c <= ord(end) :
        print(chr(c), end=" ")
        c += 1

    print()
    next = ord(end) - 1

    return print_alphabet(chr(next))

    #return print_alphabet(chr(ord(end)-1))

print_alphabet('Z')

=====<print>=====

A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 
A B C D E F G H I J K L M N O P Q R S T U V W X Y 
A B C D E F G H I J K L M N O P Q R S T U V W X 
A B C D E F G H I J K L M N O P Q R S T U V W 
A B C D E F G H I J K L M N O P Q R S T U V 
A B C D E F G H I J K L M N O P Q R S T U 
A B C D E F G H I J K L M N O P Q R S T 
A B C D E F G H I J K L M N O P Q R S 
A B C D E F G H I J K L M N O P Q R 
A B C D E F G H I J K L M N O P Q 
A B C D E F G H I J K L M N O P 
A B C D E F G H I J K L M N O 
A B C D E F G H I J K L M N 
A B C D E F G H I J K L M 
A B C D E F G H I J K L 
A B C D E F G H I J K 
A B C D E F G H I J 
A B C D E F G H I 
A B C D E F G H 
A B C D E F G 
A B C D E F 
A B C D E 
A B C D 
A B C 
A B 
A 

-1
```

#### 역으로 출력하는 코드
- next 의 수식을 + 1로 하고 아규먼트를 A로 입력하면 된다.

```
def f(end) :
    if end < 'A' or end > 'Z' :
        return -1
    
    c = ord('A')
    while c <= ord(end) :
        print(chr(c), end=" ")
        c += 1
        
    print()
    next = ord(end) + 1
    
    return f(chr(next))

f('A')

=====<print>=====

A
A B
A B C
A B C D
A B C D E
A B C D E F
A B C D E F G
A B C D E F G H
A B C D E F G H I
A B C D E F G H I J
A B C D E F G H I J K
A B C D E F G H I J K L
A B C D E F G H I J K L M
A B C D E F G H I J K L M N
A B C D E F G H I J K L M N O
A B C D E F G H I J K L M N O P
A B C D E F G H I J K L M N O P Q
A B C D E F G H I J K L M N O P Q R
A B C D E F G H I J K L M N O P Q R S
A B C D E F G H I J K L M N O P Q R S T
A B C D E F G H I J K L M N O P Q R S T U
A B C D E F G H I J K L M N O P Q R S T U V
A B C D E F G H I J K L M N O P Q R S T U V W
A B C D E F G H I J K L M N O P Q R S T U V W X
A B C D E F G H I J K L M N O P Q R S T U V W X Y
A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

-1
```
# 034. 3X3 행렬 중 합이 최소가 되는 항목 선택하기

### 1) 접근풀이 및 조건
- 3x3 크기의 행렬에서 각 행에서 열이 중복되지 않게 선택한 후 3개의 숫자의 최소합을 구하기
    - 1행에서 1열을 선택했으면, 2행에서는 2, 3열을 선택해야하고, 2열을 선택한 경우 3행에서는 3열을 선택해야한다.
- 조건 :
    - 파이썬의 최대값 상수를 사용한다
    - 백트래킹 backtracking 기반의 재귀 함수를 사용한다 : 이전단계로 돌아가서 다른 경우를 따지는 방법
    - 한번 선택한 항목을 다시 선택하지 않도록하기 위해 플래그 배열을 사용한다.

### 2) 코드

#### 조건 1 : 파이썬의 최대값 상수를 사용한다.
- sys 모듈에 파이썬에서 제공하는 상수의 최대값값과 최소값을 확인할 수 있다.

```
import sys

max = sys.maxsize
min = -sys.maxsize -1

max

=====<print>=====

9223372036854775807

min

=====<print>=====

-9223372036854775808
```

#### 조건 2 : 백트래킹 기반의 함수 이용
- 간단하지만 실제 실행되는 과정은 복잡함, 책에 자세한 설명이 없음
- 재귀호출을 통해서 현재 경로의 시작점으로 돌아가 다른 경우의 수를 탐색하는 방식

```
matrix = [
    [1,2,3],
    [4,5,6],
    [7,8,9] ]

def f(row, score) :
    for i in range(3) :
        f(row+1, score + matrix[row][i])
```
#### 조건 3 : 한번 선택한항목을 다시 선택하지 않도록 하기 위해 별도의 플래그 배열을 사용
- checked 변수에 False 로 채워진 리스트를 저장한다. 
- i 번째 인덱스의 값이 False 이면 이것을 True 로 바꾼다. 즉 i 번째 행은 사용했다는 의미가 된다.
- 재귀호출 이후 다시 i번째 인덱스의 값을 False로 바꾼다. 즉 재귀호출을 빠져나오면 다시 사용할 수 있다는 의미.

```
def f(row, score) :

    checked = [False, False, False]

    for i in range(3) :
        if checked[i] == False :
            checked[i] = True
            f(row+1, score + matrix[row][i])
            checked[i] = False
```

### 3) 최종코드
- 조건에 따라서 배열의 각 위치마다 데이터를 선택 후 덧셈을 한다. 
- 덧셈 결과를 min_sol 값에 저장 후 매번 비교하여 작은 것을 저장한다.
- 코드 실행 과정 복잡함.

```
INT_MAX = 10000

m = [
    [1,5,3],
    [2,5,7],
    [5,3,5]
]

col_check = [False, False, False]
min_sol = INT_MAX

def f(row, score) :
    global min_sol

    # 0,1,2 행을 돌면서 합산한 값을 score 파라미터에 넣어 호출한 뒤 min_sol 값과 비교하여 작은 수를 min_sol 값에 저장 후 반환한다.
    if row == 3 :
        if score < min_sol :
            min_sol = score
        return min_sol

    # 열이 중복 선택되지 않도록 False와 True 값을 변환하면서 합한 값을 score 파라미터로 재귀호출한다.
    # 0행 0열 - 1행 1열 - 2행 2열 후 다시 1행 2열 - 2행 1열을 선택한다. 모든 경우의 수를 돌면서 score 값을 파라미터로 호출한다.
    for i in range(3) :
        if col_check[i] == False :
            col_check[i] = True

            f(row+1, score + m[row][i])

            col_check[i] = False

    return min_sol

f(0,0)

=====<print>=====

8
```
#### 코트 실행 과정에서 행과 열의 선택만 일부 확인
- 각 행의 열별로 선택하는 것을 대략 확인 할 수 있다.

```
함수 호출 0행
재귀 호출전 0행, 0열
함수 호출 1행
재귀 호출전 1행, 1열
함수 호출 2행
재귀 호출전 2행, 2열
함수 호출 3행
===재귀 전후 구분====
재귀 호출 후 2행, 2열
재귀 호출후 2 열은 False 가 됨
===재귀 전후 구분====
재귀 호출 후 1행, 1열
재귀 호출후 1 열은 False 가 됨
재귀 호출전 1행, 2열
함수 호출 2행
재귀 호출전 2행, 1열
함수 호출 3행
===재귀 전후 구분====
재귀 호출 후 2행, 1열
재귀 호출후 2 열은 False 가 됨
===재귀 전후 구분====
재귀 호출 후 1행, 2열
재귀 호출후 1 열은 False 가 됨
===재귀 전후 구분====
재귀 호출 후 0행, 0열
재귀 호출후 0 열은 False 가 됨
```
- 이 과정이 for i in range(3) 에서의 i = 0 에 해당함. 이후 이 과정이 반복된다.

# 035. 회문 확인하기

### 1) 접근풀이 및 조건
- 회문 palindrome : 순서가 거꾸로 되도 같은 문장이나 낱말
    - 토마토, level 등
- 어떤 단어나 문장이  회문인지 아닌지를 확인
- 조건 :
    - 주어진 문자열의 처음과 끝의 문자를 비교하고 같으면 다음 문자를 비교하며, 아니면 비교를 끝낸다.
    - 주어진 문자열의 중간까지만 비교한다.

### 2) 코드

```
def solve(word) :

    i = 0

    while i < (len(word) / 2) :

        if word[i] != word[len(word) - i - 1] :
            return print("회문이 아닙니다 {} != {}".format(word[i], word[len(word)-i-1]))

        else :
            return print("회문 입니다.")

        i += 1

solve("tomato")

=====<print>=====

회문이 아닙니다 t != o
```
#### 책의 이 코드는 어떤 의미인지 알기 어려움
- 문자열의 각 데이터를 다른 모든 데이터와 비교하는 코드, 그런데 앞에서 회문은 앞과 뒤가 같은 문자열이라고 했는데 왜 모든 문자를 서로 비교하는지 의미를 모르겠음.

```
#str = "mississippi"
str = "ttot"
length = len(str)

def f() :
    p = 0
    c = 0

    for i in range(length) :
        j = i + 1

        while j < length :
            p = j - i + 1
            k = 0
            print("p = {}".format(p))
            while i + k < j - k :
                if str[i+k] != str[j-k] :
                    p = 0
                    print("break")
                    break
                k = k + 1
            c = c + p
            print("c = {}".format(c))
            j = j + 1

    print("회문의 갯수 : {}".format(c))
```

# 036. 만들 수 있는 삼각형의 개수 구하기

### 1) 접근풀이 및 조건
- 주어진 정수 n 안에서 만들 수 있는 삼각형의 갯수 구하기
- 삼각형의 조건 :
    - a + b + c = n
    - a + b > c : 두 변의 길이의 합은 나머지 변의 길이보다 크다.
- 조건 :
    - a, b, b의 가능한 모든 조합을 탐색하므로 전체탐색을 한다. a, b, c 를 각각 1부터 n까지 증가시키므로 반복문 3개
    - 삼각형 조건을 만족해야 한다. a <= b , b <= c 이면 a+b > c
- a, b, c 의 모든 조합을 탐색하기 위해서 반복문을 3개 사용. 각 변수를 어떤 초기값으로 설정하느냐에 따라서 탐색의 횟수가 달라진다.
    - a=1, b=a, c=b라고 하면 중복되는 조합은 재탐색하지 않게 된다. 이러한 최적화 방법을 "가지치기" 라고 한다.

### 2) 코드

#### 완전탐색 중 가지치기 방식
- 중복된 조합은 탐색하지 않음
- 삼각형의 변의 길이의 합의 관계를 탐색하므로 중복되는 조합은 굳이 탐색할 필요 없다.
- 변수 a = 1, b = a, c = b 로 시작하여 각각 n까지 증가시킬 경우, 중복되는 조합은 탐색에서 빠지게 된다.
    - 1,1,2 = 1,2,1 = 2,1,1 이므로 1,1,2 만 탐색하면 나머지는 탐색하지 않아도 된다.
- 탐색횟수 35

```
count = 0
a = 1

while a <= 5 :
    b = a
    while b <= 5 :
        c = b
        while c <= 5 :
            count += 1
            print("a = {}, b = {}, c = {}".format(a, b, c))
            c += 1

        print("=== b 증가 ===")
        b += 1

    print("=== a 증가 ===")
    a += 1

print("=== 탐색 횟수 = {} ===".format(count))

=====<print>=====

a = 1, b = 1, c = 1
a = 1, b = 1, c = 2
a = 1, b = 1, c = 3
a = 1, b = 1, c = 4
a = 1, b = 1, c = 5
=== b 증가 ===
a = 1, b = 2, c = 2
a = 1, b = 2, c = 3
a = 1, b = 2, c = 4
a = 1, b = 2, c = 5
=== b 증가 ===
a = 1, b = 3, c = 3
a = 1, b = 3, c = 4
a = 1, b = 3, c = 5
=== b 증가 ===
a = 1, b = 4, c = 4
a = 1, b = 4, c = 5
=== b 증가 ===
a = 1, b = 5, c = 5
=== b 증가 ===
=== a 증가 ===
a = 2, b = 2, c = 2
a = 2, b = 2, c = 3
a = 2, b = 2, c = 4
a = 2, b = 2, c = 5
=== b 증가 ===
a = 2, b = 3, c = 3
a = 2, b = 3, c = 4
a = 2, b = 3, c = 5
=== b 증가 ===
a = 2, b = 4, c = 4
a = 2, b = 4, c = 5
=== b 증가 ===
a = 2, b = 5, c = 5
=== b 증가 ===
=== a 증가 ===
a = 3, b = 3, c = 3
a = 3, b = 3, c = 4
a = 3, b = 3, c = 5
=== b 증가 ===
a = 3, b = 4, c = 4
a = 3, b = 4, c = 5
=== b 증가 ===
a = 3, b = 5, c = 5
=== b 증가 ===
=== a 증가 ===
a = 4, b = 4, c = 4
a = 4, b = 4, c = 5
=== b 증가 ===
a = 4, b = 5, c = 5
=== b 증가 ===
=== a 증가 ===
a = 5, b = 5, c = 5
=== b 증가 ===
=== a 증가 ===
=== 탐색 횟수 = 35 ===
```

#### 모든 조합을 다 탐색하는 경우
- 변수 a = 1, b = 1, c = 1 부터 n까지 실행하면 모든 조합을 다 탐색한다. 그러나 한번 탐색한 것까지 재탐색 하므로 비효율적
- 탐색횟수 125

```
count = 0
a = 1

while a <= 3 :
    b = 1

    while b <= 3 :

        c = 1
        while c <= 3 :
            count += 1
            print("a = {}, b = {}, c = {}".format(a, b, c))
            c += 1

        print("=== b 증가 ===")
        b += 1

    print("=== a 증가 ===")
    a += 1

print("=== 탐색 횟수 = {} ===".format(count))

=====<print>=====

a = 1, b = 1, c = 1
a = 1, b = 1, c = 2
a = 1, b = 1, c = 3
=== b 증가 ===
a = 1, b = 2, c = 1
a = 1, b = 2, c = 2
a = 1, b = 2, c = 3
=== b 증가 ===
a = 1, b = 3, c = 1
a = 1, b = 3, c = 2
a = 1, b = 3, c = 3
=== b 증가 ===
=== a 증가 ===
a = 2, b = 1, c = 1
a = 2, b = 1, c = 2
a = 2, b = 1, c = 3
=== b 증가 ===
a = 2, b = 2, c = 1
a = 2, b = 2, c = 2
a = 2, b = 2, c = 3
=== b 증가 ===
a = 2, b = 3, c = 1
a = 2, b = 3, c = 2
a = 2, b = 3, c = 3
=== b 증가 ===
=== a 증가 ===
a = 3, b = 1, c = 1
a = 3, b = 1, c = 2
a = 3, b = 1, c = 3
=== b 증가 ===
a = 3, b = 2, c = 1
a = 3, b = 2, c = 2
a = 3, b = 2, c = 3
=== b 증가 ===
a = 3, b = 3, c = 1
a = 3, b = 3, c = 2
a = 3, b = 3, c = 3
=== b 증가 ===
=== a 증가 ===
=== 탐색 횟수 = 27 ===
```
#### a, b, c가 증가하는 부분을 재귀호출로 만들 수 있다.
- 순서대로 호출하며, 전체탐색에 해당한다.
- 재귀 호출을 빠져나오도록 하는 제어조건을 잘 만들어야 한다.

```
find_triangle(n, a+1, b, c)
find_triangle(n, a, b+1, c)
find_triangle(n, a, b, c+1)
```

### 3) 최종코드

```
cnt = 0
search_count = 0
checked = [[[0 for i in range(21)] for j in range(21)] for k in range(21)]

def solve(n, a, b, c) :
    global cnt, search_count

    search_count += 1

    if a + b + c == n :
        if a <= b and b <= c and a+b > c and checked[a][b][c] == 0 :
            cnt = cnt + 1
            checked[a][b][c] = 1
            print(a,b,c)
        return

    solve(n, a+1, b, c)
    solve(n, a, b+1, c)
    solve(n, a, b, c+1)

    if search_count % 100 == 0 :
        print("★", end=" ")


if __name__ == "__main__" :
    n = 13
    solve(n, 1, 1, 1)
    print("탐색한 횟수 : {}, 만들 수 있는 삼각형의 갯수 : {}".format(search_count, cnt))

=====<print>=====

★ ★ ★ 4 4 5
★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ 3 5 5
★ ★ 3 4 6
★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ 2 5 6
★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ 1 6 6
★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ ★ 탐색한 횟수 : 88573, 만들 수 있는 삼각형의 갯수 : 5
```
# 037. 파스칼의 삼각형

### 1) 접근풀이 및 조건
- 파스칼의 삼각형 : 이항계수를 삼각형 모양의 기하학적 형태로 배열한 것
- 첫번째 줄에 1을 쓰고, 그 다음줄부터는 윗줄의 왼쪽 오른쪽 숫자를 더한 값으로 채운다.
```
      1
     1 1
    1 2 1
   1 3 3 1
  1 4 6 4 1
```
- 이항정리에서 계수들의 값을 계산할 때 사용된다.
    - $(x+1)^2=1 \cdot x^2 + 2 \cdot x + 1$
    - 이러한 방정식을 일반화하면
    $a_{i} =
    \begin{bmatrix}
    \left(n+1 \right) \\
    \left(k \right)
    \end{bmatrix}$
    - 이므로 a_i 는 파스칼의 삼각형의 n+1 번째 행의 k 번째 열의 값과 대응한다.
    - 계수 1, 2, 1 은 파스칼의 삼각형에서 3번째 줄에 해당한다.

- 조건 :
    - 현재의 숫자는 바로 위의 숫자의 왼쪽, 오른쪽 숫자들의 합으로 구한다.

### 2) 코드

#### 조건 1을 반복문을 사용한 조합 코드를 사용하면 간편해진다.

```
def combi(n, r) :
    i = 1
    p = 1
    while i <= r :
        p = p * (n-i+1) // i
        i += 1
    return p

combi(0,0)

=====<print>=====

1

print(combi(2,0))
print(combi(2,1))
print(combi(2,2))

=====<print>=====

1
2
1
```

### 3) 최종코드
- 책에 나와 있는 for 문을 사용한 조합 코드를 사용하면 파스칼의 삼각형이 제대로 안 만들어진다. combi 함수의 i 범위가 잘 못됨. r+1 로 해주어야 함.
- 출력하는 코드에서 n을 따로 정의하지 않고 N으로 for 문 값으로 얻는 점이 눈여겨 볼만 하다.

#### 파스칼의 삼각형의 형태로 출력하는 코드

```
def combi_1(n, r) :
    p = 1
    
    for i in range(1, r+1) :
        p = p * (n - i + 1) // i
    return p


if __name__ == "__main__" :
    N = 10
    
    # 주어진 N값은 출력하는 행의 갯수이다.
    # t while 문의 제어조건에 따라서 공백의 갯수가 달라진다.  
    for n in range(N+1) :
        t = 0
        while t < (N-n) * 3 : ### (N-n) * 3
            print(" ", end="")
            t +=1
        
        # combi 함수를 호출하면서 값을 출력하고 띄어쓰기를 하여 균형감을 만든다.
        # %2d, %3d, %4d에 따라서 출력시 간격이 
        for r in range(n+1) :
            print("%3d  "%combi_1(n,r), end=" ")
        print()

=====<print>=====

                                1
                             1     1
                          1     2     1
                       1     3     3     1
                    1     4     6     4     1
                 1     5    10    10     5     1
              1     6    15    20    15     6     1
           1     7    21    35    35    21     7     1
        1     8    28    56    70    56    28     8     1
     1     9    36    84   126   126    84    36     9     1
  1    10    45   120   210   252   210   120    45    10     1
```

#### 최종 코드에서 삼각형 모양으로 출력하기 위해 띄어쓰기를 입력하는 코드 확인
- n이 증가함에 따라서 t도 조건에 따라서 증가함.
- t의 조건에 의해서 띄어쓰기 입력 후, 숫자가 입력된다.

```
if __name__ == "__main__" :
    N = 5

    for n in range(N+1) :
        print("n", n)
        t = 0
        while t < (N-n) * 3 :
            print(" ", end="")
            t += 1
            print("t",t)

        for r in range(n+1) :
            print("r", r)
            print("{}    ".format(combi(n,r)), end="")
        print()

=====<print>=====

n 0
 t 1
 t 2
 t 3
 t 4
 t 5
 t 6
 t 7
 t 8
 t 9
 t 10
 t 11
 t 12
 t 13
 t 14
 t 15
r 0
1
n 1
 t 1
 t 2
 t 3
 t 4
 t 5
 t 6
 t 7
 t 8
 t 9
 t 10
 t 11
 t 12
r 0
1    r 1
1
```

# 038. 유클리드 호제법을 사용하여 최대공약수 구하기

### 1) 접근풀이 및 조건
- 앞에서 최대공약수 코드에서 한번 다루었음
- 유클리드 호제법은 두 수를 서로 나누어서 구하는 방법을 말한다.
- a, b의 최대공약수는 a를 b로 나눈 나머지 r이라고 하면, 다시 b를 r로 나누었을 때 r' 라고하면 이 과정을 반복하여 마지막 r'가 0일 때의 b가 두 수의 최대공약수이다.
    - 92 % 80 = 12, 80 % 12 = 8, 12 % 8 = 4, 8 % 4 = 0 따라서, 92와 80의 최대공약수는 4이다

### 2) 코드

```
def f(a, b) :
    if b == 0 :
        return a
    else :
        print("a : {}, b: {}, 나머지 : {}".format(a, b, a % b))
        return f(b, a % b)

if __name__ == "__main__" :
    print(f(84, 60))

=====<print>=====

a : 84, b: 60, 나머지 : 24
a : 60, b: 24, 나머지 : 12
a : 24, b: 12, 나머지 : 0
12
```

# 039. 반복문을 사용하여 피보나치 수열 구하기

### 1) 접근풀이 및 조건
- 피보나치수열 : 인도의 수학자 핑갈라가 기원전 5세기 처음 언급함, 이후 레오나르도 피보나치가 토끼의 생식을 비유로 피보나치 수열을 언급한 것이 유래가 됨.
- 토끼 한쌍은 두달이 지나면 새끼를 낳을 수 있고, 매달 새끼를 낳는다고 할때, 1달 (a,b) 한 쌍, 2달 (a,b) 한 쌍, 3달 (a,b), (c,d) 두 쌍, 4달 (a,b), (c,d), (c',d'), 5달 (a,b), (c,d), (c',d'), (c'', d''), (e,f) 5쌍 ...
- 피보나치 수열은 점화식의 형태이다.
    - f_n = if n = 0 : 0, if n = 1 : 1, if n > 1 : f_n-2 + f_n-1
- 이러한 피보나치 수열을 코드로 구현

### 2) 코드

```
def fibo(n) :

    a = 1
    b = 1

    # b 가 앞의 두 수를 더한 값이 되고, a가 원래의 b가 되므로 피보나치 수열이 가능하다.
    for k in range(3, n) :
        dummy = b
        b = a + b
        a = dummy

    return b

for i in range(2, 10) :
    print("{}달 {}쌍".format(i-1, fibo(i)))

=====<print>=====

1달 1쌍
2달 1쌍
3달 2쌍
4달 3쌍
5달 5쌍
6달 8쌍
7달 13쌍
8달 21쌍
```

# 040. 재귀호출을 사용하여 피보나치 수열 구하기

### 1) 접근풀이 및 조건
- 점화식의 조건 그대로 재귀호출로 나타내면 된다.

### 2) 코드

```
def fibo_2(n) :
    if n == 0 :
        return 0
    elif  n == 1 :
        return 1
    else :
        return fibo_2(n-1) + fibo_2(n-2)

fibo_2(5)

=====<print>=====

5
```
```
def fibo_3(n) :
    if n <= 2 :
        return 1
    else :
        return fibo_3(n-2) + fibo_3(n-1)

for j in range(1, 11) :
    print(fibo_3(j))

=====<print>=====

1
1
2
3
5
8
13
21
34
55
```
# 041. 동적계획법을 사용하여 피보나치 수열 만들기

### 1) 접근풀이 및 조건
- 동적계획법을 사용하여 피보나치 수열 만들기
- 동적계획법은 어떤 문제를 풀기위해서 여러가지 하위 문제로 나누어 풀고, 그것들을 결합하여 최종목적에 도달하는 방식을 의미한다.
- 하위문제를 계산한 후 해결책을 저장하면 같은 문제가 나왔을 때 해결하기 쉽다.
- 따라서 동적계획법은 계산횟수를 줄일 수 있고, 피보나치 수열과 같은 여러번의 계산을 해야하는 경우 재귀호출 보다 성능이 좋다.

### 2) 코드
- 동적계획법에서는 배열대신 table 이라고 부른다.

```
table = [0 for i in range(100)]
#table = [0] * (n+1)

def fibo(n) :

    if n == 0 or n == 1 :
        return n

    table[0] = 0
    table[1] = 1

    for i in range(2, n+1) :
        table[i] = table[i-1] + table[i-2]


if __name__ == "__main__" :
    fibo(30)
    for j in range(31) :
        print("피보나치 %2d = %8d"%(j, table[j]))
        #print("피보나치 {} = {}".format(j, table[j]))

=====<print>=====

피보나치  0 =        0
피보나치  1 =        1
피보나치  2 =        1
피보나치  3 =        2
피보나치  4 =        3
피보나치  5 =        5
피보나치  6 =        8
피보나치  7 =       13
피보나치  8 =       21
피보나치  9 =       34
피보나치 10 =       55
피보나치 11 =       89
피보나치 12 =      144
피보나치 13 =      233
피보나치 14 =      377
피보나치 15 =      610
피보나치 16 =      987
피보나치 17 =     1597
피보나치 18 =     2584
피보나치 19 =     4181
피보나치 20 =     6765
피보나치 21 =    10946
피보나치 22 =    17711
피보나치 23 =    28657
피보나치 24 =    46368
피보나치 25 =    75025
피보나치 26 =   121393
피보나치 27 =   196418
피보나치 28 =   317811
피보나치 29 =   514229
피보나치 30 =   832040
```

# 042. 동적계획법을 사용하여 1부터 N까지의 합 구하기 (재귀 호출 사용)

### 1) 접근풀이 및 조건
- 동적계획법 방식과 재귀호출을 사용하여 1부터 N까지의 합 구하기

### 2) 코드
- table의 k번째 인덱스에 n+1 까지 증가하며 재귀호출한 값의 합이 저장된다.
- n = 10으로 하고 f(1)을 호출하면, table[1]에 55가 저장되어 출력된다. table[1]에는 k+1의 값이 더해지게 된다.
    - f(1) = 55, f(2) = 54, f(3) = 52 ...
- 최종 범위인 N을 지정해주면, table[n]에 N값이 저장되고, table[n-1]에는 n-1 + n의 값이 저장된다.
    - n=10 이면 table[10] = 10 + 0이 저장되고, table[9] = 9 + 10의 값이 저장된다. 이 과정이 실행되면 table[1]에 10+9+8+7+...+2+1의 값이 저장된다.

```
table = [0 for _ in range(20)]
n = 0

def f(k) :
    #print(k)
    if k == n + 1 :
        return 0

    table[k] = k + f(k + 1)

    return table[k]

if __name__ == "__main__" :
    n = 10
    print("%d"%f(1))

=====<print>=====

55
```
#### n번째 인덱스에 n값이 저장되어 인덱스 1에까지 누적되어 계산되는 방식이기때문에 n과 k값이 같으면 n의 값만 저장되어있으므로 n값만 출력된다.

```
n = 15
f(15)

=====<print>=====

15

table

=====<print>=====

[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 15, 0, 0, 0, 0]
```

#### 위의 코드는 주어진 n에서 -1 씩 감소하며 더하는 것을 각 배열에 저장하는 것과 같다.

```
def ff(n) :
    i = 0
    sum = 0
    while i < n :

        print("%2d + %2d = %2d"%(sum, n-i, sum+(n-i)))
        sum = sum + (n-i)
        i += 1

    return sum

ff(10)

=====<print>=====

0 + 10 = 10
10 +  9 = 19
19 +  8 = 27
27 +  7 = 34
34 +  6 = 40
40 +  5 = 45
45 +  4 = 49
49 +  3 = 52
52 +  2 = 54
54 +  1 = 55

55
```

#### while 문을 사용한 코드

```
def solve(n) :
    i = 0
    sum = 0
    while i <= n :
        print("%2d + %2d = %2d"%(sum, i, sum + i))
        sum = sum + i

        i = i + 1
    return sum

solve(10)

=====<print>=====

 0 +  0 =  0
 0 +  1 =  1
 1 +  2 =  3
 3 +  3 =  6
 6 +  4 = 10
10 +  5 = 15
15 +  6 = 21
21 +  7 = 28
28 +  8 = 36
36 +  9 = 45
45 + 10 = 55

55
```
#### 재귀 호출을 사용한 코드

```
def solve_2(n) :
    print(n)
    if n == 0 :
        return 0
    elif n == 1 :
        return 1
    else :
        return n + solve_2(n-1)

solve_2(10

=====<print>=====

10
9
8
7
6
5
4
3
2
1

55
```

# 043. 반복문(상향식 설계)을 사용하여 1부터 N까지의 합 구하기

### 1) 접근풀이 및 조건
- 동적계획법의 특징인 메모이제이션 memoization 을 사용하여 코드 만들기
- 자세한 설명이 부족하다.

### 2) 코드

```
table = [0 for _ in range(20)]

if __name__ == "__main__" :

    n = 10

    for i in range(n+1) :
        if i == 1 :
            table[i] = 1
        else :
            table[i] = table[i-1] + i

    print("%d"%(table[n]))

=====<print>=====

55
```
```
table

=====<print>=====

[0, 1, 3, 6, 10, 15, 21, 28, 36, 45, 55, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

#### 앞의 동적계획법과 재귀호출을 사용한 방식은 n 에서부터  n-1 -> ... -> 1 까지 값이 더해져서 배열의 모습은 하향식 처럼 보인다.
- 최종값이 인덱스 1에 저장된다.

```
table = [0 for _ in range(20)]
n = 0

def f(k) :
    #print(k)
    if k == n + 1 :
        return 0

    table[k] = k + f(k + 1)

    return table[k]

if __name__ == "__main__" :
    n = 10
    f(1)
    print(table)

=====<print>=====

[0, 55, 54, 52, 49, 45, 40, 34, 27, 19, 10, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```
