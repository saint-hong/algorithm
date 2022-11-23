# Problem 4/30

## Quiz : "Class vs. Instance"
주어진 입력 코드에 따라서 초기나이를 입력하면 3년 후의 나이에 대한 메시지를 2번씩 출력하시오.

## Task
- 주어진 input code 에 따라서 클래스와 함수를 만들 것.
- initialAge 가 특정 조건의 숫자인 경우에 해당하는 메시지를 출력할 것.
- age 가 0 보다 작으면 "Age is not valid, setting age to 0." 출력
- age 가 13 보다 작으면 "You are young." 출력
- age 가 13 이상이고 18 보다 작으면 "You are a teenager." 출력
- age 가 18 이상이면 "You are old." 출력

## Input Format
- input format 코드가 주어짐.
- int t 는 age 를 테스트 하는 횟수.
```
t = int(input())
for i in range(0, t) :
   age = int(input())
   p = Person(age)
   p.amIOld()
   for j in range(0, 3) :
      p.yearPasses()
   p.amIOld()
   print("")
```

- input format 코드 분석
```
t = int(input())
for i in range(0, t) :
   age = int(input())
```
   - 어떤 숫자를 input 받는 변수 t
   - 첫번째 for 문에서 변수 i 는 rnage(0, t) 범위의 수를 차례로 받는다. 이 for 문에서 i 가 차례로 숫자를 받을 때마다 하위의 코드가 반복 실행된다. t 가 4 이면 0, 1, 2, 3 총 4번 실행 된다.
   - age 변수도 int 를 input 받으며, 첫번째 for문이 반복될때마다 age도 갱신된다.
```
p = Person(age)
p.amIOld()
```
   - 객체 p 는 class Person 을 선언한다. 아규먼트로 위에서 정의 된 age 를 사용한다.
   - class Person 의 함수 amIOld() 를 실행하면 age 에 해당하는 메시지가 출력된다.
```
for j in range(0, 3) :
   p.yearPasses()
p.amIOld()
print("")
```
   - 두번째 for 문 실행, j 는 0, 1, 2 총 3번의 숫자를 받는다. 3번 반복된다. 
   - p.yearPasses() 는 class Person 의 함수를 실행하며, for 문이 3번 실행될때마다 실행한다.
   - p.amIOld() 함수의 실행, 두번째 for 문이 3번 반복되면 age 의 멘트가 출력된다.  

## Input
```
4
-1
10
16
18
```

## Output
```
Age is not valid, setting age to 0.
You are young.
You are young.

You are young.
You are a teenager.

You are a teenager.
You are old.

You are old.
You are old.
```

## Solution !!
- input format code 분석에 맞춰서 code 를 만든다.
- class Person, 함수 amIOld, yearPasses
- amIOld 함수는 age 에 해당하는 메시지를 출력한다.
- yearPasses 함수는 처음 입력된 age 에 3이 더해지도록 한다.
```
class Person :
	def __init__(self, initialAge) :
	     self.initialAge = initialAge
	     if self.initialAge < 0 :
	             print("Age is not valid, setting age to 0.")
	
	def amIOld(self) :
	     if self.initialAge < 13 : 
	          print("You are young.")
	     elif (self.initialAge >= 13) and (self.initialAge < 18) :
	          print("You are a teenager.")
	     else :
	          print("You are old.")
	
	def yearPasses(self) :
	     self.initialAge = self.initialAge + 1
```
## Difficult Point @.@
- input format code 를 분석하는 데 어려웠다.
- 함수의 파라미터를 어떤것으로 정해야하는지 어려웠다.
- input format code 의 for 문 반복 실행 원리를 이해하고, 하위 코드가 실행되는 것을 파악하기 어려웠다

## Another Solution
```
class Person :
	def __init__(self, initialAge) :
	     self.age = 0
	     if initialAge < 0 :
	             print("Age is not valid, setting age to 0.")
             else :
	        self.age = initialAge

	def amIOld(self) :
	     if age < 13 : 
	          print("You are young.")
	     elif 13 <= age < 18 :
	          print("You are a teenager.")
	     elif age >= 18 :
	          print("You are old.")
	
	def yearPasses(self) :
	     global age
	     age += 1
```
- yearPasses() 함수에서 global 함수를 사용한 점이 흥미롭다. 
- global age 는 class 외부에서 정의 된 age 의 데이터를 가져오게 된다.
