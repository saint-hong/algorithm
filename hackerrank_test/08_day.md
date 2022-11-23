# Problem 8/30

## Quiz : "Dictionaries and Maps"
입력받은 데이터를 딕셔너리 데이터 타입으로 변환하고, 딕셔너리 타입의 데이터를 검색하는 문제

## Task
   - 연락처 데이터를 만들고 이름을 검색하여 결과를 출력한다.
   - 연락처의 데이터 수를 결정하는 정수 n 을 입력받는다.
   - n 개의 "name=phoneNumber" 를 입력받아 딕셔너리 형태로 변환한다.
   - 검색할 이름을 입력받는다.
   - 연락처에서 입력한 이름을 검색하여, 이름이 존재하면 다음과 같이 출력한다.
      - "name=phoneNumber"
   - 이름이 존재하지 않으면 다음과 같이 출력한다.
      - "Not found"

## Input Format
   - 연락처의 인원수에 해당하는 정수 n을 입력받는다.
   - 이름과 8자리의 전화번호를 입력받는다.
      - sam 11223344
   - 검색할 이름을 입력받는다.
   ```
   3
   sam 99912222
   tom 11122222
   harry 12299933
   sam
   edward
   harry
   ```
## Ountput Format
   - 검색한 이름이 연락처에 있으면 다음과 같이 출력한다.
      - sam=11223344
   - 검색한 이름이 연락처에 없으면 다음과 같이 출력한다. 
      - Not found
   ```
   sam=99912222
   Not found
   harry=12299933
   ```
## Constraints
   - 1 <= n <= 100000
   - i <= queries <= 100000

## Explanation
   - n=3 (key, value)
   - phoneBook = {(sam, 99887766), (tom, 11223344), (hong, 33445566)}

## Solution !!
1. final code :

   1) 연락처의 전체 갯수를 정하는 n 입력 받기.
   ```
   n = int(input())
   ```
   2) 이름과 8자리의 데이터를 입력 받고 dict 타입으로 변환하기.
   ```
   ### 데이터를 n 번 입력받을 때마다 .split()을 사용하여 공백을 기준으로 데이터를 구분해준다.
   ### key 와 value 로 저장하기 위해 리스트 컴프리핸션을 사용하여 k와 v 변수로 나눠준다.

   phoneBook = dict((k,v) for k,v in [input().split() for i in range(n)])
   ```
   3) 검색할 데이터를 입력받는다. 
      - 코드 테스트에서 10,000 의 연락처 데이터를 생성하고 10,000 개의 이름을 검색하는데 이떄에 EOFerror 가 발생한다. 
      - EOFerror 는 갑자기 입력변수가 중단될 때 생기는 오류라고 한다. 
      - 이 에러를 해결하려면 try, exception 함수를 설정해 주어야 한다.
   ```
   while True :
      try:
   	 find_name = input().stirp()
	 if find_name in phoneBook :
	     print("{}={}".format(find_name, phoneBook[find_name])
	 else :
	     print("Not found")
      except :
          break
   ```
   4) code
   ```
   n = int(input())
   phoneBook = dict((k,v) for k,v in [input().split() for i in range(n)])
   
   while True :
        try :
	     find_name = input().stirp()
	          if find_name in phoneBook :
	               print("{}={}".format(find_name, phoneBook[find_name])
	          else :
	               print("Not found")
	except :
	     break
   ```
2. First faile code
   1) input 받은 데이터를 dict 형태로 변환하기 위해 list 로 저장한 후, 다시 dict로 변환하는 방법을 사용.
   2) 검색할 이름을 저장하기 위해 list 로 저장한 후, 결과를 검색하는 함수를 호출하였음.
   3) 함수에서 검색할 이름을 리스트 전체로 파라미터로 넘겨 받으면, 다시 하나씩 꺼내어 연락처 데이터에 있는지 없는지 확인 하도록 만들었음.
   4) for 문을 많이 사용하고, 불필요하게 리스트로 저장을 많이 하고, 함수를 사용함으로써 코드가 복잡해졌다.
   5) 또한 결과적으로 첫번째 코드 테스트는 통과하였으나, 최종 테스트에서 많은 량의 데이터를 input 받을 때 발생하는 EOFerror 를 해결하지 못하여 통과 되지 않았다.
   
   ```
   t = int(input())
   datas = []  
   name_df = []   

   for i in range(0, t) :     
      name_num = input().split()
      datas.append(name_num)     ### dict로 변환하기 위해 리스트 형태로 연락처 데이터를 저장
      phoneBook = dict(datas)

   for j in range(0, t) :
      find_name = input()
      name_df.append(find_name)   ### 검색할 이름을 리스트로 저장하고 아규먼트로 사용하여 함수를 호출
   search_phonebook(name_df)

   def search_phonebook(self) :   ### 함수 선언
      for k in range(0, len(self)) :   ### 리스트로 받은 self 의 데이터를 하나씩 연락처와 비교 
         if self[k] in phoneBook.kesy() :
	    print("{}={}".format(self[k], phoneBook[self[k])]
	 elif self[k] not in phoneBook.keys() :
	    print("Not found")
   ```

## Difficult Point @.@
   1) EOFerror 를 해결하는 방법으로 while 문과 try, except 를 사용하여야 코드 제출에서 통과된다.
   2) input 으로 입력받은 데이터를 dict 형태로 변환하려다 보니 코드가 복잡해졌다.
   3) 함수를 사용하지 않고서도 원하는 코드를 쉽게 구현하도록 연습이 필요하다.


## Useful code !! 
- dict 만드는 유용한 코드

    ```
    ### 1)
    t = int(input())
    d = dict((k,v) for k,v in [input().split() for i in range(t)])
    ```
    
    ```
    ### 2)
    t = int(input())
    d = {}

    for i in range(n) :
       data = input().split()
       d[x[0]] = x[1]

    ```
    
    ```
    ### 3)
    data = [("apple", 150),("banana", 200),("peach", 500)]
    d = {k:v for k,v in data}

    or 

    data = [input().split() for _ in range(t)]
    d = {k:v for k,v in data}
    ```

- print 함수를 사용하여 원하는 출력결과를 얻는 방법
   
    ```
    print(name, "=", pbook[name], sep="")
    print("%s=%s" %(name, pbook[name))]
    print("{}={}".format(name, pbook[name])
    ```























