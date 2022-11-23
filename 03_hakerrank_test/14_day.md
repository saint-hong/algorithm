# Problem 14/30

## Quiz : Scope
주어진 범위의 정수 N 개를 각각 차이를 구하고 가장 큰 차이값을 출력하시오.

## Task

## Input Format
```
_ = input()
a = [int(e) for e in input().split(' ')]

d = Difference(a)
d.computeDifference()

print(d.maximumDifference)
```
```
class Difference:
    def __init__(self, a):
        self.__elements = a
```

## Output Format

## input-Output
```
<input>
3
1 2 5

<ouput>
4
```

## Solution!!
```
class Difference:
    def __init__(self, a):
        self.__elements = a

    def computeDifference(self) :
        self.maximumDifference = abs(max(self.__elements) - min(self.__elements))
```
