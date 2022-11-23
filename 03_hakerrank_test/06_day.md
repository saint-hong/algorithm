# Problem 6/30

## Quiz : "Let's Review"
loops 코드를 확장시켜서 생각해 볼 수 있는 문제로, 문자열을 입력받으면 짝수, 홀수 번째 문자를 다음의 양식에 맞게 출력한다.

## Task
- 데이터 입력횟수를 의미하는 int T, 데이터 str S
- S 의 길이는 랜덤으로 입력된다. 
- S의 j 번째 문자의 짝수번째 문자는 홀수번째 문자와 구분하여 출력하되, 스페이스바로 띄워준다.
```
Test Case 0 : S = "Hacker"
S[0] = "H"
S[1] = "a"
S[2] = "c"
S[3] = "k"
S[4] = "e"
S[5] = "r"

S[0]S[2]S[4] = "Hce"
S[1]S[3]S[5] = "akr"
```

## Input - Output
- Input
```
2
Hacker
Rank
```
- Output
```
Hce akr
Rn ak
```

## Solution !!
- 첫번째 코드
   - 입력된 str S 데이터의 길이를 확인하고
   - 길이에서 홀수 번째와 짝수 번째를 구분한다.
   - 출력 양식에 맞추기 위해, 짝수 문자를 찾는 함수와 홀수 문자를 찾는 함수 2개로 만들었다.
```
# 짝수번쨰 문자를 찾는 함수

def even_select(self) :
    even_caracter = []
    for idx in range(0, len(self)) :
        if idx % 2 == 0 :
            even_caracter.append(self[idx])

    even_num = [even for even in range(len(self)) if even % 2 == 0]
    for j in range(len(even_num)) :
        print(even_caracter[j], end="")
```
```
# 홀수번쨰 문자를 찾는 함수
def odd_select(self) :
    odd_caracter = []
    for i in range(0, len(self)) :
        if i % 2 == 1 :
            odd_caracter.append(self[i])        

    odd_num = [odd for odd in range(len(self)) if odd % 2 != 0]
    for h in range(len(odd_num)) :
            print(odd_caracter[h], end="")
```

- 함수를 호출 해보면 입력 된 문자의 짝수, 홀수번째 문자를 확인하여 출력이 된다.
- 그런데, 한 줄로 나오지 않고 줄이 바뀐 상태로 출력 된다. 
- 이 문제를 해결하기 위해 여러가지를 시도해 보았지만 찾지 못했다.
```
text = input()
even_select(text)
print("")
odd_select(text)

# Hce
# akr
```

- 코드를 조금더 간단하게 변경 해 보았다.
```
def even_data(self) :

    for num in range(0, len(self)) :
        if num % 2 == 0 :
            print(self[num], end="")
```
```
def odd_data(self) :

    for num in range(0, len(self)) :
        if num % 2 == 1 :
            print(self[num], end="")
```

- 함수를 호출해 보면, 입력된 문자의 짝수, 홀수 번째 문자를 확인하여 출력해준다. 
- 하지만 output format 에 맞지 않아 코드가 통과 되지 못했다.
```
ls = "Hacker"

even_data(ls)

# Hce

odd_data(ls)

# akr
```

- 코드를 여러번 만들어봤지만 코드 제출 과정에서 통과가 안되던 때,
- input format 을 만들어서 S 의 순서를 정해주면 된다는 것을 알게 되었다.
   - 문자 입력 횟수를 정하는 t, 문자를 담는 리스트 타입의 S
   - t 가 입력 되면 그 횟수에 맞추어 S 를 입력한다.
   - 데이터가 입력 되면 S = [] 에 순서대로 저장한다. 
   - 저장 된 S = [] 의 데이터를 순서에 맞게 꺼내어 odd_even_select 함수의 아규먼트로  호출한다.
```
<input format>

t = int(input())
S = []
if 1 <= t <= 10 :
    for i in range(1, t+1) :
        S_i = str(input())
        S.append(S_i)
    for j in range(0, t) :
        odd_even_select(S[j])
```

- 앞에서 S 의 길이와 홀, 짝수 번쨰 문제에서 빠져나오지 못했지만, 문득 offset index 기능을 떠올렸고, 이 문제를 해결 할 수 있었다.
- 최종 코드는 매우 간단해졌고, 코드 제출에서 통과할 수 있었다. 

```
def odd_even_select(self) :
    if 2 <= len(self) and len(self) <= 10000 :
        print(self[::2], self[1::2])
```

## Difficult Point !!
- 주어진 문제의 조건을 잘 파악하는 것이 중요하다. 이것을 놓치면 오랜시간 공들인 코드도 통과가 안된다. 문제의 조건을 잘 파악해야 결국 코드를 만들때 방향도 바로 잡을 수 있다는 것을 알았다.
- 처음 코드를 만들 때는 문자의 길이를 구하고, 짝수 번째, 홀수 번째를 순차적으로 발라내는 부분에 집중했다. 그러다보니 코드가 복잡해졌고, 난해해 졌다.
- 오랜 시간 코드를 완성하기 위해 매진하는 것보다도, 구글링을 통해서 해법의 실마리를 찾은 후 코드를 완성하는 것이 더 효율적이라는 것을 깨달을 수 있었다. 
