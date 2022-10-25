## 7. 흐름제어 : 반복
- for문, while문

### 7-1. for 문
- 리스트, 튜플, 사진, 문자열과 같은 객체 항목들을 순회하며 특정 작업을 반복해서 수행하기 위해 사용
- T이면 제어문 탈출, F이면 명령문 수행
- for문의 문법

```for 변수 in 순회할 객체 :
        명령문1
        명령문2
```
- 코드상에 많은 중복이 나타남 -> 변경 사항이 발생하면 수정사항이 많아짐
- 코드의 중복 된 부분을 찾아 반복문 안에서 처리하는 명령문으로 바꿔서 해결한다.

### 7-2. for문의 순회 객체
- range() 함수
- **range()** : 객체를 생성하는 코드
    - 첫번째 인자 : 범위
    - 두번쨰 인자 : 범위에 포함 안됨 (범위의 마지막 부분)
    - 세번쨰 인자 : 증감치
    - 두번째 인자 생략 불가
    - 첫번쨰, 세번쨰 인자는 생략가능
- 딕셔너리 객체
    - items() : 딕셔너리 객체 사용시 items() 함수를 사용하면 key, value 값을 동시에 가져온다.
- 문자열
    - 개별 문자를 출력할 수 있다.
- 리스트    
    - 리스트 객체 안의 데이터를 하나씩 가져 올 수 있다.

### 7-3. 중첩된 for문
- for문 안에 또 다른 for문이 들어 있는 형태
- 바깥 for문과 안쪽 for문이 순차적으로 진행 된다.
- 바깐 for문이 완료되면 중첩된 for문 전체가 종료된다.

```
for 변수1 in 순회객체1 : 
    for 변수2 in 순회객체2 :
        명령문1
        명령문2
    명령문3    
```
- **순회객체1의 항목수 x 순회객체2의 항목수** 만큼 반복된다.
- 바깥for문이 실행되기 전 무언가를 수행할 때는 안쪽 for문 바로 밑에서 명령문 실행
    - 명령문3
    
### 7-4. while 문
- bool 값을 반환하는 조건식의 결과에 의해 반복 결정된다.
    - 조건식 T 면 계속 명령문 실행
    - 조건식 F 면 while 문 탈출
- 조건식이 False 값을 반환해야 while문이 중단된다. 따라서 무한반복 방지를 고려해야 한다.

```
while 조건식 : 
    명령문1
    명령문2
```

### 7-5. break, continue
- for문 : 순회객체의 마지막 항목까지 반복
    - continue 문 : 이후 코드는 건너뛰고 반복문을 계속 실행할때 사용
    - 어떤 조건을 제외할 떄 사용하면 좋다. 
    - 3의 배수 제외한 총합 등
- while 문 : bool 값을 반환하는 조건식이 False를 반환할 때까지 반복
    - break 문 : 논리적으로 반복문을 빠져나갈때 사용, 바로 종료된다.

#### 구구단 출력하기

```python
dan = int(input("단 입력 : "))
for i in (1, 2, 3, 4, 5, 6, 7, 8, 9, 10) :
    print("{0} x {1:<2} = {2:<2}".format(dan, i, dan*i))

>>> print

단 입력 : 2
2 x 1  = 2
2 x 2  = 4
2 x 3  = 6
2 x 4  = 8
2 x 5  = 10
2 x 6  = 12
2 x 7  = 14
2 x 8  = 16
2 x 9  = 18
2 x 10 = 20
```

#### 딕셔너리객체 항목 출력

```python
dogs = {1 : "리트리버", 2 : "진돗개", 3 : "콜리"}
for key in dogs :
    print("{0} : {1}".format(key, dogs[key]))

>>> print

1 : 리트리버
2 : 진돗개
3 : 콜리
```

#### 딕셔너리객체의 items() 함수 사용

```python
for key, value in dogs.items() :
    print("{0} : {1}".format(key, value))

>>> print

1 : 리트리버
2 : 진돗개
3 : 콜리
```

#### 문자열 개별 출력

```python
temp = "python"

for c in temp :
    print("{0}".format(c))

>>> print

p
y
t
h
o
n
```

#### 리스트 객체 사용

```python
scores = [100, 95, 88, 98]
total = 0

for score in scores :
    total += score

print("총점 : {0}".format(total))

>>> print

총점 : 381
```

#### 중첩for문으로 구구단
- 바깥 for문은 단을 순회
- 안쪽 for문은 곱해지는 숫자를 순회

```python
dan = range(2, 10)
num = range(1, 10)

for i in dan :
    for k in num :
        print("{0} x {1} = {2:>2}".format(i, k, i * k))
        if k == 9 :
            print()

>>> print

2 x 1 =  2
2 x 2 =  4
2 x 3 =  6
2 x 4 =  8
2 x 5 = 10
2 x 6 = 12
2 x 7 = 14
2 x 8 = 16
2 x 9 = 18

3 x 1 =  3
3 x 2 =  6
3 x 3 =  9
3 x 4 = 12
3 x 5 = 15
3 x 6 = 18
3 x 7 = 21
3 x 8 = 24
3 x 9 = 27

....
```

#### while 문으로 구구단

```python
dan = int(input("단 입력 : "))

i = 1
while i < 10 :
    print("{0} x {1} = {2:>2}".format(dan, i, dan * i))
    i += 1

>>> print

단 입력 : 2
2 x 1 =  2
2 x 2 =  4
2 x 3 =  6
2 x 4 =  8
2 x 5 = 10
2 x 6 = 12
2 x 7 = 14
2 x 8 = 16
2 x 9 = 18
```
#### while문에서 리스트 객체 이용

```python
scores = [100, 95, 86, 93]
total = 0
cnt = len(scores)
i = 0

while i < cnt :
    total += scores[i]
    i += 1

print("총점 : {0}".format(total))

>>> print

총점 : 374
```

#### break 문

```python
answer = ""

while True :
    answer = input("명령 입력.\n'q'를 입력하면 종료 : ")
    if answer == "q" :
        break
    print("'{0}' 입력".format(answer))
print("프로그램 종료..")

>>> print

명령 입력.
'q'를 입력하면 종료 : s
's' 입력
명령 입력.
'q'를 입력하면 종료 : e
'e' 입력
명령 입력.
'q'를 입력하면 종료 : t
't' 입력
명령 입력.
'q'를 입력하면 종료 : q
프로그램 종료..
```

#### continue 문
- 3의 배수를 제외한 수의 합 구하기
   - continue 를 사용하면 특정 조건을 무시하고 넘길 수 있다.

```python
numlist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
total = 0

for i in numlist :
    if i % 3 == 0 :
        continue
    total += i

print("3의 배수를 제외한 총합 = {0}".format(total))

>>> print

3의 배수를 제외한 총합 = 37
```
#### for, while 을 사용한 트리만들기
- 트리 1

```python
for i in range(1, 5) :
    print("*" * i)

>>> print

*
**
***
****
```

```python
i = 1
while i <= 4 :
    print("*" * i)
    i += 1

>>> print

*
**
***
****
```

- 트리 2

```python
for i in range(1, 3) :
    for k in range(1, 5) :
        print("*" * k)

>>> print

*
**
***
****
*
**
***
****
```
#### while문 사용하여 이중 트리 만들기
- 안쪽 while 문이 종료되면 변수 k를 초기화 해주어야 한다.

```python
i, k = 1, 1
while i <= 2 :
    while k <= 4 :
        print("*" * k)
        k += 1
    i += 1
    k = 1

>>> print

*
**
***
****
*
**
***
****
```

#### 공백 문자열과 별표문자열을 사용한 트리
- i : 공백 문자열 제어 변수 : 1씩 감수
- k : 별표 문자열 제어 변수 : 1씩 증가
- 별표의 증가 패턴 : 등차수열 : 2씩 증가

```python
i, k = 5, 1
while i >= 0 :
    print("{0}{1}".format(" " * i, "*" * (2 * k - 1)))
    i -= 1
    k += 1

>>> print

     *
    ***
   *****
  *******
 *********
***********
```

### 7-6. 반복문 : 연습문제 1
- 5명의 학생의 점수에 대해 60 이상일 때 합격 메시지를 출력한다.
- 60미만일 때 불합격 메시지를 출력한다.

```python
scores = [88, 30, 61, 55, 95]

for i in range(5) :
    if scores[i] >= 60 :
        print("{0}번 학생은 {1}점으로 합격입니다.".format(i+1, scores[i]))
    else :
        print("{0}번 학생은 {1}점으로 불합격입니다.".format(i+1, scores[i]))

>>> print

1번 학생은 88점으로 합격입니다.
2번 학생은 30점으로 불합격입니다.
3번 학생은 61점으로 합격입니다.
4번 학생은 55점으로 불합격입니다.
5번 학생은 95점으로 합격입니다.
```

### 7-7. 반복문 : 연습문제 2
- 1부터 100까지의 숫자를 for문과 range함수를 이용해서 출력하시오.

```python
for i in range(1, 101) :
    print(i)

>>> print

1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18

....
```

### 7-8. 반복문 : 연습문제 3
- 1부터 100사이의 숫자 중 짝수를 for문을 이용해서 다음과 같이 출력하라.

```python
for i in range(2, 101, 2) :
    print(i, end=" ")

>>> print

2 4 6 8 10 12 14 16 18 20 22 24 26 28 30 32 34 36 38 40 42 44 46 48 50 52 54 56 58 60 62 64 66 68 70 72 74 76 78 80 82 84 86 88 90 92 94 96 98 100
```

### 7-9. 반복문 : 연습문제 4
- 1부터 100사이의 숫자 중 홀수를 for문을 이용해 다음과 같이 출력하라.

```python
for i in range(1, 100, 2) :
    if i != 99 :
        print(i, end=", ")
    elif i == 99 :
        print(i)

>>> print

1, 3, 5, 7, 9, 11, 13, 15, 17, 19, 21, 23, 25, 27, 29, 31, 33, 35, 37, 39, 41, 43, 45, 47, 49, 51, 53, 55, 57, 59, 61, 63, 65, 67, 69, 71, 73, 75, 77, 79, 81, 83, 85, 87, 89, 91, 93, 95, 97, 99
```

### 7-10. 반복문 : 연습문제 5
- 1부터 100사이의 숫자 중 3의 배수의 총합을 for 문을 이용해 출력하라.

```python
total = 0
for i in range(1, 100) :
    if i % 3 != 0 :
        continue
    else :
        total = total + i
print("1부터 100사이의 숫자 중 3의 배수의 총합: {0}".format(total))

>>> print

1부터 100사이의 숫자 중 3의 배수의 총합: 1683
```

### 7-11. 반복문 : 연습문제 6
- 10명의 학생들의 혈액형 데이터
    - ['A', 'A', 'A', 'O', 'B', 'B', 'O', 'AB', 'AB', 'O']
- for 문을 사용하여 각 혈액형 별 학생수를 구하시오.     

```python
data = ["A", "A", "A", "O", "B", "B", "O", "AB", "AB", "O"]
data2 = {"A" : 0, "O" : 0, "B" : 0, "AB" : 0}

for b in data :
    if b == "A" :
        data2["A"] += 1
    elif b == "O" :
        data2["O"] += 1
    elif b == "B" :
        data2["B"] += 1
    elif b == "AB" :
        data2["AB"] += 1

print(data2)

>>> print

{'A': 3, 'O': 3, 'B': 2, 'AB': 2}
```

### 7-12. 반복문 : 연습문제 7
- 10명의 학생들의 점수 데이터
    - [85, 65, 77, 83, 75, 22, 98, 88, 38, 100]
- while 문과 리스트 객체의 pop()을 이용해 80점 이상의 점수들의 총합을 구하라.

```python
scores = [85, 65, 77, 83, 75, 22, 98, 88, 38, 100]
sum = 0

while True :
    if len(scores) != 0 :
        p = scores.pop()
        if p >= 80 :
            sum += p
    else :
        break

print(sum)

>>> print

454
```

### 7-13. 반복문 : 연습문제 8
- while문을 이용해 별을 출력하라.

```python
i = 5
while i >= 1 :
    print("*" * i)
    i -= 1

>>> print

*****
****
***
**
*
```
### 7-14. 반복문 : 연습문제 9
- while문을 이용해 별을 출력하라.

```
*******

 *****

  ***

   *
```
- 코드

```python
i = 7
t = 0
while i >= 4 :
    star = i - t
    print("{0}{1}".format(" " * t, "*" * star))
    t += 1
    i -= 1

>>> print

*******
 *****
  ***
   *
```

### 7-15. 반복문 : 연습문제 10
- 어떤 양의 정수를 입력하여 그 숫자에 0~9가 몇번 사용되는지 표시하라.
- output

```
0 1 2 3 4 5 6 7 8 9

0 2 0 0 0 0 0 0 0 0
```

#### 최종 정답
- 문자열 출력시 마지막에 공백이나, 콤마를 제거하는 방법으로 if, else 대신
- str을 더하는 방식으로 하는 것이 더 깔끔하다.
- 마지막 두 줄을 출력할 때 줄바꿈이 \n이 한번 들어가야 통과 된다.

```python
num = int(input())
count_list = [0] * 10

for i in str(num) :
    for j in range(10) :
        if int(i) == j :
            count_list[j] += 1

num_str = "0"
count_str = "{}".format(count_list[0])

for i in range(1, 10) :
    num_str += " " + "{}".format(i)
    count_str += " " + "{}".format(count_list[i])

print("{}\n{}".format(num_str, count_str))

>>> print

120
0 1 2 3 4 5 6 7 8 9
1 1 1 0 0 0 0 0 0 0
```

### 7-16. 반복문 : 연습문제 11
- for문을 사용해 별 표시 출력하기.
- output

```
    *

   **

  ***

 ****

*****
```

#### 코드
- 문자열의 폭은 고정되어 있다.
- 공백과 별의 갯수가 하나씩 증감한다.

```python
for i in range(4, -1, -1) :
    print("{}{}".format(" " * i, "*" * (5-i)))

>>> print

    *
   **
  ***
 ****
*****
```









