# :boom: Problem_2

---

​																														

### 사칙 연산

```python
def calc(v):
    if len(tree[v]) == 2:
        return tree[v][1]
    else:
        L = calc(tree[v][2])
        R = calc(tree[v][3])

        if tree[v][1] == '-':
            return L - R
        elif tree[v][1] == '+':
            return L + R
        elif tree[v][1] == '*':
            return L * R
        elif tree[v][1] == '/':
            return L // R


for tc in range(1, 11):
    N = int(input())
    tree = [0] * (N+1)
    for _ in range(N):
        tmp = input().split()

        tree[int(tmp[0])] = tmp

        if len(tmp) == 4:
            tree[int(tmp[0])][2] = int(tree[int(tmp[0])][2])
            tree[int(tmp[0])][3] = int(tree[int(tmp[0])][3])
        else:
            tree[int(tmp[0])][1] = int(tree[int(tmp[0])][1])

    print(f'#{tc} {calc(1)}')
```

​																													



​																					

### 물놀이를 가자

```python
# deque 사용
from collections import deque

dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]

T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())  # N: 세로크기 M: 가로크기
    arr = [input() for _ in range(N)]
    dist = [[987654321] * M for _ in range(N)] # 방문쳌 겸 거리 쳌

    Q = deque()

    for i in range(N):
        for j in range(M):
            if arr[i][j] == 'W':
                Q.append((i, j))
                dist[i][j] = 0

    while Q:                # Q가 있으면
        r, c = Q.popleft()  # 가장 앞에있는 값을 가져와!
        for i in range(4):
            nr = r +dr[i]
            nc = c +dc[i]

            if nr < 0 or nr >= N or nc < 0 or nc >= M: 
                continue
            if arr[nr][nc] == 'L' and dist[nr][nc] == 987654321:
                dist[nr][nc] = dist[r][c] + 1
                Q.append((nr, nc))

    ans = 0

    for i in dist:
        for j in i:
            ans += j

    print("#{} {}".format(tc, ans))
```

​																				

```python
# 선형큐 사용

dr = [-1, 1, 0, 0]
dc = [0, 0, -1, 1]

T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())  # N: 세로크기 M: 가로크기
    arr = [input() for _ in range(N)]
    dist = [[987654321] * M for _ in range(N)] # 방문쳌 겸 거리 쳌

    Q = [0] * (N * M)
    front = -1
    rear = -1

    for i in range(N):
        for j in range(M):
            if arr[i][j] == 'W':
                rear += 1
                Q[rear] = (i, j)
                dist[i][j] = 0

    while front != rear:
        front += 1
        r, c = Q[front]

        for i in range(4):
            nr = r +dr[i]
            nc = c +dc[i]

            if nr < 0 or nr >= N or nc < 0 or nc >= M:
                continue
            if arr[nr][nc] == 'L' and dist[nr][nc] == 987654321:
                dist[nr][nc] = dist[r][c] + 1
                rear += 1
                Q[rear] = (nr, nc)

    ans = 0

    for i in dist:
        for j in i:
            ans += j

    print("#{} {}".format(tc, ans))
```

​													

```python
# BFS
def bfs(N, M):

    front = -1
    rear = -1

    # 큐 생성
    q = [0] * (N*M)

    # visited 생성
    visited = [[0] * M for _ in range(N)]  # 거리 계산
    # 시작점 인큐, 방문 표시
    for i in range(N):
        for j in range(M):
            if arr[i][j] == 'W':
                rear += 1
                q[rear] = (i, j)
                visited[i][j] = 1
    # 큐가 비어 있지 않으면,
    while front != rear:
        front += 1       # 디큐
        i, j = q[front]
        # 모든 칸을 탐색하므로 i, j에 대해 처리할 것은 없음.
        for di, dj in [[0,1], [1,0], [0,-1], [-1,0]]:
            ni, nj = i + di, j + dj
            if 0<= ni< N and 0 <= nj < M and visited[ni][nj] == 0:
                # 인큐
                rear += 1
                q[rear] = (ni, nj)
                # 방문표시
                visited[ni][nj] = visited[i][j] + 1
    s = 0
    for i in range(N):
        for j in range(M):
            s += visited[i][j]
    return s - (N*M)

T = int(input())

for tc in range(1, T+1):
    N, M = map(int, input().split())
    arr = [input() for _ in range(N)]
    # ['WLL','LLL']
    # arr = [list(input()) for _ in range(N)]
    # [['W','L','L'],['L','L','L']]

    print(f'#{tc} {bfs(N,M)}')


```

​										

​																			

### 탈주범 검거

```python

dr = [0,1,0,-1]
dc = [1,0,-1,0]

# 터널 구조물
pipe =[
    [0,0,0,0],
    [1,1,1,1],
    [0,1,0,1],
    [1,0,1,0],
    [1,0,0,1],
    [1,1,0,0],
    [0,1,1,0],
    [0,0,1,1],
]

T = int(input())
for tc in range(1, T+1):
    N, M, R, C, L = map(int, input().split())

    # 지도 정보
    tunnel = [list(map(int, input().split())) for _ in range(N)]
    visited = [[0] * M for _ in range(N)]

    Q = [(R, C)]
    visited[R][C] = 1

    ans = 0

    while Q:
        r, c = Q.pop(0)
        ans += 1

        if visited[r][c] >= L:
            continue

        # 사방향 탐색
        for d in range(4):
            curr_p = tunnel[r][c]
            # 현재 바라보는 방향으로 길이 없으면
            if pipe[curr_p][d] == 0:
                continue

            nr = r + dr[d]
            nc = c + dc[d]

            # 다음 좌표가 맵을 벗어났다면.
            if nr < 0 or nr >= N or nc < 0 or nc >= M:
                continue

            nd = (d + 2) % 4
            np = tunnel[nr][nc]

            # 방문을 했거나, 다음 좌표의 파이프가 현재좌표와 연결되지 않는다면,
            if visited[nr][nc] or pipe[np][nd] == 0:
                continue

            visited[nr][nc] = visited[r][c] + 1
            Q.append((nr,nc))

    print("#{} {}".format(tc, ans))
```



### 수영장

```python
T = int(input())
for tc in range(1, T+1):
    D, M, TM, Y = map(int, input().split())       # 1일, 1개월, 3개월, 1년
    plan = list(map(int, input().split()))

    DP = [0] * 12                                 # DP는 해당 달까지의 가장 효율높은 지불 방법
    DP[0] = min(D * plan[0], M)                   # 1월 (1일 vs 1개월)
    DP[1] = DP[0] + min(D * plan[1], M)           # 2월 (1월 비용 + 1일 vs 1개월)
    DP[2] = min(TM, DP[1] + min(D * plan[2], M))  # 3월 (3개월 vs 2월까지의 지불 + 1일, 1개월 이용권 중 최솟값 비교)

    for i in range(3,12):                         # 4월 부터는 3개월 전 비용 + 3개월 이용권 vs 직전 비용 + 1일,1개월 최솟값 비교
        DP[i] = min(DP[i-3] + TM, DP[i-1] + min(D * plan[i], M))
    ans = min(DP[11], Y)                          # 12월까지의 값과 1년 이용권 비교
    print(f'#{tc} {ans}')
```

​												

```python
def f(n, s):   # n월, s 이전까지의 비용
    global minV

    if n > 12:
        if minV > s:
            minV = s
    elif minV < s:                                    # 시간을 줄이기 위해 중간에 1년 이용권 보다 큰 경우.
        return
    else:
        f(n+1, s + min(swim[n]*price[0], price[1]))   # n월에 1개월치만 결제하는 경우
        f(n+3, s + price[2])                          # n월에 3개월 이용권을 결제하는 경우

T = int(input())
for tc in range(1, T+1):
    price = list(map(int, input().split()))
    swim = [0] + list(map(int, input().split()))      # 1~12월을 인덱스로 사용
    minV = price[3]                                   # 1년 이용권을 최솟값으로.
    f(1,0)

    print(f'#{tc} {minV}')

```

​													

```python

# cost: 이전 달 까지의 계산 결과, m 현재 내가 보낼 결과
def calc(cost, m):
    global min_cost
    if m > 12:
        if min_cost > cost:
            min_cost = cost
        return
    # 1일권
    calc(cost + d*month[m], m +1)
    # 1달권
    calc(cost + m1, m +1)
    # calc(cost + min(d*month[m], m1), m+1)
    # 3달권
    calc(cost + m3, m +3)



T = int(input())

for tc in range(1, T+1):
    d, m1, m3, y = map(int, input().split())
    month = [0] + list(map(int, input().split()))

    min_cost = y

    calc(0,1)
    print(f'#{tc} {min_cost}')

```

​																					

​																																												

### 등산로 조성

```python
def f(i, j, N, K, c, s):     # i, j 칸이 등산로에 포함, 깎는 횟수 c 이전까지의 길이 s
    global maxV

    if maxV < s + 1:
        maxV = s + 1    # 최대 등산로 길이 갱신
    v[i][j] = 1         # 현재의 등산로에 포함된 칸
    # 주변 칸 탐색
    for di, dj in [[0, 1],[1, 0], [-1, 0],[0, -1]]:
        ni, nj = i +di, j + dj
        if 0 <= ni < N and 0 <= nj < N and v[ni][nj] == 0:
            if arr[i][j] > arr[ni][nj]:
                f(ni, nj, N, K, c, s+1)
            elif c == 1 and arr[i][j] > arr[ni][nj] - K:
                tmp = arr[ni][nj]   # 원래 높이 저장
                arr[ni][nj] = arr[i][j] - 1
                f(ni, nj, N, K, 0, s+1)
                arr[ni][nj] = tmp   # 깎기 전 높이로 다시 탐색해봐야 함
    v[i][j] = 0     # i, j 칸을 이전의 다른 경로에서 사용할 수 있도록.

T = int(input())

for tc in range(1, T+1):
    N, K = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]
    v = [[0] * N for _ in range(N)]   # 현재 등산로에 포함된 칸 표시
    h = 0    # 최대 높이

    for i in range(N):
        for j in range(N):
            if h < arr[i][j]:
                h = arr[i][j]

    # 최대 높이인 곳에서 등산로 만들어보기
    maxV = 0          # 최대 등산로 길이
    for i in range(N):
        for j in range(N):
            if arr[i][j] == h:
                f(i, j, N, K, 1, 0)     # i, j에서 부터 등산로 만들어 보기.  깎을 수 있는 횟수, 지금까지의 등산로 길이

    print(f'#{tc} {maxV}')
```

​																													

```python
    # 상하좌우
di = [-1,1,0,0]
dj = [0,0,-1,1]

def work(i,j, road, skill):     # 현재 좌표, 지금까지 길의 길이, 공사여부
    global ans
    if road > ans:
        ans = road

    visited[i][j] = 1

    for q in range(4):
        ni = i + di[q]
        nj = j + dj[q]

        if 0 <= ni < N and 0 <= nj < N and not visited[ni][nj]:
            # 1. 현 위치보다 낮을 곳으로 이동할 때
            if mountain[i][j] > mountain[ni][nj]:
                work(ni, nj, road+1, skill)
            # 2. 현 위치보다 높거나 같은 곳으로 이동할 때
            elif skill and mountain[i][j] > mountain[ni][nj] - K:
                tmp = mountain[ni][nj]
                mountain[ni][nj] = mountain[i][j] - 1
                work(ni, nj, road+1, 0)  # 스킬 사용
                mountain[ni][nj] = tmp   # 다음 반복문을 위해 원상복구

    visited[i][j] = 0       # 다음 경로를 위해 방문 풀어줌

T = int(input())

for tc in range(1, T+1):
    N, K = map(int, input().split())
    mountain = [list(map(int, input().split())) for _ in range(N)]
    max_h = 0    # 최대 높이
    ans = 0
    for i in range(N):
        for j in range(N):
            if max_h < mountain[i][j]:
                max_h = mountain[i][j]

    visited = [[0] * N for _ in range(N)]   # 현재 등산로에 포함된 칸 표시

    for i in range(N):
        for j in range(N):
            if mountain[i][j] == max_h:
                work(i,j,1,1)

    print(f'#{tc} {ans}')
```

