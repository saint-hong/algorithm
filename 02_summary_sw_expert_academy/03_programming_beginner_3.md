# 함수의 기초 

## 1. 함수의 개념과 목적
- 함수 : 프로그램에서 어떤 특정한 기능을 수행할 목적으로 만들어진 재사용 구조의 코드 부분

### 1-1. 함수의 장점
- 1) 하나의 큰 프로그램을 여러 부분으로 나눌 수 있기때문에 구조적 프로그래밍이 가능해짐
- 2) 동일 함수를 여러 곳에서 필요할 때마다 호출 할 수 있음
- 3) 수정이 용이함

### 1-2. 함수의 사용방법
- 인자 -> 매개변수 -> 함수 -> 반환값
- 순수함수 pure function : 결과값 반환 이외에 외부에 영향을 주지 않는 함수 
- 파이썬 등의 함수형 프로그래밍 지원 언어에서는 순수 함수를 인자나 반환값으로 사용

## 2. 함수의 호출 및 선언

### 2-1. print()
- print() 함수 : 괄호안에 인자를 입력하면 인자가 print() 함수로 전달되어 출력된다.

### 2-2. 함수의 선언
- 명령문1~return문까지 코드블록
```
def 함수명 (매개변수) : 
      명령문1
      명령문2
      return문
```
- **함수 선언의 위치 문제**
    - 인터프리터 언어의 경우 함수 선언 위치가 중요하다.
    - 동일한 쉘에서 명령문의 순서에 따라서 실행된다.
    - 함수가 맨 밑에 있으면 실행 할 수 없다는 오류 발생한다.

## 3. 함수의 유형
- 매개변수 : 함수에 입력값을 전달해야 하는가를 결정하는 요인
- 반환값 : 함수가 수행 결과를 호출한 곳으로 돌려줄 필요가 있는가를 결정하는 요인

### 3-1. 매개변수와 반환 값이 있는 함수
- 인자 -> 매개변수 -> 함수 -> 반환값

```
def func_parameters_return(x, y, z) : 
    print()
    print()
    return "hello"
    
ret_val = func_parameters_return(1, 2, 3)
print(ret_val)
```
- 함수를 호출하면 매개변수(x, y, z)에 인자값이 전달된다.
- 함수를 호출한 위치에 반환값으로 return 값이 전달 된다. 
- 함수를 호출하면 1, 2, 3 인자값이 각각 매개변수 x, y, z에 전달된다.
- 함수의 반환값 return 값이 변수 ret_val에 저장된다. 
- 함수 내부의 print() 함수 2개가 실행되고, 마지막으로 함수를 호출한 위치의 print()함수가 실행된다.

### 3-2. 매개변수는 없고 반환 값이 있는 함수
- 입력값이 전달될 필요가 없고, 함수를 호출한 위치에 반환값을 돌려줄 필요가 있다고 생각되는 함수

```
def func_noparameters_return() :
    print()
    return "hello"
    
ret_val = func_noparameters_return()
print(ret_val)
```
- 매개변수가 없어서 괄호만 입력됨
- 함수를 호출한 위치에 반환값으로 return 값이 전달된다.
- 함수를 호출할때 전달할 인자값이 없다.
- 함수를 호출한 위치에 return 값이 ret_val 변수에 전달되어 저장된다.
- 함수 내부의 print()가 실행된 후 함수호출 위치의 print()가 실행된다.

### 3-3. 매개변수는 있고 반환 값이 없는 함수
- 인자값을 함수로 입력받고, 반환값을 호출위치로 전달하지 않는 함수

```
def func_parameters_noreturn(x, y, z) :
    print()
    print()
    
func_parameters_noreturn(1, 2, 3)    
```
- 함수에 매개변수 x, y, z가 인자를 받는다.
- 함수호출시 1, 2, 3 인자값을 매개변수 x, y, z에 전달한다.
- 반환값 return 이 없으므로 함수내부의 print()함수가 실행되어 출력 된다.

### 3-4. 매개변수와 반환 값이 없는 함수
- 함수에 인자값을 입력 받을 필요가 없고, 반환값을 전달할 필요도 없는 함수

```
def func_noparameters_noreturn() :
    print()
    
func_noparameters_noreturn()  
```
- 함수에 매개변수가 없으므로 인자값을 받지 않는다.
- 함수에 반환값이 없으므로 호출위치에 값을 전달하지 않는다.
- 함수를 호출하면 함수 내부의 print()가 실행된다.


## 4. 함수와 매개변수
- `명시적 매개변수 parameter` : 함수 호출 시 입력값을 전달 받기 위한 변수
    - 함수호출 시 전달받은 인자의 값에 의해 타입이 결정된다. 
    - 선언된 매개변수의 개수만큼 인자를 전달 가능하다. (기본)
    - 언팩연산자(*)가 붙지 않은 매개변수
- `인자 argument` : 함수 호출시 함수의 매개변수에 전달되는 값    
- 매개변수와 인자의 갯수가 일치하는 경우
    - 매개변수 : x, y, z
    - 인자값 : 1, 2, 3

```
def func(x, y, z) : 
    result = x + y + z
    return result
    
func(1, 2, 3)    
```

- 인자의 갯수가 적은 경우
    - typeerror 발생

```
func(1, 2)
```

- 인자의 갯수가 더 많은 경우
    - typeerror 발생
    
```
func(1, 2, 3, 4)
```

### 4-1. 언팩 연산자 (*)
- `언팩 연산자 (*)` : 매개변수의 개수를 가변적으로 사용할 수 있도록 한다.
    - **매개변수 적용 시 인자를 튜플형식으로 처리한다.**
- `가변형 매개변수` : 언팩연산자+매개변수
    - 가변형 매개변수는 하나만 사용하는 것이 좋다.
    - 가변형 매개변수는 매개변수의 마지막으로 지정해야 부작용이 없다.

```
def calc_sum(*params) : 
    total = 0
    for v in params : 
        total += v
    return total
    
ret_val = calc_sum(1, 2, 3)
print(ret_val)
```

- 함수를 호출하면 인자값들이 튜플형식으로 매개변수에 전달된다. (언팩연산자 사용)
- 함수 내부에서 가변 매개변수 params를 반복문의 순회객체로 사용한다.
- 반환값으로 total에 누적된 params의 합이 호출위치에 전달된다.
- 함수호출시 인자값으로 1, 2, 3을 가변 매개변수에 전달한다.
- ret_val에 반환값이 저장된다.
- print() 함수가 실행된다.

### 4-2. 튜플 형식의 반환값
- 하나 이상의 값을 반환할 수 있다. 
    - return total1, total2 -> (total1, total2)
    - print() 함수의 인자값으로 언팩연산자를 사용할 수 있다.

### 4-3. 키워드 언팩 연산자 (**)
- `키워드 언팩 연산자 keywords parameter` : 매개변수의 개수를 가변적으로 사용할 수 있도록 함
    - **키워드 인자들을 전달해 매개변수를 딕셔너리 형식으로 처리한다.**
    - key1=value1, key2=value2
    
```
def func(**params) : 
    for k in params.keys() : 
        print(k, params[k])
        
func(a=1, b=2, c=3)      
```

- 키워드 언팩 연산자를 사용한 가변 매개변수는 전달받은 인자들을 딕셔너리 형식으로 처리한다.
- 여기에서 key는 전달받은 매개변수 값이고, value는 전달받은 인자값이다.
- 함수호출에서 a, b, c는 딕셔너리의 key가 되고, 1, 2, 3은 딕셔너리의 value 가 된다.

### 4-4. 기본값을 갖는 매개변수
- 매개변수에 전달할 인자값이 생략 된 경우
    - **사용할 기본값을 지정할 수 있다.**
    - 기본값을 가지는 매개변수는 일반 매개변수 앞에 위치할 수 없다.

```
def func(x, y, operator="+") : 
    if operator == "+" : 
        return x + y
    else : 
        return x - y

ret_val = func(10, 5)
print(ret_val)
```
    
- 함수의 일반 매개변수 뒤에 기본값 매개변수를 입력한 경우
- 매개변수 순서데로 인자값이 전달된다.
- operator에 해당하는 인자값이 없는 경우 기본값인 "+"가 사용된다.
- 함수를 호출하면 10, 5 인자값이 x, y 매개변수에 전달된다. 
- operator 매개변수에는 전달된 인자값이 없으므로 기본값이 사용된다.

### 4-5. scope
- `스코프 scope` : 변수의 유효범위
    - 전역 스코프 : 어디서나 접근 가능한 **전역 변수**
    - 함수 스코프 : 함수 내에서만 접근 가능한 **지역 변수**
- 변수에 접근하는 절차
    - 함수 스코프안에서 가장 먼저 변수 a를 찾는다.
    - 함수내에 변수가 없으면 그 다음 전역 스코프에서 변수를 찾는다.
    - 전역, 함수 스코프 양쪽에 변수가 없으면 error 발생한다.
    - 지역변수와 전역변수의 이름이 같을 경우 전역변수가 가려져 접근을 못할 수 있다.
        
```
a = 1
def scope() : 
    a = 2
    print(a)
    
scope()
print(a)
```

#### 접근하고자 하는 전역변수 앞에 **global** 을 기술한다.
- x=5 -> x=6으로 변경됨
- x가 함수 스코프의 global x로 바뀌었기 때문

```
def change_global_var() : 
    global x
    x += 1
    
x = 5
change_global_var()
print("전역변수 x의 값 : {0}".format(x))
```

## 5. 고급함수 사용법

### 5-1. 중첩함수
- 함수내에 중첩함수를 선언해 사용가능
    - 중첩함수를 포함하는 함수 내에서만 호출이 가능함
    - 중첩함수를 포함하는 함수의 스코프에도 접근이 가능함
- 함수내에서 직접 선언해 호출할 수도 있음
- 함수의 매개변수로 함수인자를 전달받아 함수 내에서 호출해서 사용가능
    - calc() 함수를 호출할 때 함수 plus()를 인자를 매개변수에 전달한다.
    - calc() 함수의 func 매개변수에 plus()가 전달되고
    - 반환값으로 func(x, y)가 호출 된다. (plus함수가 호출된다.)
    - plus() 함수에 x, y 값이 인자로 전달된다.
    
```
def calc(func, x, y) :
    return func(x, y)
    
def plus(op1, op2) : 
    return op1 + op2

def minus(op1, op2) :
    return op1 - op2
    
ret_val = calc(plus, 10, 5)
print(ret_val)
```

- **프로그램의 유연성을 높이기 위해 함수를 매개변수로 전달하는 방식을 선호한다.**
    - 그러나 매번 함수를 선언해 사용하는 불편함이 있을 수 있다.
    
### 5-2. 람다식
- `lambda 매개변수 : 반환값`
    - 변수에 저장해 재사용이 가능한 함수처럼 사용함
    - 기존의 함수처럼 매개변수의 인자로 전달함
    - 함수의 매개변수에 직접 인자로 전달함
- 매번 함수를 호출해야하는 불편함을 덜어준다.

### 5-3. 클로저
- 중첩함수에서 중첩함수를 포함하는 함수의 scope에 접근이 가능
- 중첩함수 자체를 반환값으로 사용하는 경우(return에서 중첩함수를 호출하지 않음)
    - 정보 은닉 구현 가능
    - 전역변수의 남용 방지
    - 메서드가 하나밖에 없는 객체를 만드는 것보다 우아한 구현 가능

## 6. 실습

### 6-1. 함수 선언
- 함수의 매개변수 x, y에 인자값이 전달된다.
    - 함수 호출에서 사용 된 변수 a, b

```python
def calc_sum(x, y) :
    return x + y

a, b = 2, 3
c = calc_sum(a, b)
d = calc_sum(a, c)

print("사용자 정의 함수 calc_sum() 호출을 이용한 c의 결과 : {0}".format(c))
print("사용자 정의 함수 calc_sum() 호출을 이용한 d의 결과 : {0}".format(d))

>>> print

사용자 정의 함수 calc_sum() 호출을 이용한 c의 결과 : 5
사용자 정의 함수 calc_sum() 호출을 이용한 d의 결과 : 7
```

### 6-2. 명시적 매개변수와 가변 매개변수의 혼합 사용
- 첫번째 명시적 매개변수에 인자값이 가장 먼저 전달된다.
    - 0 -> precision 전달
- 나머지 인자값들이 가변 매개변수에 튜플 형식으로 전달된다.
    - (1, 2) -> `*params` 전달

```python
def calc_sum(precision, *params) :
    if precision == 0 :
        total = 0
    elif 0 < precision < 1 :
        total = 0.0

    for val in params :
        total += val

    return total

ret_val = calc_sum(0, 1, 2)
print(ret_val)

>>> print

3

ret_val = calc_sum(0.5, 1.2, 3.4)
print(ret_val)

>>> print

4.6
```

### 6-3. 한 개 이상의 결과값을 튜플 형식의 반환값으로 전달하는 매개변수
- 언팩 연산자를 붙인 매개변수는 인자값을 튜플 형식으로 전달한다.

```python
def calc_sum(precision1, precision2, *params) :
    if precision1 == 0 :
        total1 = 0
    elif 0 < precision1 < 1 :
        total1 = 0.0

    if precision2 == 0 :
        total2 = 0
    elif 0 < precision2 < 1 :
        total2 = 0.0

    for val in params :
        total1 += val
        total2 += val

    return total1, total2

ret_val = calc_sum(0, 0.5, 1, 2)
print(ret_val)

>>> print

(3, 3.0)
```

#### print() 함수에 언팩연산자를 사용하여 인수 입력
- 튜플 인수값의 값이 순차적으로 str.format() 함수에 입력된다.

```python
print("{0}, {1}".format(*ret_val))

>>> print

3, 3.0
```

### 6-4. 키워드 언팩 연산자를 사용하는 딕셔너리 형식의 가변 매개변수
- 키 key : 전달된 매개변수 이름 : a, b, c
- 값 value : 전달된 인자 값 : 1, 2, 3

```python
def use_keyword_arg_unpacking(**params) :
    for k in params.keys() :
        print("{0} : {1}".format(k, params[k]))

print("use_keyword_arg_unpacking()의 호출")
use_keyword_arg_unpacking(a=1, b=2, c=3)

>>> print

use_keyword_arg_unpacking()의 호출
a : 1
b : 2
c : 3
```

### 6-5. 기본값을 가진 매개변수를 사용한 함수

```python
def func(x, y, operator="+") :
    if operator == "+" :
        return x + y
    else :
        return x - y

ret_val = func(10, 5)
print(ret_val)

>>> print

15

ret_val = func(10, 5, "+")
print(ret_val)

>>> print

15

ret_val = func(10, 5, "-")
print(ret_val)

>>> print

5

ret_val = func(10, 5, 2)
print(ret_val)

>>> print

5
```

### 6-6. 함수 스코프를 갖는 변수의 유효 범위

```python
def test_scope(a) :
    result = a + 1
    print("\n\ttest_scope() 안에서의 a의 값 : {0}".format(a))
    print("\n\ttest_scope() 안에서의 result의 값 : {0}".format(result))
    return result

x = 5
print("test_scope() 호출 전 x의 값 : {0}".format(x))
ret_val = test_scope(x)
print("\ntest_scope() 함수가 반환한 값 : {0}".format(ret_val))
print("test_scope() 호출 후 x의 값 : {0}".format(x))

>>> print

test_scope() 호출 전 x의 값 : 5

	test_scope() 안에서의 a의 값 : 5

	test_scope() 안에서의 result의 값 : 6

test_scope() 함수가 반환한 값 : 6
test_scope() 호출 후 x의 값 : 5
```

### 6-7. 함수 내에서 global 변수에 접근하기
- 함수내 스코프의 변수에 global 을 붙여주면 전역변수에 접근할 수 있다.

```python
def change_global_var() :
    global x
    x += 1

x = 5
change_global_var()
print("전역변수 x의 값 : {0}".format(x))

>>> print

전역변수 x의 값 : 6
```

### 6-8. 고급함수 사용 : 중첩함수

```python
def calc(operator_n, x, y) :
    return operator_n(x, y)

def plus(op1, op2) :
    return op1 + op2

def minus(op1, op2) :
    return op1 - op2

ret_val = calc(plus, 10, 5)
print(ret_val)

>>> print

15

ret_val = calc(minus, 10, 5)
print(ret_val)

>>> print

5
```

### 6-9. 고급함수 사용 : 람다식

```python
def calc(operator_n, x, y) :
    return operator_n(x, y)

ret_val = calc(lambda a, b : a + b, 10, 5)
print(ret_val)

>>> print

15

ret_val = calc(lambda a, b : a - b, 10, 5)
print(ret_val)

>>> print

5
```

### 6-10. 고급함수 사용 : 람다식, 언팩 연산자를 사용한 경우
- calc 함수의 매개변수는 가변 매개변수이다.
- 반환값으로 호출된 op_n 함수의 매개변수는 람다식의 매개변수의 갯수와 같아야 한다.
- 따라서 가변 매개변수의 튜플형식의 값을 인덱스를 사용하여 인수로 전달해줘야 한다.

```python
def calc(op_n, *params) :

    return op_n(params[0], params[1])

ret_val = calc(lambda a, b : a + b, 10, 5)
print(ret_val)

>>> print

15
```

### 6-11. 고급함수 사용 : 클로저
- `id = 0` : id 변수는 outer_func의 지역변수
    - outer_func 함수내의 코드로 접근가능 
    - outer_func 함수내의 중첩함수에서만 접근가능
- `nonlocal id` : 변수 id가 중첩함수인 inner_func 함수의 지역변수가 아니라는 의미.
    - 변수 id에 접근하려면 outer_func함수의 스코프에서 찾게 만든다.
- `return inner_func` : inner_func 함수를 호출하는 것이 아님
    - 함수에 대한 참조를 반환함
- 함수 작동 순서
    - 1) 중첩함수 inner_func() 호출
    - 2) outer_func() 함수의 지역변수 id의 값이 1씩 증가
    - 3) 증가된 id값 반환
    - 4) str.format()함수의 인자로 전달. 변환 문자열 생성
    - 5) print() 함수를 통해 표준출력으로 출력

```python
def outer_func() :
    id = 0

    def inner_func() :
        nonlocal id
        id += 1

        return id

    return inner_func

make_id = outer_func()

print("make_id()의 호출 결과 : {0}".format(make_id()))
print("make_id()의 호출 결과 : {0}".format(make_id()))
print("make_id()의 호출 결과 : {0}".format(make_id()))

>>> print

make_id()의 호출 결과 : 1
make_id()의 호출 결과 : 2
make_id()의 호출 결과 : 3
```

### 고급함수 사용 : 문제
- 반지름 입력
- 원의 면적을 계산하는 함수
- 원의 둘레를 계산하는 함수

```python
PI = 3.14

def input_radius()  :
    radius = input("반지름을 입력하시오 : ")
    return float(radius)

def circle_area(r) :
    return PI * r * r

def calc_circumference(r) :
    return 2 * PI * r

radius = input_radius()
area = circle_area(radius)
circumference = calc_circumference(radius)

print("원의 면적 : {0:.2f}, 원의 둘레 : {1:.2f}".format(area, circumference))

>>> print

반지름을 입력하시오 : 3
원의 면적 : 28.26, 원의 둘레 : 18.84
```

## 7. 연습문제

### 7-1. 함수 연습문제 1
- 반복문을 이용해 단어의 순서를 거꾸로 반환하는 함수를 작성하시오.
- 함수를 이용해 회문(앞뒤 어느쪽에서도 같은 단어) 여부를 판단하는 코드를 작성하시오.

```python
def solve(word) :
    half_len = int(len(word) / 2)
    reverse_word = ""

    for s in word[::-1] :
        reverse_word += s

    if word[:half_len] == reverse_word[:half_len] :
        return print("{}\n입력하신 단어는 회문(Palindrome)입니다.".\
                     format(reverse_word))
    else :
        return print(reverse_word)

test_word = "abvvba"
solve(test_word)

>>> print

abvvba
입력하신 단어는 회문(Palindrome)입니다.
```

#### 단어 거꾸로 만드는 코드
- str을 반복문의 순회객체로 사용한다.
- 인덱싱을 거꾸로 하여 뒤의 단어부터 꺼낸다.
- 이것을 변수에 차례대로 누적하여 합한다.

```python
test = "apple"
test 

>>> print

'apple'

word_str = ""
for i in test[::-1] :
    word_str += i

word_str

>>> print

'elppa'
```

#### 입력 된 단어가 회문인지 확인하는 코드 추가
- 입력된 단어 길이의 절반을 계산한다.
- 입력된 단어의 절반이 거꾸로 만든 단어의 절반과 같으면 회문

```python
test = "abecba"
word_str = ""
for i in test[::-1] :
    word_str += i

half_temp = int(len(test) / 2)

if test[:half_temp] == word_str[:half_temp] :
    print("회문")
else :
    print("회문 아님")

>>> print

회문 아님
```
### 7-2. 함수 연습문제 2
- 사용자 두명으로부터 가위, 바위, 보를 입력 받는다.
- 가위, 바위, 보 규칙이 정의된 함수를 만든다.
- 이 함수를 이용해 승패를 결정하는 코드를 만든다.

```python
def solve(p1_ele, p2_ele) :
    if p1_ele == "가위" :
        if p2_ele == "바위" :
            print("바위가 이겼습니다!")
        elif p2_ele == "보" :
            print("가위가 이겼습니다!")
        elif p2_ele == "가위" :
            print("무승부 입니다!")

p1 = str(input())
p2 = str(input())
ele1 = str(input())
ele2 = str(input())

>>> print

홍길동
이순신
가위
바위

## 함수 호출
solve(ele1, ele2)

>>> print

바위가 이겼습니다!
```

### 7-3. 함수 연습문제 3
- 소수를 검사하는 함수를 정의하시오.
- 입력한 숫자가 소수인지 판단하는 프로그램을 작성하시오
- 소수이면 "소수입니다." 출력
- 아니면 "소수가 아닙니다." 출력

```python
def solve(num) :
    count = 0
    i = 1

    while i <= num :
        if num % i == 0 :
            count += 1
        i += 1

    if count == 2 :
        print("소수입니다.")
    else :
        print("소수가 아닙니다.")

temp = int(input())
solve(temp)

>>> print

13
소수입니다.
```

### 7-4. 함수 연습문제 4
- 다음 결과와 같이 피보나치 수열의 결과를 생성하는 프로그램을 작성하시오.
    - 피보나치 수를 리스트에 담아서 출력하기

#### 반복문을 사용한 피보나치 코드

```python
def fibo(num) :
    a = 1
    b = 1
    temp_lst = [a, b]

    for k in range(0, num-2) :
        dummy = b
        b = a + b
        a = dummy
        temp_lst.append(b)

    return temp_lst

p = int(input())
fibo(p)

>>> print

10
[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

#### 재귀함수 호출을 사용한 피보나치 코드

```python
def fibo2(x) :
    if x < 2 :
        return 1
    else :
        return fibo2(x-2) + fibo2(x-1)

num = 10
temp_lst = []
for j in range(0, num) : 
    temp = fibo2(j)
    temp_lst.append(temp)

print(temp_lst)

>>> print

[1, 1, 2, 3, 5, 8, 13, 21, 34, 55]
```

### 함수 연습문제 5
- 리스트의 항목 중 유일한 값으로만 구성된 리스트를 반환하는 함수를 만드시오.
- 함수를 사용하여 리스트의 중복 항목을 제거하는 프로그램을 작성하시오.
    - not in 명령어를 사용하여 특정값이 숫자 리스트에 들어 있는지 확인하고
    - 없으면 비어있는 리스트에 담는다. 있으면 지나간다.

```python
def solve5() :
    lst = [1, 2, 3, 4, 3, 2, 1]
    print(lst)
    temp_lst = []

    i = 0
    while i <= len(lst)-1 :
        if lst[i] not in temp_lst :
            temp_lst.append(lst[i])
        else :
            pass
        i += 1

    print(temp_lst)

solve5()

>>> print

[1, 2, 3, 4, 3, 2, 1]
[1, 2, 3, 4]
```

### 함수 연습문제 6
- 정렬된 숫자를 가진 리스트에서 특정 숫자를 찾는 함수를 정의하시오.
- 함수를 사용하여 임의의 숫자의 포함 여부를 출력하는 프로그램을 작성하시오.

```python
def solve6() :
    num_lst = [2, 4, 6, 8, 10]
    print(num_lst)

    for i in [5, 10] :
        num1 = i
        if num1 in num_lst :
            print("{0} => True".format(num1))
        else :
            print("{0} => False".format(num1))

solve6()

>>> print

[2, 4, 6, 8, 10]
5 => False
10 => True
```

### 함수 연습문제 7
- 팩토리얼을 구하는 함수를 정의하시오.
- 입력된 숫자에 대한 팩토리얼 값을 구하는 프로그램을 작성하시오.
    - 반복문의 순회객체로 숫자범위를 거꾸로 전달하게끔 만든다.
    - 숫자를 누적하여 곱해준다.
- 재귀함수를 사용하여 만든 코드는 출력양식이 맞지 않음.

```python
def solve7(num) :
    temp = 1

    for i in range(num, 0, -1) :
        temp *= i

    return print(temp)

solve7(5)

>>> print

120
```

### 7-8. 함수 연습문제 8
- 숫자에 대해 제곱을 구하는 함수를 정의하시오.
- 콤마를 구분해 숫자를 입력하면 함수를 사용하여 제곱값을 출력하는 프로그램을 작성하시오.
    - replace 함수를 사용하여 특정 문자열을 ""으로 변환한다.
    - 인덱스번호로 처음 숫자와 두번째 숫자를 정수로 변환하여 각각 변수에 담는다.

```python
def solve8(temp) :
    temp1 = temp.replace(",", "")
    temp1 = temp1.replace(" ", "")
    num1 = int(temp1[0])
    num2 = int(temp1[1])
    print("square({0}) => {1}".format(num1, num1**2))
    print("square({0}) => {1}".format(num2, num2**2))

test = input()
solve8(test)

>>> print

2, 3
square(2) => 4
square(3) => 9
```

### 7-9. 함수 연습문제 9
- 인자로 전달된 두 개의 문자열 중 길이가 더 긴 문자열을 출력하는 함수를 정의하라.

```python
def solve9(word) :
    temp = word.replace(" ", "")
    temp = temp.split(",")

    if len(temp[0]) > len(temp[1]) :
        print(temp[0])
    else :
        print(temp[1])

p = input()
solve9(p)

>>> print

seven, two
seven
```

### 7-10. 함수 연습문제 10
- 인자로 전달된 숫자를 이용해 카운트다운을 하는 함수를 정의하시오.
    - countdown
- 함수를 사용하여 countdown(0), countdown(10)을 순서대로 실행하시오.
- 0보다 작거나 같은 인자인 경우
    - "카운트다운을 하려면 0보다 큰 입력이 필요합니다." 출력

```python
def countdown(num) :
    i = num
    if i <= 0 :
        print("카운트다운을 하려면 0보다 큰 입력이 필요합니다.")
    else :
        while i >= 1 :
            print(i)
            i -= 1

countdown(0)
countdown(10)

>>> print

카운트다운을 하려면 0보다 큰 입력이 필요합니다.
10
9
8
7
6
5
4
3
2
1
```
