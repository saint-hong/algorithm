# basic certificate problem
hackerrank의 python 유저의 기본 능력 파악을 위한 문제.. 
3가지 문제를 풀면, hackerrank 공식 basic certification 이 제공된다. 
먼저 hackerrank 의 문제 출제 방식을 이해햐고 code를 만들어야 한다. 
예를들면 sample input 과 sample output 에만 맞춰서 code를 만들면, code를 제출하는 
code submit 에서 테스트에 통과하지 못할 수가 있다. code submit 에서는 sample input 에 들어가는 
케이스보다 더 다양하고 많은 케이스들이 설정되어 있어서, 반드시 출제 문제의 조건들을 꼼꼼하게
코드에 잘 반영해야 통과 될 수 있다는 점을 알아두어야 한다.  
생각보다 까다로운 문제가 포함되어 있다.

## 1. FizzBuzz
fizzbuzz 함수를 선언하고, 함수에 들어가는 수에 따라서 15, 3, 5 의 
배수임을 확인하는 문구를 출력하고, 3가지에 해당하지 않으면 숫자를 그대로 출력한다.

### solution
  ```
  def fizzbuss(n) :
    if n % 15 == 0 :
      print("15의 배수")
    elif n % 3 == 0 :
      print("3의 배수")
    elif n % 5 == 0 :
     print("5의 배수")
    else :
      print(n)
  ```
  
  ```
  fizzbuzz(25) 
  5의 배수
  ```
### apply
for 문에 fizzbuzz 함수를 넣어서, 원하는 범위의 연속된 숫자들을 출력할 수 있다.

  ```
  number = []
  for idx in range(1, 10):
     number.append(fizzbuzz(idx))
  ```
  
  ```
  1
  2
  3의 배수
  4
  5의 배수
  3의 배수
  7
  8
  3의 배수
  5의 배수
  ```
## 2. avg 구하기
입력 되는 숫자들의 합을 구하고 평균값을 출력한다. 예를들면 10, 2, 6, 30 을 입력받으면,
네 가지 숫자를 더한 후 평균값을 출력한다. 

```
10 + 2 + 6 + 30 / 4

12.0
```
문제의 어려운 점은 평균값을 구하기 위해서 몇 개의 숫자가 입력되었느지 갯수를 세야하는 과정이
포함하는 것이다.

### solution
- 함수를 만들고,
- 파라미터 값을 받는 datas 변수를 선언한다.
- datas의 값들을 차례대로 더해주기 위해서 reduce와 lambda 를 사용하고 datas_sum 변수에 담는다.
- datas의 갯수를 세는 코드를 len()을 사용하고 datas_length 변수에 담는다. 
- result 에서 datas_sum과 datas_length 를 나누어 평균값을 구한다.
- return 으로 result 값이 출력되도록 한다. 

   ```
   def avg(*args) :
      from functools import reduce

      datas = [*args]
      datas_sum = reduce(lambda x, y : x + y, datas)
      datas_length = len(datas)
      result = datas_sum / datas_length

      return result
   ```
   ```
   avg(10, 2, 6, 30)
   
   12.0
   ```

- "reduce" 와 lambda 를 함께 사용하면 주어진 값을 차례대로 더하는 과정을 간편하게 처리할 수 있다. 
   ```
   from functools imprt reduce

   reduce(lambda x, y : x + y, test)
   ```
   ```
   test = [10, 12, 20]

   42
   ```
