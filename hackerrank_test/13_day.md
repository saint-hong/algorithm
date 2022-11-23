# Problem 13/30

## Quiz : "Abstract Class"
추상 클래스 기능을 사용하여 책제목과 작가, 책 가격을 주어진 형식으로 출력하시오.

## Task
- Book 클래스와 이를 상속받는 MyBook 클래스를 만든다.
- MyBook 클래스는 3개의 파라미터를 갖는다.
   - (str) title, author, (int) price
- Book 클래스의  추상 메서드인 display()를 구현하고 3줄을 출력한다.
   - Title : title name
   - Author : author name
   - Price : price

## Input Format
- 추상 클래스의 모듈 호출과 Book 클래스, 추상 매서드가 주어진다.
```
from abc import ABCMeta, abstractmethod    ### 추상클래스 모듈 불러오기

class Book(object, metaclass=ABCMeta):     ### 추상클래스 설정
    def __init__(self, title, author):     ### 생성자 함수 설정
        self.title=title
        self.author=author

                                  
    @abstractmethod      ### display() 추상 매서드 선언, 추상 매서드는 비어있는 함수여야 한다. 호출안됨.
    def display() :      
        pass
```
- 데이터 입력받는 변수와 클래스의 선언 및 함수 호출이 주어진다.
```
title = input()         ### 책 이름 입력 받기
author = input()        ### 작가 이름 입력 받기
price = int(input())    ### 책 가격 입력 받기       
new_novel = MyBook(title, author, price)   ### MyBook 클래스 선언, 아규먼트로 title, author, price 정의
new_novel.display()     ### MyBook 클래스의 display() 함수 호출
```

## Sample Input-Output
```
<input>
The Alchemist
Paulo Coelho
248

<output>
Title: The Alchemist
Author: Paulo Coelho
Price: 248

```

## Solution !!
- 추상 클래스는 메서드의 목록만 가진 클래스이며, 상속받는 클래스에서 메서드 구현을 강제 한다.
- 상속 받는 클래스에서 추상 메서드를 구현하지 않고 실행하면 에러가 발생한다. 
- 추상 클래스는 인스턴스로 만들 수 없다. 즉 클래스로 선언되지 않는다. 따라서 추상 메서드를 만들 때 빈 메서드로 만든다. (pass) 사용
```
class MyBook(Book) :                             ### Book 추상 클래스 상속
    def __init__(self, title, author, price) :   ### 생성자 함수 설정
        self.title = title
        self.author = author
        self.price = price

    def display(self) :              ### 추상 매서드인 display() 함수를 반드시 구현해야 한다.  
        print("Title:", self.title)
        print("Author:", self.author)
        print("Price:", self.price)
```
## Expansion : 객체지향 프로그래밍 (Object-Oriented Programming, OOP)
- 추상 클래스는 객체지향 프로그래밍(Object-Oriented Programming, OOP)을 따른다.
- 객체지향 프로그래밍은 프로그래밍의 여러 방식 중 하나이며, 프로그램을 코드의 목록으로 보는 시각이 아니라, 객체들의 모임으로 파악하는 시각을 전제한다.
- 이렇게 만들어진 객체들간에는 메시지를 주고받고 데이터를 효율적으로 처리하도록 한다.
- 복잡한 프로그래밍의 협업에서 반복적인 코드로 인한 문제점들을 해결해주기때문에, 변경이 쉽고 유연하도록 만들어 준다. 
- 자동차의 제조를 비유로 들면,  자동차 전체 구조를 표상하는 전체 설계도가 있고, 자동차의 각 부품이나 파트별 제작을 위한 세부 설계도가 있듯이  객체지향 프로그래밍도 코드 전체를 표상하는 전체 설계도에 따라서 각 기능별 세부 설계도를 만들고 언제든지 세부 설계도의 코드를 수정하고 전체 구조와 협업될 수 있도록 한다.  

