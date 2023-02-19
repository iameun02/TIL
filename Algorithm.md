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
        
     *  프로그래머스 : 제공하는 기본 소스코드를 파이참에 복붙 후, <br>
         test를 위해 구현 함수를 호출하고, <br>
         호출시 화면에서 제공된 샘플 입출력 데이터를 파라미터로 넣어준다. <br>

     * 백준 :
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
   2. List 중복 제거시 : (set) 
   3. List comprehension
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
   ```
5. 참고
   - visualgo 사이트 :  정렬 종류 공부할 때 활용해보기
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
1) (n)*(n+1)/2 알고리즘 적용시 : ➡︎ O(1) <br>
2) 두 포인터 접근방식 적용시 ➡︎ O(n) (정확히는 O(2n)이지만, n으로 표기) <br><br>


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
* <h3>Programmers</h3>

   ```python
   #12928_약수의 합

   def solution(n):
      answer = 0

      for i in range(1,n+1):
         if n%i ==0:
               answer += i
         print(answer)
      return answer
   ```
   ```python
   #92334_신고 결과 받기

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
   #121687_실습용로봇

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
   #71_송아지찾기
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

* <h3> Baekjoon </h3>

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
<br><br><br>

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
