# :boom: DFS

---

​											

### 길찾기

---

```python
def dfs(S, G, V):
    visited = [0] * V
    stack = []
    visited[S] = 1
    i = S             # 현재 방문한 정점

    while i != -1:                                     # 방문할 정점이 없으면
        for w in range(V):
            if arr[i][w] == 1 and visited[w] == 0:     # 인접하고 미방문이면,
                stack.append(i)                        # 현재 위치를 경로로 저장
                i = w
                visited[w] = 1
                if i == G:                             # 목표G 를 방문하면 종료
                    return 1
                break
        else:                                          # 인접한 w를 못찾은 경우
            if stack:                                  # stack에서 꺼내기
                i = stack.pop()
            else:                                      # stack이 없으면 종료
                i = -1
    return 0

for _ in range(10):
    tc, road = map(int, input().split())
    arr = [[0]*100 for _ in range(100)]
    edges = list(map(int, input().split()))            # 경로들을 리스트로 저장
    for i in range(road):                              # 입력된 경로의 개수의 범위내에서
        start, end = edges[i*2], edges[i*2+1]          # 시작과 끝 지점을 각각 배당하고
        arr[start][end] = 1                            # 인접행렬에 값을 넣어줌

    print(f'#{tc} {dfs(0, 99, 100)}')
```









# :smile: BFS

---

​																																									

```python
'''
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def bfs(s, V):     # 시작 정점, 끝 정점
    q = []
    visited = [0] * (V+1)
    visited[s] = 1
    q.append(s)

    while q:       # 큐가 비어있지 않으면, 처리할 정점이 남아 있으면,
        t = q.pop(0)
        print(t)   # t에 대한 처리
        for i in range(1, V+1):  # t에 인접이고 미방문인 모든 i에 대해
            if adj[t][i] == 1 and visited[i] == 0:
                q.append(i)
                visited[i] = visited[t] + 1

def bfs2(s, V):     # 인접 리스트를 이용한 해결
    q = []
    visited = [0] * (V+1)
    visited[s] = 1
    q.append(s)

    while q:       # 큐가 비어있지 않으면, 처리할 정점이 남아 있으면,
        t = q.pop(0)
        print(t)   # t에 대한 처리
        for i in adjlist:  # t에 인접이고 미방문인 모든 i에 대해
            if visited[i] == 0:
                q.append(i)
                visited[i] = visited[t] + 1

def bfs3(s, V):
    q = [0] * V            # 큐 생성
    front = -1
    rear = -1
    visited = [0] * (V+1)
    rear += 1
    q[rear] = s
    visited[s] = 1         # 시작점 visited
    while front != rear:   # 큐가 비어있지 않으면
        front += 1         # 디큐해서 t에 저장
        t = q[front]
        print(t)
        for i in range(1, V+1):   # t에 인접하고 미방문인 모든 i에 대해
            if adj[t][i] == 1 and visited[i] == 0:
                rear += 1
                q[rear] = i
                visited[i] = visited[t] + 1

V, E = map(int, input().split())
edge = list(map(int, input().split()))
adj = [[0] * (V+1) for _ in range(V+1)]       # 인접 행렬 만들기
adjlist = [[]for _ in range(V+1)]             # 인접 리스트 만들기

for i in range(E):
    n1, n2 = edge[2*i], edge[2*i+1]
    adj[n1][n2] = 1
    adj[n2][n1] = 1                    # 방향이 없는 그래프

    adjlist[n1].append(n2)                    # 인접 리스트로 풀어보는 방법  ni 정점일 때 인접인애들 리스트
    adjlist[n2].append(n1)
bfs(1, V)
```

---

