# 알고리즘 성능평가
- 코딩 테스트의 문제를 풀다가 시간 초과라는 실패 원인을 해결하기 위해 찾던 중 알게 되었다.
   - 되짚어 보면 알고리즘 공부를 위해 보았던 책에서 어느정도 접했던 기억이 있었음
- 코딩 테스트에 통과하기 위해 코드를 여러번 다른방식으로 만들어보아도 시간 초과로 실패하면서 알고리즘의 성능이 중요하다는 것을 깨달을 수 있었다.
- 알고리즘의 성능을 평가하는 개념과 성능을 높일 수 있는 방안들을 정리해 보았다.

### 알고리즘 성능평가란?
- 알고리즘이 제대로 작동하는지 성능을 테스트 해보는 것을 말한다.
   - 알고리즘의 성능은 컴퓨터 환경, 코드의 구성등에 따라서 실행과정이 다를 수 있다. 
   - 그러나 일반적으로 환경적 요인보다 알고리즘 자체의 구성적 문제를 가지고 평가를 한다.
- 알고리즘의 성능을 평가하기 위한 기준
   - 시간 복잡도 time complexity : 알고리즘의 수행시간 분석
      - 시간 복잡도가 높으면 더 많은 시간이 소요된다는 의미
   - 공간 복잡도 space complexity : 알고리즘이 작동하면서 사용하는 메모리량에 관한 분석
      - 공간 복잡도가 높으면 메모리 사용량이 높다는 의미
- 알고리즘의 성능은 복잡도가 낮을 수록 좋다고 볼 수 있다.

### 복잡도는 어떻게 측정하나?
- `빅오표기법 big-o notation` : 어떤 함수의 증가 양상을 다른 함수와의 비교로 표현하는 방법 (점근표기법, 란다우 표기법 이라고 함)
   - 알고리즘의 최악의 상태를 측정한다. (Worst cast)
   - 알고리즘의 성능이 최악의 기준 이상은 한다는 의미
- 빅오 표기법의 수학적 정의 : f(n) <= kg(n)
   - 내가 만든 알고리즘 f(n)의 성능은 kg(n) 함수의 성능(점근 상한선)을 넘어가지 않는다는 의미
- `세부내용`
   - **O(1)** : 입력 데이터가 몇 개이든 상관없이 같은 시간이 걸린다.
      - 입력 데이터의 크기가 상관 없다. 
      - 그러나 상수 자체가 무한히 커지면 좋은 것은 아니다.
      - 해쉬 테이블 조회, 삽입 알고리즘, push, pop 등...
   - **O(logN)** : 입력 데이터가 N개이면 시간은 약간씩 증가한다. 로그 그래프와 유사함.
      - 입력 데이터의 크기가 커도 크게 영향을 받지 않는다.
      - 이진 탐색 알고리즘 등...
   - **O(N)** : 입력 데이터가 N개이면 N 시간이 걸린다. (선형시간)
      - 반복문 for : n번 반복하면 O(n) 시간
      - 모든 입력값을 최소 한번 살펴보는 경우 등..
   - O(NlogN) : 로그 선형시간, 성능이 좋은 알고리즘이 대체로 이 시간에 속한다.
      - 퀵정렬, 힙정렬, 병합정렬 등..
   - **O(N^2)** : 입력 데이터가 N개이면 N의 제곱 만큼 시간이 걸린다.
      - N이 작으면 괜찮지만, N이 100000, 그 이상인 경우 시간이 오래 걸리 수 있다.
      - for 문이 2개 중첩된 경우, 삽입정렬, 거품정렬, 선택정렬 등..
   - O(N^3) : 입력 데이터가 N개이면 N의 3제곱 만큼 시간이 걸린다.
      - for 문이 3개 중첩된 경우 등..
   - O(2^N) : 입력 데이터가 N개이면 2의 N제곱만큼 시간이 걸린다. 
      - 알고리즘 성능이 나쁘다는 의미이다.
   - O(n!) : 입력 데이터가 N개이면 N팩토리얼 만큼 시간이 걸린다.
- 시간이 오래 걸리는 순서 
   - O(1) < O(logN) < O(N) < O(N^2) < O(N^3) < O(2^N) < O(N!)
- 이를 통하여 **각각의 기준마다 어떤 코드를 구성해야하는지 알 수 있다.**
   - 즉 알고리즘의 성능을 어떻게 좋게 개선할 수 있는지 최적화를 생각해 볼 수 있다. 
   - 반복문의 사용, 자료형의 사용에 따라서 알고리즘의 성능이 달라진다.
- 이 외에도 여러가지 성능 측정 방법이 있다.
   - 소문자 O 표기법
   - 대문자 오메가 표기법 : 알고리즘의 최적의 실행 시간을 표기
   - 소문자 오메가 표기법
   - 대문자 세타 표기법
- 참고 여러가지 함수, 명령어들과의 조합 등에 의해서 성능이 달라질 수 있다.

### 시간 복잡도가 의미하는 것은?
- 알고리즘, 즉 코트를 구현할 떄 내가 원하는 결과를 도출하기 위한 목적도 중요하지만 효율적인 방향으로 구현해야 한다는 의미이다.
   - 경우에 따라서는 몇달이 걸리는 알고리즘들도 있다고 하는데, 어쨌든 프로그래밍, 알고리즘 구현이라는 행위 자체가 복잡한 과정을 단순하고 빠르게 변화시키는 것이 중요하기 때문에 효율성을 고려해야 한다.
- **빅오 표기법이 의미하는 것은 시간 복잡도에 맞는 코드를 할 필요가 있다는 것이다.**
   - 예를들면 리스트 자료형을 사용하는 경우와 딕셔너리 자료형을 사용하는 경우에 따라서 시간 복잡도가 달라진다.

### 자료형에 따른 시간 복잡도
- ics information and computer science :  캘리포니아 대학의 Richard E. Pattis 교수의 컴퓨터 사이언스 렉쳐
- 이 렉쳐의 오픈 소스 중 자료형의 사용에 따른 시간 복잡도에 관한 것을 참고하였다.
   - https://www.ics.uci.edu/~pattis/ICS-33/lectures/complexitypython.txt
- 자료형의 특징
   - list : 순서가 있다. 수정이 가능하다. mutable
   - set : 순서가 없다. unique, 수정이 가능하다. mutable
   - dict : 순서가 없다. 키와 값의 메핑 형태


#### List
```
Operation     | Example      | Class         | Notes
--------------+--------------+---------------+-------------------------------
Index         | l[i]         | O(1)	     |
Store         | l[i] = 0     | O(1)	     |
Length        | len(l)       | O(1)	     |
Append        | l.append(5)  | O(1)	     | mostly: ICS-46 covers details
Pop	      | l.pop()      | O(1)	     | same as l.pop(-1), popping at end
Clear         | l.clear()    | O(1)	     | similar to l = []

Slice         | l[a:b]       | O(b-a)	     | l[1:5]:O(l)/l[:]:O(len(l)-0)=O(N)
Extend        | l.extend(...)| O(len(...))   | depends only on len of extension
Construction  | list(...)    | O(len(...))   | depends on length of ... iterable

check ==, !=  | l1 == l2     | O(N)          |
Insert        | l[a:b] = ... | O(N)	     |
Delete        | del l[i]     | O(N)	     | depends on i; O(N) in worst case
Containment   | x in/not in l| O(N)	     | linearly searches list
Copy          | l.copy()     | O(N)	     | Same as l[:] which is O(N)
Remove        | l.remove(...)| O(N)	     |
Pop	      | l.pop(i)     | O(N)	     | O(N-i): l.pop(0):O(N) (see above)
Extreme value | min(l)/max(l)| O(N)	     | linearly searches list for value
Reverse	      | l.reverse()  | O(N)	     |
Iteration     | for v in l:  | O(N)          | Worst: no return/break in loop

Sort          | l.sort()     | O(N Log N)    | key/reverse mostly doesn't change
Multiply      | k*l          | O(k N)        | 5*l is O(N): len(l)*l is O(N**2)
```

#### Tuples
- 튜플은 동일한 시간 복잡도를 갖는다.

#### Sets

```
Operation     | Example      | Class         | Notes
--------------+--------------+---------------+-------------------------------
Length        | len(s)       | O(1)	     |
Add           | s.add(5)     | O(1)	     |
Containment   | x in/not in s| O(1)	     | compare to list/tuple - O(N)
Remove        | s.remove(..) | O(1)	     | compare to list/tuple - O(N)
Discard       | s.discard(..)| O(1)	     |
Pop           | s.pop()      | O(1)	     | popped value "randomly" selected
Clear         | s.clear()    | O(1)	     | similar to s = set()

Construction  | set(...)     | O(len(...))   | depends on length of ... iterable
check ==, !=  | s != t       | O(len(s))     | same as len(t); False in O(1) if
      	      	     	       		       the lengths are different
<=/<          | s <= t       | O(len(s))     | issubset
>=/>          | s >= t       | O(len(t))     | issuperset s <= t == t >= s
Union         | s | t        | O(len(s)+len(t))
Intersection  | s & t        | O(len(s)+len(t))
Difference    | s - t        | O(len(s)+len(t))
Symmetric Diff| s ^ t        | O(len(s)+len(t))

Iteration     | for v in s:  | O(N)          | Worst: no return/break in loop
Copy          | s.copy()     | O(N)	     |
```

#### Dictionaries
- dict 자료형도 대부분의 연산이 O(1) 에 해당한다.
```
Operation     | Example      | Class         | Notes
--------------+--------------+---------------+-------------------------------
Index         | d[k]         | O(1)	     |
Store         | d[k] = v     | O(1)	     |
Length        | len(d)       | O(1)	     |
Delete        | del d[k]     | O(1)	     |
get/setdefault| d.get(k)     | O(1)	     |
Pop           | d.pop(k)     | O(1)	     |
Pop item      | d.popitem()  | O(1)	     | popped item "randomly" selected
Clear         | d.clear()    | O(1)	     | similar to s = {} or = dict()
View          | d.keys()     | O(1)	     | same for d.values()

Construction  | dict(...)    | O(len(...))   | depends # (key,value) 2-tuples

Iteration     | for k in d:  | O(N)          | all forms: keys, values, items
	      	      	       		     | Worst: no return/break in loop
```

