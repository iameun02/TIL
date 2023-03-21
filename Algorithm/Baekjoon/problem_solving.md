# Beakjoon
>   

<br>

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
```python
#b2178_미로찾기
import sys
sys.stdin = open('b2178.txt')
T = int(input())
from collections import deque

for tc in range(1, T+1):
    n,m = map(int,input().split())
    graph = [list(map(int,input())) for _ in range(n)]
    #상하좌우 (행열좌표)
    dx = [-1,1,0,0]
    dy = [0,0,-1,1]


    #현재위치에서 인접한 상하좌우 가보기 (bfs) > 갈수있는곳 to_visits > bfs
    def bfs(x,y):
        #visited = [[0 for _ in range(M)] for _ in range(N)]

        to_visits = deque()
        to_visits.append((x,y))
        while to_visits:
            x,y = to_visits.popleft()
            #visited[x,y] = True
            for i in range(4): #4방향
                nx = x + dx[i]
                ny = y + dy[i]

                #미로 찾기 공간 내 이동 불가
                if nx < 0 or ny < 0 or nx >= n or ny >= m:
                    continue
                #0인경우 이동불가
                if graph[nx][ny] ==0:
                    continue
                #해당노드를 처음 방문하는 경우에만 최단거리 기록
                if graph[nx][ny] ==1:
                    graph[nx][ny] = graph[x][y] +1
                    to_visits.append((nx,ny))

        return graph[n-1][m-1]

    print(bfs(0,0))
```
```python
#b1697_숨바꼭질
def dfs(N,K):
    visited = [False] * 1000
    #to_visits = deque()
    to_visits = [N]
    cnt = 0
    while to_visits:
            current = to_visits.pop()
            if not visited[current]:
                visited[current] = True
                print(current)
                if current == K:
                    print('정답',cnt)
                    break

                # 현위치에서 동생위치 +1 지점 안에서, 2배씩 최대로 이동
                # 마지막에 한칸만 뒤로가면 되니까
                if current*2 <= K+1:
                    to_visits += [2*current]
                    cnt +=1
                else:
                    to_visits += [current-1]
                    cnt +=1
dfs(5, 17)
```