# Problem 5/30

## Quiz : "Loops"
int n 이 주어지면 구구단을 아래와 같은 양식으로 출력하시오.

## Task
- n 의 1 부터 10까지의 곱을 구하시오.
- 2 <= n <= 20

## Output Format
- 10 개의 행으로 출력하고, 각 행마다 1 부터 10 까지의 곱을 출력하시오.
- "n x i = result"

## Input - Output
- input
```
2
```
- Output
```
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
2 x 4 = 8
2 x 5 = 10
2 x 6 = 12
2 x 7 = 14
2 x 8 = 16
2 x 9 = 18
2 x 10 = 20
```

## Solution !!
- 특정한 양식으로 출력할 떄에는 print 함수의 세부 조건을 이용한다.
- 특히 데이터가 변경되는 위치에서는 .format 을 사용하면 간편하다.
```
if __name__ = '__main__' :
   
   n = int(input())

    if 2 <= n <= 20 :
       for i in range(1, 11) :
          print("{} x {} = {}".format(n, i, n*i)
    else :
       print("n is wrong!")
```
## Another Solution
- print 함수와 for 문을 한 줄로 구현할 수 있다.
```
n = int(input())
print(*['%d x %d = %d'%(n, i, n*i) for i in range(1, 11)], sep="\n")
```

## Useful code
- print 함수의 특징
```
print(1, 2, 3)
1 2 3

print(1, 2, 3, sep='')
123

print(1, 2, 3, sep=', ')
1, 2, 3

print(1, 2, 3, end='')
print(4, 5, 6)
1 2 3 4 5 6
```
- list 데이터의 출력시 부호 삭제
```
L = [1,2,3, "a", 'b', -1]

print(L)
[1, 2, 3, 'a', 'b', -1]

print(*L)
1 2 3 a b -1
```
