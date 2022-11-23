# Problem 9/30

## Quiz : "Recursion 3"
재귀함수를 구현하는 문제

## Task
- 재귀함수를 코드로 구현하고, N 을 파라미터로 정수를 입력받아 수열을 결과값을 출력하시오.

```
factorial(N) = 1 (N<=1) , N * factorial(N-1) (otherwise)
```

## Input Format
- 단일한 정수 N : factorial 에 전달할 아규먼트

## Output Format
- N! 출력 

## Constraints
- 2 <= N <= 12
- 반드시 재귀함수의 이름을 factorial 로 할 것

## Input - Output 
```
input 
3

output
6
```

## Solution !!
- 재귀함수는 함수 안에서 함수 자신을 실행한다.
- 무한히 실해되며, 특정 횟수를 넘어가면 자동으로 중단된다.
- 여러가지 "점화식"을 구현하는 데 유용하다.

```
def factorial(n) :
    if n <= 1:
       return 1
    else :
       return n * factorial(n-1)
```

- factorial 함수를 선언하고, 조건문을 사용하여 해당 수열의 조건을 한정해주었다.
- return 을 사용하여 함수 호출 시 결과값을 저장하여 출력할 수 있도록 하였다.

## Useful code !!
- 다양한 점화식을 코드로 구현해 보자.
- 우선 수열은 반복적인 현상을 수학적으로 표현하는 방법이며, 다양한 반복적 현상을 수열을 통해서 그 반복성의 일반화를 구현할 수 있는 장점이 있는 것 같다.
- 점화식(=재귀식)은 수학에서 다루는 여러가지 수열의 하나이며 정의는 다음과 같다.

```
수열에서 이웃하는 두개의 항 사이에 성립하는 관계를 나타낸 관계식이다. (위키백과)

```
- 수열은 선형대수, 행렬 등과 연관되어 데이터사이언스 분야의 토대라고 생각된다.
- 대표적인 점화식인 등차수열과 피보나치 수열을 파이썬으로 구현해 본다.

### 1. Arithmetic Progression : 등차 수열
- 특징 : 입력값이 1이면 결과는 0이고, 입력값이 1보다 크면 입력값보다 1작은 결과값에 2를 더한 값이다.

```
An = 0 (if n = 1)
An = An(n-1) + 2 (if n > 1)
```
- 코드
```
def an(n) :
   if n == 1 :
      return 0
   else :
      return an(n-1) + 2
```
### 2. Fibonacci numbers : 피보나치 수열
- 특징 : 입력값이 0 또는 1이면 결과값은 입력값과 같다. 입력값이 1보다 크면 입력값보다 1작은 결과값과 2작은 결과값을 합한 값이다.
- 피보나치 수열은 자연 현상의 반복성을 잘 나타내는 수열 중 하나이며, 황금비율 등과도 관계까 있어서 유용하게 사용되는 경우가 많다고 한다. 

```
Fn = 0 (if n = 0)
Fn = 1 (if n = 1)
Fn = Fn(n-1) + Fn(n-2) (if n > 1)
```
- 재귀문을 이용한 피보나치 수열
```
def fbn(n) :
   if n < 2 :
      return n
   else :
      return fbn(n-1) + fbn(n-2)
```
- dynamic programing 을 이용한 피보나치 수열
```
fibo = []
for x in range(0, 10) :
   if x < 2 :
      fibo.append(1)
   else :
      fibo.append(fibo[x-2] + fibo[x-1])
```
- list nested 를 이용한 피보나치 수열
```
fibo2 = [1,1]
[fibo2.append(fibo2[x-2]+fibo[x-1]) for x in range(0, 10) if i >= 2]
print(fibo2)
```
- list nested + python property 를 이용한 피보나치 수열
- 파이썬에서 음수 인덱스는 가장 뒤에서부터 시작하므로, -1, -2 는 해당 list 의 최신 1 , 2 번째를 구해준다.
```
fibo3 = [1, 1]
[foibo3.append(fibo3[-1]+fibo3[-2]) for x in range(0, 10)]
print(fibo3)
```
- lambda 를 이용한 피보나치 수열
```
fibo4 = lambda n : n if n < 2 else fibo4(n-2) + fibo4(n-1)
for i in range(0, 10) :
   print(fibo4(i))
```
- reduce 와 lambda 를 이용한 피보나치 수열
```
from functools import reduce

fibo5 = lambda n : reduce(lambda x, n : [x[1], x[0] + x[1]], range(n), [0, 1])[0]
for i in range(1, 10) :
   print(fibo5(i))
```

## 참고한 사이트
- 피보나치 수열의 의미에 대해서 알기 쉽게 정리 해준 사이트
```
https://holicmath.tistory.com/45
```
- 피보나치 수열을 파이썬 코드로 구현하는데 여러가지 방법을 공유해준 사이트
```
https://www.crocus.co.kr/1643
```
