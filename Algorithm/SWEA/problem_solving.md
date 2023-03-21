# SWEA
>   

<br>

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

