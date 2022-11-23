# problem 10/30

## Quiz : "Binary Numbers"
이진숫자에서 숫자 1이 반복되는 횟수를 찾고, 가장 큰 횟수를 출력하시오.

## Task 
- 10진법의 숫자를 입력받는다.
- 정수 n 을 이진법의 숫자로 변환시킨다.
- 변환된 이진숫자에서 연속으로 반복해서 나오는 숫자 1의 최대 횟수를 출력한다.

## Input Format
- 단일한 정수 n, n 을 이진수로 변환, long_repeat 함수의 결과 출력
```
if __name__ == "__main__"

   n = int(input())
   b_num = bin(n).replace("0b", "")
   print(long_repeat(b_num))
```

## Constraints
- 1 <= n <= 1000000

## Output Format
- 이진숫자에서 숫자 1이 연속으로 반복될 경우, 최대 반복횟수를 출력

## Sample Input-Output
```
input
5

output
1
```

```
input
13

output
2
```
```
input
34567

output
3
```

## Solution !!
### coment
   - 입력받는 숫자의 범위가 넓으므로, 이진숫자의 형태도 다양하다는 것을 코드에 반영해야 한다. 예컨데 "10" 일 경우 최대 반복횟수는 1이 출력되어야 하며, "110111" 일 경우에는 "3"이 출력되어야 한다.
   - 처음에는 이진숫자에서 문자를 하나씩 꺼내어 앞문자와 뒷문자가 같은 경우 count 하는 방식으로 코드를 짰으나, 이렇게 되면 앞, 뒤문자가 다른 경우, 중간에 0이 오는 경우, 인덱스가 -1 일때 처음과 마지막 숫자가 1이면 연속 숫자로 파악하는 경우 등의 상황이 발생하여 어려움을 겪었다.
   - 그러다가 파이썬의 itertools 패키지의 groupby 함수를 알게 되었고, 반복적으로 등장하는 문자를 key, value 형태로 추출할 수 있다는 것을 알게 되었다.

### final code
   - 리스트 컴프리핸션 기능에 groupby 기능을 추가하면, 연속해서 오는 문자의 문자자체와 횟수를 추출하고, 횟수를 list 로 저장한 뒤 list 의 길이를 저장한다.
   - 조건문을 사용하여 문자가 1일 경우에만 한정해주면 1이 연속해서 반복되는 횟수의 최대수 출력을 간편하게 할 수 있다.

```
def long_repeats(self)

   from itertools import groupby

   return max([len(list(count)) for char, count in groupby(self) if char == "1"], default=0)
```
## Anotehr code !!
- for 문을 사용하여 문자열에서 각각 문자를 순서대로 추출하고, 등장하는 문자와 앞,뒤 문자의 조건에 따라서 count 를 하는 코드
- 문자의 count 와 최대반복 maxcount 를 구분한 뒤 1 이 반복되면 count 에 1일 더해지고, maxcount 보다 count 가 큰 경우 maxcount와 count를 같게 설정하였다. 0 이 나오면 count 를 0으로 만들어 준다.

```
n = int(input())
b_num = bin(n).replace("0b", "")

count = 0
maxcount = 0

for i in b_num :
    if i == "1" :
        count += 1
    elif count > maxcount :
        maxcount = count
        count = 0
    else :
        count = 0
        
if count > maxcount :
    maxcount = count
```
- 그 외로, collections 패키지의 Counter 함수를 사용하면, 문자열의 모든 문자의 빈도수를 세어준다.
```
from collection import Counter

word = "11000111"
result = Counter(word)
```
```
출력
Counter({'1':5, '0':3})
```

## Expansion
- 파이썬의 itertools 모듈은 효율적인 반복함수를 만드는 함수를 제공해준다. 데이터의 반복적인 형태를 분석하거나, 만들어야할 때 유용하게 사용할 수 있다.
- 특히 데이터 분석에서 반복적인 작업을 많이 해야할 때에, 메모리 사용을 줄이고, 코드를 더 간결하게 만드는데 도움을 준다.
- python docs 에 소개 된 iterater 함수들을 공부해 보는 것이 좋을 것 같다. 
```
https://docs.python.org/ko/3.8/library/itertools.html
```
