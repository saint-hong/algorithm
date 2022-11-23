# Problem 7/30

## Quiz : "Arrays"
array 의 범위를 설정하는 정수를 input 으로 받고, array 의 데이터를 입력하면, 순서를 거꾸로 출력한다.

## Task
- array A 는 정수 N 개의 요소를 갖는다.
- array A 를 공백을 포함하여 순서를 거꾸로 출력한다. 
- array A 의 각 데이터는 행열의 값이므로 바뀌면 안된다.

## Input Format
- 첫 번째 라인은 int N 을 포함 하라.
- 두 번쨰 라인은 공백으로 구분하여 array A 의 요소를 순서를 거꾸로 출력하라.

## Input - Output
- Input
```
4
1 4 3 2
```

- Output
```
2 3 4 1
```

## Solution !!
- int N = 5 이면, array 는 5개의 데이터를 갖는다. int N = 6 이면, array 는 6개의 데이터를 갖는다.
- array A 의 데이터를 N개 입력 받으면, 입력한 순서를 거꾸로 출력한다.
- 중요한 포인트는 input() 함수로 입력받은 데이터를 형태변환을 해줘야, 원하는 방식으로 출력이 쉬워진다. 

- 첫번째 접근.
   - 기본적인 input() 함수의 데이터는 str 타입이고, offset index 를 사용하여 역으로 출력하면 가능하다.
   - array A 의 데이터가 한 자리 정수 일 때는 output format 에 맞는다.
```
data = input() -> 1 2 3 4
print(data[::-1], end=" ")

출력 : 4 3 2 1
```
   - 그러나 str 데이터는 모든 요소를 데이터로 취급하기 때문에, array A 의 데이터가 두자리 이상의 정수가 되면 output format 에 맞지 않는다.
```
data = input() -> 24 18 154 2789
print(data[::-1, end=" ")

출력 : 42 81 451 9872
```
   - 코드를 테스트 하는 과정에서 여러가지 샘플을 테스트하는데, 수십자리의 수나 여러가지 변칙적인 조건도 포함되기도 한다. 따라서 input() 데이터를 str 타입 그대로 사용하는 것은 문제가 발생한다.

- 두번째 접근.
   - input() 데이터를 map 함수를 사용한 int 로 형변환 한다. 
   - strip, split 을 사용하여 입력 데이터를 정제한다.
   - int 로 형변환 후 순서를 거꾸로 저장한 후, 0, 1, 2, 3... 순서로 출력한다.
```
arr = list(map(int, input().strip().split()))
inverse_arr = arr[::-1]

for i in range(0, n) :
   print(inverse_arr[i], end=" ")
```

## Difficult Point @.@
- 코드 테스트에서 사용되는 데이터의 종류가 여러가지라는 것을 파악하는 데 어려웠다.
- strip() 과 split()의 기능을 추가하는 데 어려웠다.

## Useful code !!
- map 함수는 리스트 안의 모든 데이터에 특정 함수를 적용시켜 준다.
- strip() 은 공백이나 특수문자 등을 제거 해준다. 
   - strip() : 양쪽, rstrip() : 오른쪽, lstrip() : 왼쪽
   - 제거할 조건이 여러가지이면 순서가 중요하다.
```
오른쪽에서 설정한 기호들을 제거해준다.

"<#<<python is good.>>>!#".rstrip(">, !, #, .")
출력 : '<#<<python is good'

왼쪽에서 설정한 기호들을 제거해준다.

"!<#<<@python is good.>>>!#".lstrip("!, <, #, @")
출력 : 'python is good.>>>!#'

양쪽에서 공백을 제거해준다.
"  python ".strip()
출력 : python

```
- split() 은 문자열을 설정한 조건으로 나누고, 리스트로 반환해준다.
```
test = "My name is hong seong,hyun."
split_test = test.split()
출력 : ['My', 'name', 'is', 'hong', 'seong,hyun.']

, 를 기준으로 구분 해준다.
test = "My name is hong seong,hyun."
split_test = test.split(",") 
출력 : ['My name is hong seong', 'hyun.']

test = "My, name, is hong, seong_hyun."
split_test = test.split(",")
출력 : ['My', ' name', ' is hong', ' seong_hyun.']

```
