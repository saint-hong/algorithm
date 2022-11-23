# Problem 2/30

## Operators
저녁 식사 비용을 계산하시오.

## Task
- meal_cost, tip_percent, tax_percent 입력받는다.
- meal_cost 와 각각의 비율을 곱하여 tip, tax 비용을 계산한다.
- meal, tip, tax cost 를 합산하여 total_cost 를 출력한다.

## Input
- meal_cost : 12.00
- tip_percent : 20
- tax_percent : 8

## Output
- total_cost : 15

## Solution !!
함수를 만들고 각각의 task 를 수행하는 코드를 순차적으로 입력.

```
def solve(meal_cost, tip_percent, tax_percent) :
   tip = meal_cost * tip_percent / 100
   tax = meal_cost * tax_percent / 100
   total_cost = meal_cost + tip + tax
   print(round(total_cost))
```
- 주어진 입력 변수
```
if __name__ == '__main__' :
   meal_cost = float(input())
   tip_percent = int(input())
   tax_percent = int(input())
   solve(meal_cost, tip_percent, tax_percent)
```
