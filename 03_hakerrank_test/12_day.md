# Problem 11/30

## Quiz : "Inheritance"
Person 클래스와 이를 상속받는 Student 클래스를 만들고, 학생이름과 아이디, 과목수, 과목별 점수를 입력받아서 클래스를 호출하여 이름, 아이디, 평균점수에 해당하는 등급을 출력하시오.

## Task
- 다른 하나로부터 상속받는 2개의 클래스를 만든다.
- Student 클래스는 Person 클래스를 상속받는다. 
- Person 클래스는 printPerson() 함수를 갖는다. printPerson() 함수는 주어진 조건데로 출력을 한다.
- Student 클래스는 calculator() 함수를 갖는다. calculator() 함수는 함수호출 시 주어진 아규먼트 중에서 과목 점수를 파라미터로 받아서, 평균값을 구하고, 등급을 저장한다.
- 등급 
```
O : 90 <= avg <= 100
E : 80 <= avg < 90
A : 70 <= avg < 80
P : 55 <= avg < 70
D : 40 <= avg < 55
T : avg < 40
```

## Input Format
- 성과 이름, 아이디를 입력받는다.
- 각각 변수를 선언하여 저장한다. 
- 과목 점수를 입력받는다.
- Student 클래스를 호출하고, 아규먼트로 fristName, lastName, idNum, scores 4개를 사용한다.
- Student 클래스의 printPerson() 함수를 호출한다.
- studend 클래스의 calculator() 함수를 호출하여 등급을 출력한다.
```
line = input().split()
firstName = line[0]
lastName = line[1]
idNum = line[2]
numScores = int(input())
scores = list(map(int, input().split()))
s = Student(firstName, lastName, idNum, scores)
s.printPerson()
print("Grade:", s.calculator())
```

## Sample Input-Output
```
### input 
Heraldo Memelli 8135627
2
100 80

### output
Name: Memelli, Heraldo
ID: 8135627
Grade: O
```

## Solution !!
- 주어진 조건을 확인한 후 Person 클래스와 Student 클래스를 만들고, Student 클래스가 Person 클래스를 상송받도록 한다.
- 클래스 호출시 주어지는 아규먼트를 클래스에서 파라미터로 받을 수 있도록 생성자 함수를 사용하여 정의해준다. 
   - fristName, lastName, idNum, scores
- Person 클래스의 함수는 printPerson()
- Student 클래스의 함수는 calculator(

```
class Person :

   def __init__(self, firstName, lastName, idNum) :
        self.firstName = firstName
        self.lastName = lastName
	self.idNum = idNum
   
   def printPerson(self) :
        print("Name: {}, {}".format(firstName, lastName))
	print("ID: {}".format(idNum))

class Student(Person) : ### Person 클래스를 상속받는다.
   
   def __init__(self, firstName, lastName, idNum, scores) :
        self.firstName = firstName
        self.lastName = lastName
	self.idNum = idNum
        self.scores = scores

   def calculator(self) :
        avg = sum(self.scores) / len(self.scores) ### self.scores 는 리스트 타입의 데이터이다.
        if 90 <= avg and avg <= 100 :
            return "O"
        elif 80 <= avg and avg < 90 :
            return "E"
        elif 70 <= avg and avg < 80 :
            return "A"
        elif 55 <= avg and avg <700 :
            return "P"
        elif 40 <= avg and avg < 55 :
            return "D"
        else :
            return "T"
``` 

## Expansion
- super : 부모 클래스에서 사용된 함수의 코드를 가져다가 자식 클래스의 함수에서 재사용할 때 사용.
```
class A :
   def plus(self) :
      code 1

class B(A) :
   def minus(self) :
      super().plus()  ### class A 의 plus 함수의 코드를 쉽게 가져온다
      code 2
```

- 다중상속 : 여러개의 클래스를 한번에 상속 받는다.
```
class A :
   def show_img(self) :
      print ("show_img")

class B :
   def save_mail(self) :
      print ("samve_mail")

class C :
   def wifi(self) :
      print ("wifi")

class D(A, B, C) :   ### 클래스 A, B, C 를 다중상속 받는다.
   def camera(self) :
      print ("camera")
```
