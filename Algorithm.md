# Algorithm
>   

<br>

## Intro
1. 알고리즘 연습 url (for 코딩테스트) 

  + 사이트

     https://www.acmicpc.net/ <br>
     https://swexpertacademy.com/main/main.do <br>
     https://programmers.co.kr/ <br>
  
  + 도서 Introduction to Alogorithm


2. Work Flow <br>
   #1. 공유 Repository의 우측 code 버튼 클릭 후 http주소 복사 <br>
   #2. (alt+f11) 터미널 : git clone 복사한주소붙여넣기 <br>
   #3. 파이참 셋팅 (Tools- Terminal : bash) <br>
   #4. <br>
       ❶ ```git pull origin master``` 업데이트된 문제파일 받아오기 <br>
       ❷ ```git switch -c``` 브랜치명 <br>
         (혹시 브랜치 수정이 필요한 경우, 삭제후 재생성 <br>
	   ```git switch master``` <br>
	   ```git branch -D 잘못된브랜치명``` <br>
       확인을 위해 ```git branch```) <br>
        ❸ 문제파일 우측파일 클릭 후 내 이름으로된 파일 생성 후 문제풀기 <br>
        
     * 프로그래머스 : 제공하는 기본 소스코드를 파이참에 복붙 후, <br>
                  test를 위해 구현 함수를 호출하고, <br>
                  호출시 화면에서 제공된 샘플 입출력 데이터를 파라미터로 넣어준다. <br>

     * SWEA :
             ``` import sys
               sys.stdin =open('input.txt') ```

            소스코드를 상단에 쓰면 계속해서 input을 안넣어줘도 된다.
         	단 소스제출시 위 코드는 제거후 제출 

    ❹ 소스를 add + commit <br>
    ❺ (주의! 브랜치명으로 push) git push origin 브랜치명 <br>
    ❻ PR(Pull Request : 병합)

3. pycharm 활용
   -  디버깅 활용하기 (F7 누르면 코드를 한줄씩 실행시키며 결과확인가능) 
   



4. 소스활용
   ``` python
   1. a,b = ____.split()
   2. List 중복 제거시 : set(list) 
   3. List comprehension [i for i in range(n)]
   4. Enumerate (index를 함께 발생시켜줌)
   5. 변수명은 boolean값이 리턴될경우 is__로 시작하며, 리스트와 튜플은 복수형으로 지어준다. 함수명은 동사형
      (파이참에서 shift+F6 을 누르면 변수명을 일괄변경 가능하다.)
   6. For inx in range(N-1, -1, -1) : N개까지 끝에서부터 하나씩 차례로 읽어옴
   7. input 자료 입력받기

      a = int(input())                        정수형 변수 1개 입력 받는 예제
      b, c = map(int, input().split())        정수형 변수 2개 입력 받는 예제
      
      # map object는 list형으로 변환을 안해줘도 unpacking(쪼개주는 기능)을 해주는 특징을 가짐
      # 근데 1회용이다. 한번 소비되면 데이터가 날라가기때문에 재사용을 위해선 list로 변수 할당 후 사용해야한다.
   
      d = float(input())                      실수형 변수 1개 입력 받는 예제
      e, f, g = map(float, input().split())   실수형 변수 3개 입력 받는 예제
      h = input()                             문자열 변수 1개 입력 받는 예제


   8. for _ in range(n) 인덱스(변수)가 사용되지 않아, 필요하지 않고 반복기능만 사용할 때 간단히 쓰인다.

   9. 반복문을 활용한 자료 탐색

   * 행탐색
   For row in range(N):
      for col in range(N):
         print(matrix[row][col])

   * 열탐색
   For col in range(N):
      for row in range(N):
         print(matrix[row][col])

   * 대각탐색
   For i in range(N):
      print(matrix[i][i])

   * 역방향 대각탐색
   For j in range(N):
      print(matix[j][N-1-j])

   10. 코드구문을 중복으로 사용 해야 할때는 함수 접근 방식을 고려해본다.

   11. false (if/ if not 구문 또는 while 문 뒤에서 0 으로 처리 되는 경우)
      - None, 0, 그외 비어있는 값 모두 : 빈문자열 (''), 빈리스트([]), 빈딕셔너리 ({}), 빈set (set()) 등

   12. print(* 변수명) 
      - 변수가 리스트일 경우 리스트 안에 있는 요소들만 프린트해줌
   13. matrix 생성방법
      [[0 for in range(N)] for _ in range(N)]
      
        # 색칠하기_겹치는 부분 문제 푸는 2가지 접근법
         #1. Matrix 를 만들어서 숫자합으로 비교
         #2. 좌표를 List로 나열 후에 비교


   14. a = sum(array[left:right]) #슬라이싱한것을 sum할수 있다.
   15. max(list) #list에서 min/max 가능
   16. dictionary{key,value} 활용 = list + enumerate함수활용

   17. 초기값으로 최대/최소값 선언해주기 
      * 최소값 : 최초에 최대로 지정 Min = float('INF')
      * 최대값 : 최초에 최소로 지정 Max = -float('INF')
      * 또는  min = max = idx[0] 설정 

   18. 미래,또는 답이 있을때 효율적인 방법을 구하는 문제는 끝에서부터 답을 찾아가는 접근법을 활용한다.

   19. 고마운 파이썬 순열과 조합 
       from itertools import combinations, permutations
                              #조합          #순열
   20. 고마운 파이썬의 정렬
       객체명.sort()
   
   21. 재귀함수에서 외부변수 사용시
       a
       def():
         b
         def():
           global a #함수밖변수
           nonlocal b #함수내변수 (global이아님 주의!)

   22. list 요소 counting : dictionary 활용
     for i in range(리스트명) :
         try : dict[i]  += 1 #기존에 키값이 존재하면 1 증가
         except : dict[i] = 1 #기존에 키값이 없으면 1 입력

   23. a를 출력하고 싶을때 : a()() 
      def a():
         def b():
            return a
      return b

   ```
5. 참고
   - visualgo 사이트 :  정렬 종류 공부할 때 활용해보기
   - pythontutor 사이트
<br>

-----
## 개념

### 1. 시간복잡도
<br>
input양의 변화량이 아닌, input양에 따라 '연산의 횟수'의 변화량에 따라 '시간복잡도'를 구한다.
빅오표기법에서는 차수가 가장 큰 항만 남기기 때문에 항상 절대적인 것은 아니다. <br>

- 빅오 : 최악의 경우를 고려 <br>
- 빅세타 : 평균의 경우를 고려 <br>
- 빅오메가 : 최선의 경우를 고려 <br>
  

|빅오표기법|명칭|
|:---:|:---:|
|O(1)|상수시간|
|O(logN)|로그시간|
|O(N)|선형시간|
|O(NlogN)|로그선형시간|
|O(N²)|이차시간|
|O(N³)|삼차시간|
|O(2^𝒏)|지수시간|

<br>
[예시] #67258_보석쇼핑
<br>
  1) for 중첩 반복문을 적용시 ➡︎ O(n^2) <br>
  2) (n)*(n+1)/2 알고리즘 적용시 : ➡︎ O(1) <br>
  3) 두 포인터 접근방식 적용시 ➡︎ O(n) (정확히는 O(2n)이지만, n으로 표기) <br><br>


### 2. 자료구조 (DS) 
>데이터 보관방식 (※ 각각의 내장함수가 존재하는 것이 아니라 '개념'이다)<br>

  ① Stack <br>
     - 저장특성 : LIFO = FILO = 후입선출 <br>
     - 연산 : PUSH / POP <br>
     - 활용 : 함수 호출의 순서를 정할때 필요 <br>

    ☺︎ Stack 개념은 Python 의 List(구현체)로 구현 가능
       PUSH 기능 : 객체.append()
       POP 기능 : 객체.pop()
   
 
  ② Queue <br>
     - 저장특성 : FIFO = 선입선출 <br>
     - 연산 : ENQUE / DEQUE <br>

    ☺︎ Queue 개념 또한 Python의 List로 구현가능
       ENQUE 기능 : 객체.append()
       DEQUE 기능 : 객체.pop(0) 
         단!pop(0)의 경우는, 인덱스가 0인 자료가 한번 빠지면,
         자동으로 뒤의 자료가 앞으로 당겨지지 않으므로, 
         n개만큼 re_index하는 절차가 소모되는데 , 
         그렇게 되면 그만큼의 시간복잡도가 증가하게된다.
         (※ pop() 의 시간복잡도 : O(1), pop(0) 의 시간복잡도 : O(n))
 
         그래서 이때는 Pop(0)이 아닌 파이썬 라이브러리 deque의 
         .popleft() 함수를 가져다 사용한다.
 ```python
    from collections import duque
    객체.popleft()
   ```
	
      이는 인덱스를 직접 일일이 조정하는 것이아닌, 
      인덱스를 가리키는 화살표를 (first, last) 조정하는 방법으로 
      양끝에서 넣고 빼는 작업에 최적이다.
      
      
     
  ③ Graph : 관계를 모델링하기 위해 사용되는 모델 <br>
     [그래프의 구성요소] <br> 
     
 - Node = Vertex = 정점
 - Edge = 간선
 - 가중치 <br>
       1) 그래프 중에 사이클이 없는 그래프 : Tree <br>
       2) 그래프 중에 사이클이 있는 그래프 : Graph <br>
- 방향 : 무향: 쌍방향 / 유향 : 단방향 <br>
         * 탐색경로 코드화<br>
           ```dict(key: 노드의 번호, value : 튜플(연결노드,가중치) 또는 리스트 [연결노드,가중치] 가능) ``` <br>
           ``` 노드를 인덱스로 사용 [[0번사용안함],[],[],[]...] ``` <br><br>
         * 무향일 때 코드화   <br>
          ``` graph[start].append(end)``` <br>
          ```graph[end].append(start) #'순열'개념```
         <br>
         * 유향일 때 코드화 <br>
         ```graph[start].append(end) #'조합'개념```


### Array (이차원 배열)과 Adj List (인접리스트) 의 차이점

우선, RAM (Random Access Memory)이라는 물리적인 저장공간에는 <br>
'Random Access'란 말 그대로 들어오는 자료들을 메모리 내에 뒤죽박죽 채운다. <br>
(실행 중인 크롬탭들, 카톡, 파이썬 등..) <br>
(※ 메모리 주소값 확인 함수: id(객체명) ) <br><br>

배열은 이러한 메모리 공간 상에서 물리적인 위치가 보장 되어야 한다. <br>
즉, 배열의 자료끼리 물리적 공간에 인접하여 함께 위치해야 한다. <br>
그런데 만약 배열의 크기가 확장 되어야 할 때,  <br>
확장 되어야하는 RAM에서의 물리적인 위치를 이미 다른 자료가 사용 중이라면 <br>
배열의 조정이 불가능하다. <Br>
이러한 배열의 특성으로 배열은 크기가 사전에 정해져있고, <br>
리스트는 크기가 사전에 정의되지 않는다. <br>
(그래서, 실제 코딩시 배열을 초기값을 9999칸로 잡아 놓는 경우가 있다.) <Br>

``` 🤓Python Tutor 사이트를 활용하여 자료의 저장구조에 대해 조금 더 시각적으로 확인 가능하다.```


반면, 리스트의 경우는 다르다. <Br>
리스트의 요소가 만약 [1,2,3]이라면, 각각의 요소는 실제 메모리에서 제각각 위치하고 있다. <Br>
단 요소들은 본인의 이전자료주소,다음자료주소값을 가지고 있어서 서로를 연결시켜준다. <br>
(주소 값 외에 인덱스 값도 별도로 가지고 있다.) <br>그래서 List는 사실 Linked List라고 불린다.


결론 : Array 길이 조절불가, List는 가능하기 때문에 <br>
Node 수를 정확히 알때 (변할일이 없을 때)는 Array를 사용하고, <br>
List 안에 몇개가 들어올지 모를 때 (탐색을 해봐야 알때)는 List를 사용한다. <Br>


또한 공간의 복잡도의 관점으로 봤을 때,
Array는 노드의 개수에 영향을 받아 공간복잡도가 O(V^2),
List는 간선개수의 영향을 받아 O(E)가되어 Array가 높지만,

시간의 복잡도 관점에서는 Array가 더 효율적이다.
Adj List로 접근시에는 완전 탐색이 들어가기때문에 O(n) 의 복잡도를 가진다 (=in연산자)
반면 Array는 O(1)이다.

   
<br><br>
### 3. 알고리즘 : 문제 해결 방식

  ① BFS (너비우선탐색 Breadth First Search)
   - 행마다 하나씩 순회하며 탐색 (빨리 찾는게 답임)
   - '최단' 거리/시간 을 구하는 문제에 활용

  ② DFS (깊이우선탐색 Depth First Search)
   - 하나의 행을 끝까지 가봐야 한다
   - 경우의 수 탐색 : 끝까지 탐색 해봐야 답이 나오는 문제 
   - 시뮬레이팅은 보통 모두 DFS다 
   - 'A','B','C' 로 가질 수 있는 경우의 수 - 경우의 수는 결국 '순열' 문제다
      • 순열 ₃P₃ : 6개
      • 조합 ₃C₃ : 1개
   

Process

1. 목적지에서 마지막 위치를 POP 한다.
2. POP한 정점이 기존 방문한 적이 있는 체크한다.
   #cycle이 생길수가 있으니까, 방문여부를 체크하여 POP으로 지움
3. 방문한 적이 없다면 POP된 정점을 방문체크한다.
4. 현재 위치에서 갈수 있는 정점들을 목적지에 추가한다.

> <h3>Deque(데크)</h3> <br>
> 앞, 뒤 양쪽 방향에서 엘리먼트(element)를 추가하거나 제거할 수 있는 '양방향 큐'를 가리킨다. 데크는 양 끝 엘리먼트의 append와 pop이 압도적으로 빠르다. <br>
> 리스트(list) : O(n) 소요  vs  데크(deque) : O(1) 소요 <br>
> 무엇보다 데크를 이용하면 Stack과 Queue를 모두 구현할 수 있다. <br>
> 
> 
>  ```deque.append(item): item을 데크의 오른쪽 끝에 삽입``` <br>
   ```deque.appendleft(item): item을 데크의 왼쪽 끝에 삽입``` <br>
   ```deque.pop(): 데크의 오른쪽 끝 엘리먼트를 가져오는 동시에 데크에서 삭제``` <br>
   ```deque.popleft(): 데크의 왼쪽 끝 엘리먼트를 가져오는 동시에 데크에서 삭제``` <br>
   ```deque.remove(item): item을 데크에서 찾아 삭제``` <br>
   ```deque.rotate(num): 데크를 num만큼 회전한다(양수:오른쪽, 음수:왼쪽)``` 

<br><br>

### 4. DP (Dynamic Programming)
문제를 작은 문제로 쪼개서 기존 답을 재활용하는 방식으로 접근하기 <br>
(기억하는 프로그래밍:Memoization) <br>
DP는 1.재귀 2. Memoization 두가지 방식으로 모두 표현가능하지만 <br>
Memoization이 기억을 이용하여 연산하기 때문에 훨씬 더 빨라 DP문제에 보통 선택된다. <br>
<br>

반면 재귀함수는 DFS문제에 대신 사용될 수 있는 방법론이다. <br>
함수 호출을 하는데 사용되는 DFS 정의가 바로 '재귀'의 기능이기도 하기때문 <br>
(*bfs는 안됨)

<br><br>

### 5. Greedy
탐욕기법의 핵심은 Sort(정렬)다.

x[1] 기준으로 sorting 하기
   1) sort 활용
      routes.sort(key=lambda x:x[1]) #내림차순일때는 -x[1]
   2) sorted 활용 
      sorted(users, key = lambda user:(user['age'],user['balance'])) #age, balace로 정렬

> lambda 함수란? <br>
> 짧은 일회용 함수를 함수명 선언없이 바로 사용할 때 활용 <br><br>
> ``` * 제곱함수를 만들때 아래 두 코드는 기능이 동일``` <br>
>  ``` a = lambda n: n*n ``` <br>
>  ```def square(n): return n*n```

<br>

한편, 그리디 알고리즘은 앞/뒤 상황을 연결하여 고려 하지 않고, <br>
당장의 상황에서 최선의 선택을 하고, <br>
만약 그 선택이 다음 상황에 만족되지 않을시, <br>
최초 상황처럼 동일한 기준을 반복하여 한번 더 갱신/적용하는 식으로 <br>
활용이 되기 때문에, 알고리즘을 적용할 수 있는 유형이 한정적이다. <br>

[문제유형별 적용가능여부]
  * 0 - 1 : all or nothing 문제는 탐욕적 방법으로 최적해 구할 수 없음
    - 이때의 최적해는 '조합'으로 모든 경우의 수를 찾아 구해야됨. <br>
    - 참고 : 원소의 수가 n인 집합의 부분집합은 2^n
  * Fractional : 부분집합이 가능한 경우 -> 탐욕적 방법 사용가능
   
<br><br>

### 6. Heap

>Tree (Cycle 이 없는 그래프) <br>
Heap : Tree에서 특정 특성을 가진 트리 <br>
- heap은 완전 이진트리다
  > 이진트리의 특성 <br>
   1~N까지의 번호 순서대로 이진 트리가 생성되었을때, <br>
    ```V번째 자식 노드들 번호 : V*2, V*2+1``` <br>
    ```V번째 부모 노드 번호 : V//2``` <br><br>
   차수 : 자식노드의 개수 <br><br>
   <순회 종류> <br>
   전위순회 : 자손노드보다 루트노드 먼저 방문 <br> 
   중위순회 : 왼쪽자손 > 루트 >오른쪽 <br>
   후위순회 : 루트보다 자손을 먼저 방문 <br>

- 최대힙 : 루트가 언제나 제일 커야함, 서브트리에서도 마찬가지 
- 최소힙 : 루트가 언제나 가장 작아야됨, 서브트리에서도 마찬가지
- 시간복잡도 :
   * heap은 삽입, 탐색 : O(logn) > 정렬이 아님, 젤 최상 루트값만 조정 해주는 것!
      heapify = O(n) <br>
      heapq.pop : O(logn) <br>
      heapq.push = O(logn) <br>
      
   * list는 삽입 O(1), 탐색: O(n)
   * 파이썬 정렬 sort() : O(nlogn)
  
- 힙활용 소스코드
   ```python
   #리스트에서 최소합 구하기 (p121688_신입사원교육문제)
   import heapq

   #기존 리스트를 최소힙으로 만들겠다.
   heapq.heapify(리스트명)

   P1 = heapq.heappop(리스트명)
   #최소힙에서 최소값 pop (가장 낮은 값)
   P2 = heapq.heappop(리스트명)
   #최소힙에서 두번째로 최소값 pop
   P3 = P1 + P2

   heapq.heappush(리스트명,P3)
   heapq.heappush(리스트명,P3)
   ```


이처럼, 
최대/최소 문제는 힙의 시간복잡도를 이길 수 없다. <br>  

다만, heapq 자체는 최소힙만 지원을 하기때문에 <br>
최대힙을 이용하기 위해서는 음수화로 알고리즘 수행 후, <br>
```리스트명2 = list(map(lambda x:-x, 리스트명))``` <br>
맨 마지막에 다시 마이너스로 부호를 바꿔서 return 하는 식으로 활용된다. <br><br>





### 7. 참고_객체 In Python

모든 파이썬 프로그래밍은 객체와 객체간의 상호작용으로 설명할 수 있다. <br>
.함수 = 다 메서드
파이썬에서 연산자 / 예약어 외엔 거의 모두 객체로 표현된다. <br>
파이썬 객체에는 ```1급객체``` 유형 밖에 없는데, (1급)객체의 조건은 3가지다. <br>
1. 변수로 할당 가능
2. 인자로 넘기기 가능
3. 함수의 리턴 가능

이러한 관점에서 함수 또한 ```1급 객체```다. <br>
함수의 부모클래스 확인을 해보면 function으로 나오는데,<br>
(```부모클래스 확인방법 type()```) <br>
함수는 function 클래스의 객체인 것이다. <br>





---
<br>

## 문제풀이

* <h3>SWEA</h3>
   
   ```python
   #1945_간단한 소인수분해

   import sys
   sys.stdin = open('input.txt')


   T = int(input())

   for tc in range(1, T+1):
      N = int(input())
      num = [2,3,5,7,11]
      cnt = [0,0,0,0,0]
      for i in range(len(num)):
         while True: # '0' 즉 값이 False가 될 때 까지 무한루프 돌리기
               if N % num[i] == 0: # i로 소인수분해 되는 경우라면
                  N = N // num[i] # i로 나누어 N에 몫을 남기어 준다.
                  cnt[i] += 1 # i cnt에 +1 증가
               else:
                  break
      print(f'#{tc} {cnt}')
   ```

   ```python
   #2001_파리퇴치
   import sys
   sys.stdin = open('input.txt')

   T = int(input()) #테스트케이스 개수

   for tc in range(1, T + 1):
      N, M = map(int,input().split())
      array = [list(map(int, input().split())) for _ in range(N)]
      max = 0


      for i in range(N-(M-1)): #초기 셀 선택 (가로)
         for j in range(N-(M-1)):  #초기 셀 선택(세로)

               sum = 0
               for a in range(M): #값 순회 (가로)
                  for b in range(M): #세로
                     sum += array[i+a][j+b] #i,j를 더함으로써 시작점 좌표를 지정해줌 (M이 2일때 a,b는 0,1)
                  if sum > max:
                     max = sum

      print(f'#{tc} {max}')
   ```
   ```python
   #5789_현주의상자바꾸기
   import sys
   sys.stdin = open('input.txt')


   T = int(input())

   for tc in range(1, T+1):
      N, Q = map(int,input().split())
      array = [0 for _ in range(N+1)]


      for i in range(1, Q+1):
            a,b = map(int,input().split())
            for j in range (a-1, b):
                  #print(i)
                  array[j] = i
      print(array)
    ```

    ```python
    #4835_구간합
    import sys
    sys.stdin = open('input.txt')

    T = int(input()) #테스트케이스 개수

    for tc in range(1, T+1):
      N,M = map(int,input().split())
      array = list(map(int, input().split()))


      ''' Make prefix sum array '''
      summation = 0 #초기값
      prefix_sum = [0] #접두사합 리스트
      max = 0

      for i in array:
         summation += i
         prefix_sum.append(summation)
      #print(prefix_sum)

      ''' Get interval sum ''' #M 이 구간길이
      for num in range(1, N+1): #1부터 10까지
         left = num
         right = num + (M-1)
         if right <= N: #right의 최대가 len(array)
               inter_sum = prefix_sum[right] - prefix_sum[left - 1]
         else:
               if inter_sum > max:
                  max = inter_sum
                  print(f'#{tc} {max}')
   ```
   ```python
   #4834_숫자카드

   import sys
   sys.stdin = open('input.txt')

   T = int(input())

   for tc in range(1, T+1):
      N = int(input())
      num = list(input()) #구분자가 없는 문자열의 경우 list로 변환시 문자열 하나씩 요소로 저장
      dict = {}
      max = 0
      
      ### 리스트 요소 카운트 하는 방법 ###
      for i in num:
         if i in dict: #key로 value 찾기 (dict.get(i)도 가능)
               dict[i] += 1
         else:
               dict[i] = 1


      for k, v in dict.items():
         if v >= max: # 동등한 값이 존재할 경우, 등호가 있으면 뒤에 위치한 숫자, 없으면 앞에 위치한 숫자가 추출됨
               max = v
               ans = [k,v]
      print( f'#{tc} {ans[0]} {ans[1]}')

   ```

   ```python
   #s4871_그래프 경로
   
   import sys
   sys.stdin = open('input.txt')

   T = int(input())

   for tc in range(1, T+1):
      V, E = map(int, input().split())
      # 빈 인접 리스트 그래프 생성
      graph = [[] for _ in range(V+1)]
      #0번 인덱스는 사용안할거니까 V+1로 만들어준다.

      # 간선 입력
      for _ in range(E):
         start, end = map(int, input().split())
         graph[start].append(end)
         # 양방향(무향)그래프 일 경우 아래 줄 추가
         #graph[end].append(start)
      S, G = map(int, input().split())
      print(graph)

      def dfs():
         # S => G 로 갈 수 있는가?
         # DFS
         # 방문 여부
         visited = [False for _ in range(V+1)]
         # 목적지
         to_visits = [S]

         while to_visits:
               # 현재 위치 = 목적지들에서 마지막
               current = to_visits.pop()
               # 현재 위치를 방문한 적이 없다면,
               if not visited[current]:
                  print(current)
                  # 현재 위치 방문 체크
                  visited[current] = True
                  # 현재 위치에서 갈 수 있는 정점들을 목적지들에 추가
                  to_visits += graph[current]
      #dfs()

      def bfs():
         from collections import deque

         # 방문 여부
         visited = [False for _ in range(V + 1)]
         # 목적지
         to_visits = deque()
         to_visits.append(S)


         while to_visits:
               # 현재 위치 = 목적지들에서 마지막
               current = to_visits.popleft()
               # 현재 위치를 방문한 적이 없다면,
               if not visited[current]:
                  print(current)
                  # 현재 위치 방문 체크
                  visited[current] = True
                  # 현재 위치에서 갈 수 있는 정점들을 목적지들에 추가
                  to_visits += graph[current]

      bfs()
   
   # ☻ DFS : 도착한 노드의 '연결된 노드들 중 마지막 노드'를 계속 꼬리물기 식으로 타고 끝까지 들어가며 하나씩 탐색 ❯ 연결의 끝점까지 도달했는데 값을 못 찾을 경우 Back!

   # ☻ BFS : 도착한 노드에 연결된 노드를 모두 탐색 후, 없으면 왼쪽 연결 노드를 물고 이동, 이동하여 도착한 노드에 연결된 노드를 모두 탐색 후 없으면 왼쪽 연결 노드를 물고 이동, 이과정을 반복, 연결이 없는 노드에 도착시 Back!
   ```
   
   
   ```python
   #s4873_반복문자지우기
   
   import sys
   sys.stdin = open('input.txt')

   T = int(input())


   for tc in range(1, T+1):
      string = list(input())
      answer =[]   #빈 리스트 : false

      for s in string:
         if answer and s == answer[-1]: # 리스트가 비어있지 않고, 끝자리 인덱싱과 s가 같다면
               answer.pop() #리스트에서 제거
         else:
               answer.append(s)  #리스트에 추가

      print(f'#{tc} {len(answer)}') #len함수로 list 요소세기



   ```
   
   ```python
   #s4866_괄호검사

   import sys
   sys.stdin = open('input.txt')

   T = int(input())

   for tc in range(1, T+1):
      string = list(input())
      brace = 0 #중괄호
      braket = 0 #소괄호

      for i in string:
         if i == '{':
               brace +=1
         elif i == '}':
               brace -=1
         elif i == '(':
               braket +=1
         elif i == ')':
               braket -=1
      if brace ==0 and braket ==0:
         print(f'#{tc} {0}')
      else:
         print(f'#{tc} {1}')
   #참고 : 문자열 포함여부는 한번에 if char in '(){}'로 표현가능
   ```
   ```python
   #s4837_부분집합의합 (복습필요!)
   #방법1_itertools
      import sys
      sys.stdin = open('input.txt')


      #                        조합           순열
      from itertools import combinations, permutations

      T = int(input())

      for tc in range(1, T+1):
         N, K = map(int, input().split())
         numbers = [i for i in range(1, 13)]
         count = 0

         for case in combinations(numbers, N): #numbers 원소로 N개 원소의 조합만들기
            if sum(case) == K:
                  count += 1

         print(f'#{tc} {count}')

   #방법2_recursive(재귀함수)
      import sys
      sys.stdin = open('input.txt')


      def dfs(idx):
         global count

         # 현재 idx 가 numbers의 길이와 같다 => 부분 집합 완성
         if idx == len(numbers):
            # 조건을 만족했다면, count 추가
            if len(subset) == N and sum(subset) == K:
                  count += 1
            return

         subset.append(numbers[idx])
         dfs(idx+1)
         # visited[idx] = True

         subset.pop()
         dfs(idx+1)
         # visited[idx] = False


      T = int(input())

      for tc in range(1, T+1):
         N, K = map(int, input().split())
         numbers = [i for i in range(1, 13)]

         # 부분집합 / 포함 여부 둘 중에 하나만 있어도 됨
         # 부분 집합
         subset = []
         # 포함 여부
         # visited = [False] * 12

         count = 0
         dfs(0)
         print(f'#{tc} {count}')

   ```
   ```python
   #s4869_종이붙이기(복습하기!)
   import sys
   sys.stdin = open('input.txt')

   T = int(input())

   #재귀
   def make_square(n):
      if n == 1: #Base Case (재귀문은 더이상 깊이 탐색하지 않도록 root역할을 할 Base Case지정이 필요하다.)
         return 1
      elif n == 2: #Base Case
         return 3

      # Dynamic Programming => DP => 문제를 작은 문제로 쪼개서 접근하기
      return make_square(n-1) + make_square(n-2) * 2 #점화식 (DP는 관계 속 규칙을 찾아내는게 중요)

   #Memo
   def make_square2(n):
      # 최적화 => memoization => 기억 하기
      answers = [0, 1, 3]

      if n <= 2:
         return answers[n]

      for i in range(1, n+1):
         x = answers[i-1]
         y = 2 * answers[i-2]
         answers.append(x+y)

      return answers[n]


   for tc in range(1, T+1):
      w = int(input()) // 10
      print(f'#{tc} {make_square(w)}')
   ```
   ```python 
   #s1209_sum

   import sys
   sys.stdin = open('input.txt')

   for tc in range(10): #tc = 10개
      T = int(input())
      arr = []

      for i in range(100):
         array =list(map(int,input().split()))
         arr.append(array)


      #가로
      max_r = 0
      for i in range(100): #100행 반복
         summation = 0
         for j in range(100): #100열 반복하여 합산
               summation += arr[i][j]

         if summation > max_r:
               max_r = summation

      #세로
      max_c = 0
      for i in range(100):  # 100행 반복
         summation = 0
         for j in range(100):  # 100열 반복하여 합산
               summation += arr[j][i]
         if summation > max_c:
               max_c = summation


      # 대각선 \,/
      max_d = 0
      for i in range(100):
         sum1 = 0
         sum2 = 0
         sum1 += arr[i][i]
         sum2 += arr[i][99 - i]
      if max(sum1, sum2) > max_d:
         max_d = max(sum1, sum2)

      print("#{} {}".format(T, max(max_r, max_c, max_d)))
   ```
   ```python
   #s5202_화물도크

   sys.stdin = open('input.txt')

   T = int(input())
   for tc in range(1, T+1):
      n = int(input())

      #정렬
      anw =[]
      for i in range(n):
         anw.append(list(map(int,input().split())))
         #result = list(map(int,input().split()))
      anw.sort(key= lambda x:x[1]) #작업이 빨리 끝나는 순으로 정렬
      print(anw)

      load = 0
      cnt = 0
      for s,e in anw:
         if s >= load:
               load = e
               cnt +=1

      print(cnt)
   ```
   ```python
      #s5209_최소생산비용 (복습하기, 특히 순열문제를 재귀로 바꾸어 푸는방법 중요_재귀풀이로 백트래킹이 가능하기 때문에 구현방법 익숙해져야함)

      import sys
      sys.stdin = open('input.txt')
      from itertools import permutations

      T = int(input())

      for tc in range(1, T+1):
         N = int(input())
         matrix = [list(map(int,input().split())) for _ in range(N)]
         #print(matrix)
         answer = float('inf')

      # #1. 순열풀이
         for case in permutations(matrix,N):
            sum = 0
            for i in range(N):
                  sum += case[i][i]
            answer = min(answer, sum)

         print(f'#{tc} {answer}')

      #2. 재귀풀이
         def solution(matrix):
            result = float('inf')
            # 공장수
            fac_cnt = len(matrix)
            # 제품수
            prod_cnt = len(matrix[0])
            # 공장포함여부
            visited = [False for _ in range(fac_cnt)]

            def dfs(prod_idx, total):
                  nonlocal result

                  if prod_idx == prod_cnt:
                     result = min(total, result)
                     return

                  for fac_idx in range(N):
                     if not visited[fac_idx]:
                        visited[fac_idx] = True
                        #new_total = 지금까지 생산비용 + 이번선택에 의한 생산비용
                        new_total =  total + matrix[prod_idx][fac_idx]
                        #Backtraing(가지치기) : new_total이 result보다 작을때만
                        if new_total < result:
                              dfs(prod_idx + 1, new_total) #+1이필요
                        visited[fac_idx] = False

            dfs(0, 0)
            return result

         print(solution(matrix))
      
   ```



* <h3>Programmers</h3>

   ```python
   #p12928_약수의 합

   def solution(n):
      answer = 0

      for i in range(1,n+1):
         if n%i ==0:
               answer += i
         print(answer)
      return answer
   ```
   ```python
   #p92334_신고 결과 받기

   def solution(id_list, report, k):
     a =[]
     b = []
     answer =[]

     for i in set(report):
         a.append(i.split(' ')[1])

     for j in id_list:
          if a.count(j) >= k:
              b.append(j)

     answer = [i.split()[0] for i in set(report) if i.split()[1] in b]

     return [answer.count(i) for i in id_list]



   # [2,1,1,0]
      print(solution(
                     ["muzi", "frodo", "apeach", "neo"]
                     ,["muzi frodo", "apeach frodo", "frodo neo", "muzi neo", "apeach muzi"]
                     ,2))
   # [0,0]
      print(solution(
                  ["con", "ryan"]
            ,["ryan con", "ryan con", "ryan con", "ryan con"]
            ,3))

   ```
   ```python
   #p121687_실습용로봇

   def solution(command):
    loc = [0, 0]
    direction = [[0, 1], [1, 0], [0, -1], [-1, 0]]
    chk = 0

    for i in command:
        chk %= len(direction)
        if i =="G" :
            loc[0] += direction[chk][0]
            loc[1] += direction[chk][1]
        elif i == "L":
            chk -= 1
        elif i == 'R':
            chk += 1
        elif i == "B":
            loc[0] -= direction[chk][0]
            loc[1] -= direction[chk][1]

    return loc

   print(solution("GRGRGRB"))
   ```
   ```python
   #p71_송아지찾기
   #bfs이용

   def solution(s,e):
      #목적지가 뒤에 위치하면 가까이가자
      if s < e:
         count = (e-s)// 5 #최대 보폭 5로 나눠줌(간만큼 카운팅)
         s += count * 5 #가까워진 만큼 출발점 갱신

      #목적지가 뒤에 있으면 뒤로 후진
      elif s > e:
         count =0


      #방문여부
      from collections import deque
      visited = [False for _ in range(10001)] #좌표 10000까지 갈수있음
      #목적지
      to_visits = deque() #데크사용
      to_visits.append(s)


      while to_visits:
         #목적지 수 만큼 반복
         for _ in range(len(to_visits)):
               #현재 위치 갱신
               current = to_visits.popleft()
               print('현위치',current)
               #방문여부 체크
               if not visited[current] :
                  #방문체크
                  visited[current] = True
                  #e 도달 했으면 끝
                  if current == e:
                     return count
                  # 도달하지 못했으면 이동가능한 선택지들 : 해당좌표에서의 연결좌표 역할 >탐색 >없으면 왼쪽 꼬리 물고 이동
                  for nxt in [current-1, current+1, current+5]:
                     if 0< nxt <= 10000 and not visited[nxt]:
                           to_visits.append(nxt)

         count +=1
      return count

   #3
   print(solution(5, 14))
   #5
   print(solution(8, 3))

   ```

   ```python
   #p87946_피로도 (순열(조합영역)과 재귀(조건만족판단)를 활용해 풀이)

   from itertools import permutations

   def solution(k, dungeons):
      result = []
      cnt =0
      def rc(idx,k):
         nonlocal result
         nonlocal cnt

         if idx >= 3:
               return cnt

         if i[idx][0] <= k:
               k -= i[idx][1]
               cnt += 1
               rc(idx + 1,k)


      for i in list(permutations(dungeons,3)):
         rc(0,80)
         result.append(cnt)
         if max(result) == 3: #가능한 최대의 값을 이미 만족시켰으면 반복문 중단
               break
         cnt= 0
      print(max(result)) 


   print(solution(80,[[80,20],[50,40],[30,10]]))
   ```
   ```python
   #p121683_외톨이알파벳

   ##Review: try-except 문은 예외처리용으로 코테에는 '지양'
   ## index + 1 이 오류나는걸 처리하기 위해선 , index를 사용하지말고 range를 사용해서 out of range 에러가 발생안하도록 코딩
   ## 또는 마지막 인덱스는 if문으로 건너뛰게끔 해줄수도 있음

   def solution(string):
      dict = {}
      visited = {}
      for i in list(string):
         visited[i] = False
      result =[]


      for idx,i in enumerate(string): #문자열은 enumerate 사용시 list(string)로 안감싸줘도 된다!
         #등장횟수 처리
         try:
               dict[i] += 1
         except:
               dict[i] = 1

         #방문횟수 및 구간이 True인가? pop
         if dict[i] >=2 and visited[i]:
            result.append(i)

         #해당 요소 구간 처리
         try:
               if i == list(string)[idx+1]: #다음요소가 동일하면 아직 바꾸지말고
                  visited[i] = False
               else: #동일하지 않으면 바꾸기
                  visited[i] = True
         except:pass



      if result == [] :
         return 'N'
      else:
         return set(result)




   print(solution("edeaaabbccd"))
   print(solution("eeddee"))
   print(solution("string"))
   print(solution("zbzbz"))
   ```
   ```python
   #p86971_전령망둘로 나누기 (재풀이필요..;ㅁ;)

   def solution(n, wires):
      # 간선연결정보
      edge = [[] for _ in range(n+1)]
      for i,j in wires:
         edge[i].append(j)
         #edge[j].append(i) _이것도 포함해야하는데..
      # 노드방문여부
      visited = [False] * (n+1)
      min = float('inf')

      for i in range (len(visited)-1):
         visited[i] = True
         to_visit = [1]
         cnt_v1 = 0
         cnt_v2 =0
      # 노드 카운팅(DFS)
         while to_visit:
               current = to_visit.pop()
               # true를 만났을 때
               if visited[current-1]:
                  cnt_v1 +=1
               else:
                  to_visit += edge[current]
                  cnt_v1 +=1
                  #print(to_visit)

         cnt_v2 = n - cnt_v1
         if abs(cnt_v1 - cnt_v2) < min:
               min = abs(cnt_v1 - cnt_v2)

         visited[i] = False

      return min



   print(solution(9 ,[[1, 3], [2, 3], [3, 4], [4, 5], [4, 6], [4, 7], [7, 8], [7, 9]]))
   print(solution(4 ,[[1,2],[2,3],[3,4]] ))
   print(solution(7, [[1,2],[2,7],[3,7],[3,4],[4,5],[6,7]]))
   
   ```
   ```python
   #p42884_ 단속카메라

   #[풀이1 : 집합이용]
   def solution(routes):

      result = [[] for i in range(len(routes))]

      #차마다 달린 주행거리를 각각 list로 만들기
      i=0
      for s,e in routes:
               result[i] = [j for j in range(s,e+1)]
               i+=1

      # 집합을 활용하여 차선마다 주행거리를 비교해서 중복구간이 있는 차선들은 모두 True로 체크후,
      # 카메라 1대 설치 (cnt +=1)
      cnt = 0
      visited = [False] * len(routes)
      for i in range(len(result)):
         if not visited[i]:
               for j in range(len(result)):
                  if set(result[i]) & set(result[j]):
                     if j == i:
                           continue
                     visited[j] = True
                     visited[i] = True

               if visited[i] == True: #중복구간이 있는 차선그룹당
                  cnt +=1  #카메라 1대 설치

      # 중복구간이 없는 차들은 차당 카메라 1대설치
      left =[1 for x in visited if x == False]
      
      return cnt + sum(left)

   print(solution([[-20,-15], [-14,-5], [-18,-13], [-5,-3]]))
   print(solution([[1,3], [3,4], [5,6]]))


   #[풀이2: 그리디 이용]
   def solution(routes):
      answer = 0
      routes.sort(key=lambda x: x[1])
      camera = -30001
      print(routes)
      cnt = 0
      for i in range(len(routes)):
         s, e = routes[i]
         if camera < s:
               cnt += 1
               camera = e
      answer = cnt

      return answer


   print(solution([[-20, -15], [-14, -5], [-18, -13], [-5, -3]]))

   ```
   ```python
   #p121684_체육대회
   
   from itertools import permutations ,product
   def solution(ability):
      answer = 0

      for case in permutations(ability, len(ability[0])): #ability 내 리스트로 특정 자리 수에 맞게 생성 가능한 순열 경우의 수를 모두 뽑는다.
         #(두자리인 경우 리스트 2개씩 비교)
         sum = 0 
         for i in range(len(case)): # 주어진 case마다  
               sum += case[i][i] #각 i열 list의 i번째 요소를 합산 (순열이기때문에 이경우만 고려하면된다.)
         answer = max(answer, sum)

      return answer


   print(solution([[40, 10, 10], [20, 5, 0], [30, 30, 30], [70, 0, 70], [100, 100, 100]]))
   print(solution([[20, 30], [30, 20], [20, 30]]))
   ```
   
   ```python
   #p121688_신입사원교육(꼭풀어보기..!, dfs+sort방법으로 풀이는 가능하지만 시간초과발생 > heap문제)
   from itertools import combinations

   def solution(ability, number):
      n = len(ability)
      minimum = float('INF')
      
      #1. dfs풀이
      def dfs(x, arr):
         nonlocal minimum

         if x == number:
               total = sum(arr)
               if total < minimum:
                  minimum = total
               return

         for case in combinations(range(n), 2):
               copy_arr = arr[:]
               p1, p2 = case
               copy_arr[p1] = copy_arr[p2] = copy_arr[p1] + copy_arr[p2]

               if sum(copy_arr) > minimum:
                  continue

               dfs(x+1, copy_arr)

      dfs(0, ability)
      return minimum

      #2. heap풀이
      def solution(ability, number):
         heapq.heapify(ability)
         print(ability)
         for _ in range(number):
            p1 = heapq.heappop(ability)
            p2 = heapq.heappop(ability)
            p3 = p1 + p2
            heapq.heappush(ability, p3)
            heapq.heappush(ability, p3)

         print(sum(ability))

   print(solution([10, 3, 7, 2], 2))
   print(solution([1, 2, 3, 4], 3))
   ```
* <h3> Baekjoon </h3>
```python
#b1260_ DFS와 BFS
import sys
sys.stdin = open('input.txt')

T= int(input())

for tc in range(1, T+1) :
    N, E, S = list(map(int, input().split()))
    dict = [[] for _ in range(N+1)] #node + 1
    link = [list(map(int,input().split())) for _ in range(E)]

    # 간선정보
    for k, e in link: #양방향
        dict[k].append(e)
        dict[e].append(k)


    print(dict)

    def dfs():
        to_visits = [S]
        visited = [False] * (N + 1)

        while to_visits:
            current = to_visits.pop()
            if not visited[current]:
                print(current)
                visited[current] = True
                to_visits += sorted(dict[current], reverse=True) #스텍이니 역순정렬

    #dfs()

    from collections import deque
    def bfs():
        to_visits = deque()
        to_visits.append(S)
        visited = [False] * (N + 1)

        while to_visits:
            current = to_visits.popleft()
            if not visited[current]:
                print(current)
                visited[current] =True
                to_visits += sorted(dict[current]) #정렬
    bfs()

```
```python
#b2644_촌수계산

import sys
sys.stdin = open('input_b2644.txt')
T = int(input())
from collections import deque

for tc in range(1, T+1):
     N = int(input())
     S, E = list(map(int, input().split()))
     iter = int(input()) #관계
     edge = [[] for _ in range(N+1)]


     for i in range(iter):
         parent, child =list(map(int,input().split()))
         edge[parent].append(child)
         edge[child].append(parent)
     print(edge)

    #큐의 반대방향개념, 꼬리물고 올라가기
     def bfs():
          visited = [False]* (N+1)
          to_visits = deque()
          to_visits.append(S)
          cnt = 0

          while to_visits:
              current = to_visits.popleft()
              if not visited[current]:
                  print(current)
                  visited[current] = True
                  if current == E:
                      break
                  for i in (sorted(edge[current],reverse=True)):
                      to_visits.appendleft(i)
                  #스텍에 담을 때 앞쪽에 붙여주기
                  cnt +=1

          # E가 방문처리가 안되있으면 -1 리턴
          if visited[E]:
              print('answer:',cnt)
          else:
              print('answer:',-1)
     bfs()

```
```python
#b2606_바이러스

import sys
sys.stdin = open('input_b2606.txt')
from collections import deque

N = int(input())
M = int(input())

graph = [[] for _ in range(N+1)]



a=  [list(map(int, input().split())) for _ in range(M)]


for s,e in a :
    graph[s].append(e)
    graph[e].append(s)
print(graph)

def bfs(S):
    visited = [False for _ in range(N + 1)]
    to_visits = deque()
    to_visits.append(S)

    cnt = 0
    while to_visits:
        current = to_visits.pop()
        #print(current)
        if not visited[current]:
            visited[current] = True
            to_visits += graph[current]
            if current ==S:
                continue
            else:
                cnt += 1
    print(cnt)

bfs(1)

```
---
<br>

## 유형별 접근방법
* <h3> 구간합 (Interval Sum) 구하기</h3>
 > 연속적으로 나열된 N개의 수가 있을 떄 특정 구간의 모든 수를 합한 값을 계산하는 문제

𝑁개의 정수로 구성된 수열과 𝑀개의 쿼리(Query)정보가 주어졌을때, <br>
각 쿼리는 [𝐿𝑒𝑓𝑡와 𝑅𝑖𝑔ℎ𝑡] 구간으로 구성된다. <br>

이때 접두사 합 개념을 이용해 빠르게 계산이 가능하다. <br>
(✓ 접두사 합(Prefix Sum): 배열의 맨 앞부터 특정 위치까지의 합을 미리 구해 놓은 것) <br><br>
접두사 합을 활용한 알고리즘 <br>
 - 𝑁개의 수 위치 각각에 대하여 접두사 합을 계산하여 𝑃에 저장
 - 구간 합은 𝑃[𝑅𝑖𝑔ℎ𝑡] - 𝑃[𝐿𝑒𝑓𝑡 - 1]이다
  
  
  * <h3>그리디</h3>
  > 현 상황에서 지금 당장 좋은 것만 고르는 방법이며 탐욕적으로 접근시에 정확한 답을 찾을수 있다는 보장이 있을때 효과적

  ```python
  #예제 3-1_최소 개수의 동전으로 거스름돈 주기

   n = 1260 #거스름돈
   count =0

   coin_types =[500,100,50,10]

   for coin in coin_types:
      
      count += n//coin
      n %= coin
   print(count)
   
    #큰 단위가 작은 단위의 배수 형태이므로 가장큰단위의 화폐부터 차례대로 거슬러 주는 작업의 아이디어가 정당하다. 

    #만약 500,400,100원의 경우라면 (무작위로 주어진 경우) 작은 단위의 동전들을 종합해 다른해가 나올수 있기때문에 그리디 알고리즘 사용불가 -> 다이나믹 프로그래밍으로 해결 
  ```
<br>

```python
#예제 3-2_큰 수의 법칙
import sys
sys.stdin = open('input.txt')


N, M, K = list(map(int, input().split()))
array = list(map(int, input().split()))
result = 0

array.sort(reverse= True)

first = array[0]
second= array[1]

#[방법1] : input양이 많아지면 비효율적
# while True: #7. 반복 수행
#     for i in range(K): #1. 최대 K번까지
#         if M == 0: #8. K번까지 수행 중에 M=0 이되면 for문 break
#             break
#         result += first #2. result에 first를 더한다.
#         M -= 1 #3. 각 수행 마다 M을 차감
#     if M ==0: #4. K번 모두 수행 후 M=0 이면 break
#         break
#     result += second #5. 그렇지 않으면 result에 second를 더해준다.
#     M-=1 #6. M을 차감해준다.
#
# print(result)

#[방법2]
count = int(M/ (K+1)) * K #반복되는 수열 K+1이 M에 몇 번 등장하는지 구하고 거기다 K를 곱하면 가장 큰 수의 등장횟수가 구해진다.
count += M % (K+1) #반복되는 수열로 나눈 나머지만큼 큰 수가 추가로 등장할 횟수를 추가하여 합산해준다.
#결국 count 변수에는 큰수의 등장 횟수를 구한 것임

result = 0
result += (count) * first #등장횟수에 큰수를 곱하여 계산
result += (M-count) * second #전체 등장횟수 -큰수등장횟수 = 두번째로 큰수 등장횟수, 얘도 횟수에 수를 곱하여 계산후 합산
print(result)
```
<br>

```python
#예제 3-3_숫자 카드 게임

import sys
sys.stdin = open('input3.txt')

M, N = map(int,input().split())

array = [list(map(int,input().split())) for _ in range(M)]
#print(array)
minimum = 0

for i in array:
    #print(min(i))
    if min(i) >= minimum:
        minimum = min(i)
print(minimum)
```
```python
#예제 3-5_1이될때까지

import sys
sys.stdin= open('input.txt')

N = 25
K =3
cnt =0

while True:
    if N % K ==0:
        N /= K
        cnt +=1
    else :
        N -=1
        cnt +=1
    if N ==1:
        break
print(cnt)
```
<br>

 * <h3>구현</h3>
  > 완전탐색(모든 경우의수를 다 계산하는 해결방법) + 시뮬레이션 (문제에서 제시한 알고리즘을 한단계씩 차례대로 직접수행)
```python
#예제 4-1_상하좌우
n = 5
M = ('R R R U D D')

x,y = 1,1
#이동할 방향을 기록해주는 변수 dx, dy
dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]
move = ['L','R','U','D']


for plan in list(M.split()):
    for i in range(len(move)):
        if plan == move[i]:
            nx = x + dx[i]
            ny = y + dy[i]
    if nx <1 or ny <1 or nx > n or ny > n:
        continue
    x,y = nx, ny

print(x,y)
```
```python
#예제 4-2_시간

n = 5
count = 0

for t in range(n+1):
    for m in range(60):
        for s in range(60):
            if '3' in str(t) + str(m) + str(s):
                count +=1

print(count)

```

```python
#예제 4-3_왕실의 나이트

input = list('b1')
row = int(input[1])
col = int(ord(input[0])) -int(ord('a')) +1 
# input의 문자에서 a 유니코드(97) 만큼을 빼줘서 차이를 이용해 10진수로 활용(a의경우 1로 만들어줌)
#ord(c)는 문자의 유니코드 숫자 값을 리턴하는 함수이다. (chr 함수와 반대)
steps = [(-2,-1), (-1,-2) ,(1,-2), (2,-1), (2,1), (1,2), (-1,2), (-2,1)]

cnt = 0
for step in steps:
    next_row = row+step[0]
    next_col = col+step[1]
    if next_row >= 1 and next_row <=8 and next_col >= 1 and next_col <=8:
        cnt +=1

print(cnt)
```

```python
# 예제 4-4_게임개발

import sys
sys.stdin = open('input4.txt')
#0 북
#1 동
#2 남
#3 서


n, m = list(map(int,input().split()))
x, y, direction = list(map(int,input().split()))
visited = [[0] * n for _ in range(m)]
visited[x][y] = 1 #현재좌표 방문처리

#방향정의
dx = [0,1,0,-1]
dy = [1,0,-1,0]


#맵
array =[]
for i in range(n):
    array.append(list(map(int, input().split())))

#왼쪽회전함수
def turnleft():
    global direction
    direction -=1
    if direction == -1:
        direction =3

count = 1 #현재위치 방문처리용 카운팅
turntime = 0
while True:
     turnleft() # 회전 및 이동
     nx = x + dx[direction]
     ny = y + dy[direction]

    # 0: 육지, 1:바다
     if visited[nx][ny] == 0 and array[nx][ny]==0:
         #방문처리 맵에도 F, 전체맵에도 F여야됨
         visited[nx][ny] = 1
         x= nx
         y= ny
         #print(visited[x][y])
         count += 1
         turntime =0 # 이동했으면 초기화
         continue
     else:
         turntime +=1

     #사면 모두 이동불가능하다면
     if turntime == 4: #후진은 경우의 수가 중복인것같은데 왜 또처리하는지..모르겠음
         # nx= x-dx[direction]
         # ny = y- dy[direction]
         # if array[nx][ny] ==0:
         #     x= nx
         #     y= ny
         # else:
        break
        turntime = 0

print(count)
```
```python
#피보나치 수열 구하기
def fibo(n):
    # 재귀로 작성하시오.
    if n <= 1:
        return n
    return fibo(n-1) + fibo(n-2)
for i in range(1, 20):
    print(fibo(i), end=' ')


'''출력 결과
1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181
'''

def fibo(n):
    # 메모이제이션(memoization)을 활용하여 작성하시오.
    fibo = [0,1]
    for i in range(2,n+1):
        fibo.append(fibo[i-1] + fibo[i-2])
    return fibo[n]

for i in range(1, 20):
    print(fibo(i), end=' ')

'''출력 결과
1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597 2584 4181 
'''
```