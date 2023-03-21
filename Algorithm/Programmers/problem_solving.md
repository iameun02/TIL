# Programmers
>   

<br>

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
   def solution(routes)
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

<br>