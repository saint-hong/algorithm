# Problem 3/30

## Quiz : "Intro to Conditional Statements"
홀수와 짝수의 조건에 따라 주어진 값을 출력 하시오.

## Task
- 주어진 int n 으로 다음의 조건을 만족하는 코드를 만드시오.
- n 이 odd (홀수) 이면 "Weird" 를 출력
- n 이 even (짝수) 이면서 2 이상 5 이하의 숫자이면 "Not Weird" 를 출력
- n 이 even 이면서 6 이상 20 이하의 숫자이면 "Weird"를 출력
- n 이 even 이면서 20 보다 큰 숫자이면 "Not Weird"를 출력

## Input -> Output
- 3 -> Weird
- 24 -> Not Weird
- 기타 입력된 정수를 위의 조건에 맞도록 출력

## Solution !!
- 조건문 if / elif 와 in / not in 을 사용한다.
- 가장 상위의 조건인 odd, even 여부를 조사하는 코드 작성
- even 인 경우 하위 조건을 각각 작성

- 입력 조건
```
if __name__ == '__main__':
   N = int(input())
```
- 코드 작성
```
if N % 2 != 0 :
   print("Weird")
elif N % 2 == 0 :
   if N in range(2, 6) :
      print("Not Weird)
   elif N in range(6, 21) :
      print("Weird")
   elif N > 20 :
      print("Not Weird")
```
## Difficult Point @.@
- odd / even 을 구분하는 조건문을 명확하게 작성하는데 시간이 오래 걸림.
- 상위 조건 하위 조건을 구분하기 위해if / elif 의 순서를 정하는데 어려웠다.

## Another Solution
- hackerrank 의 대쉬보드에는 discussion 메뉴가 있는데 여러유저들이 자신이 푼 해법을 공유하거나, 코드 문제를 논의 한다.
- 좀더 간결하고 배울점이 있는 코드를 찾아서 공부해보기로 한다.

- lambda 함수와 삼항연산자를 사용하여 한줄로 조건문을 만족시키는 코드를 작성할 수 있다.
```
print((lambda N : "Weird" if N%2 or 5<N<20 else "Not Weird")int(input()))
```
- 삼항연산자의 if 문으로 "or" 을 사용하였다.
```
T or T = T / T or F = T / F or F = F
```
- Weird 출력의 조건: N 이 홀수 인 경우, 짝수이면서 5와 20 사이의 수
- Not Weird 출력의 조건: N 이 짝수 이면서 2와 6사이의 수인 경우, 20보다 큰 수인 경우를 "or" 을 사용하여 처리할 수 있다.
