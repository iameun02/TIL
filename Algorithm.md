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





<br>
