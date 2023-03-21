# else
>   

<br>


## 유형별 접근방법
<br>

* <h3> 구간합 (Interval Sum) 구하기</h3>
 > 연속적으로 나열된 N개의 수가 있을 떄 특정 구간의 모든 수를 합한 값을 계산하는 문제

<br>
𝑁개의 정수로 구성된 수열과 𝑀개의 쿼리(Query)정보가 주어졌을때, <br>
각 쿼리는 [𝐿𝑒𝑓𝑡와 𝑅𝑖𝑔ℎ𝑡] 구간으로 구성된다. <br>

이때 접두사 합 개념을 이용해 빠르게 계산이 가능하다. <br>
(✓ 접두사 합(Prefix Sum): 배열의 맨 앞부터 특정 위치까지의 합을 미리 구해 놓은 것) <br><br>
접두사 합을 활용한 알고리즘 <br>
 - 𝑁개의 수 위치 각각에 대하여 접두사 합을 계산하여 𝑃에 저장
 - 구간 합은 𝑃[𝑅𝑖𝑔ℎ𝑡] - 𝑃[𝐿𝑒𝑓𝑡 - 1]이다
  
  <br><br>

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
<br><br>


  * <h3>정렬</h3>
  > 선택정렬 : 가장 작은 데이터를 앞으로 보내는 과정을 N-1번 반복하며 정렬
```python
#예제 6-1_선택 정렬 

array = [7,5,9,0,3,1,6,2,3,8]

for i in range(len(array)):
    min_idx= i #초기값 : 최좌측값
    #반복문을 통해 가장 작은 값 찾고, 최좌측값과 스와이프
    for j in range(i+1, len(array)):
        if array[min_idx] > array[j]:
            min_idx = j
    array[i], array[min_idx] = array[min_idx], array[i]

print(array)
```

<br><br>

  * <h3>기타</h3>
  > 재귀함수, 메모이제이션

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