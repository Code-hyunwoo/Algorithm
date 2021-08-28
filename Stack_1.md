# :boom: Stack

---

​						

### 괄호검사

```python
s = input()   
stack = []
ans = 1
for x in s:
    if x == '(':              # push(x)
        stack.append(x)
    elif x == ')':            # pop(x)
        if stack:             # stack 이 비어있지 않으면 
            stack.pop(-1)
        else:
            ans = 0
            break
    else:
        pass
# 스택에 남은 괄호가 있는 지 확인
if ans == 1 and stack:
    ans = 0
      
print(ans)
```

​																									

### 팩토리얼 DP

```python
def fact(n):
    table[0] = 1
    for i in range(1, n+1):
        table[i] = i * table[i-1]
    return table[n]

n = int(input())
table = [0] * (n+1)
print(fact(n))
```

​			

### 파스칼의 삼각형

크기가 N인 파스칼의 삼각형을 만들어야 한다.

파스칼의 삼각형이란 아래와 같은 규칙을 따른다.

\1. 첫 번째 줄은 항상 숫자 1이다.

\2. 두 번째 줄부터 각 숫자들은 자신의 왼쪽과 오른쪽 위의 숫자의 합으로 구성된다.

N이 4일 경우,

N을 입력 받아 크기 N인 파스칼의 삼각형을 출력하는 프로그램을 작성하시오.


**[제약 사항]**

파스칼의 삼각형의 크기 N은 1 이상 10 이하의 정수이다. (1 ≤ N ≤ 10)


**[입력]**

가장 첫 줄에는 테스트 케이스의 개수 T가 주어지고, 그 아래로 각 테스트 케이스가 주어진다.

각 테스트 케이스에는 N이 주어진다.


**[출력]**

각 줄은 '#t'로 시작하고, 다음 줄부터 파스칼의 삼각형을 출력한다.

삼각형 각 줄의 처음 숫자가 나오기 전까지의 빈 칸은 생략하고 숫자들 사이에는 한 칸의 빈칸을 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)

---

```python
T = int(input())
for tc in range(1, T+1):
    n = int(input())
    arr = [[0] * n for _ in range(n)]         # n크기 만큼 이차원 배열 생성

    for x in range(n):
        for y in range(x+1):                  # 열의 범위는 x+1까지
            if x == y or y == 0:              # x, y값이 같거나, 첫번째 항일 경우
                arr[x][y] = 1
            else:
                arr[x][y] = arr[x-1][y-1] + arr[x-1][y]
                                              # 전행의 전열 값 + 전행의 같은 열 값
    print(f'#{tc}')
    for x in range(n):
        for y in range(x+1):
            if arr[x][y] != 0:                # 0인 값들을 제외한 파스칼 삼각형 출력
                print(arr[x][y], end=' ')
        print()
```





### 종이붙이기

---

```python
T = int(input())
for tc in range(1, T+1):
    n = int(input())

    def paper(n):
        if n == 10:
            return 1
        elif n == 20:
            return 3
        return paper(n-10) + 2*paper(n-20)
        # 직전 종이에 10짜리 종이 붙이는 경우 +
        # 2번째 전 종이에 가로 20을 추가하는데 10짜리 2개를 붙이는 건 제외하고(바로 위 경우와 겹침)
        # 작은 종이를 가로로 20붙이거나, 큰거 20짜리 하나 붙이는 2가지 경우를 고려하여

    print(f'#{tc} {paper(n)}')

```

---

​											

### 괄호검사

---

```python
T = int(input())
for tc in range(1, T+1):
    S = input()
    stack = []
    ans = 1

    for i in S:
        if i == '(' or i == '{':                  # 여는 괄호일 경우 stack에 저장
            stack.append(i)
        elif i == ')':                            # 닫는 소괄호일 때
            if stack != [] and stack[-1] == '(':  # stack이 비어있지 않고, 마지막이 여는 소괄호이면
                stack.pop(-1)                     # pop 해서 제거
            else:                                 # stack의 마지막이 여는 중괄호이면
                ans = 0                           # 오류, 중단
                break
        elif i == '}':                            # 닫는 중괄호의 경우도 같음
            if stack != [] and stack[-1] == '{':
                stack.pop(-1)
            else:
                ans = 0
                break

    if ans == 1 and stack:                         # stack에 남아있는지 확인
        ans = 0

    print(f'#{tc} {ans}')
```

---

​											

### 반복문자 지우기

---

```python
T = int(input())
for tc in range(1, T+1):
    S = input()
    stack = []

    for i in S:
        if not stack:              # stack 이 비어있을 경우
            stack.append(i)        # 무조건 추가
        elif i == stack[-1]:       # 비어있지 않고, 그 다음 문자가 stack의 마지막 문자와 같으면
            stack.pop(-1)          # stack 의 마지막 문자 pop으로 제거
        else:
            stack.append(i)        # 이외는 stack 에 문자 추가

    print(f'#{tc} {len(stack)}')
```

---

​										

### 그래프 경로

---

```python
T = int(input())
for tc in range(1, T+1):
    V, E = map(int, input().split())
    arr = [[0]*(V+1) for _ in range(V+1)]      # 인접행렬을 나타내기 위한 배열리스트 생성
    for _ in range(E):                         # 입력값을 인접행렬 리스트에 넣기
        s, e = map(int, input().split())
        arr[s][e] = 1                          # 화살표가 있으므로, s에서 e로 가는 인덱스 행렬에 1 값주기
    S, G = map(int, input().split())           # 시작점, 목표지점
    visited = [0] * (V+1)                      # 방문확인 리스트 1번부터 V번까지
    stack = [S]                                # 시작점 S를 넣고 stack 리스트 생성
    visited[S] = 1                             # 시작점은 방문확인
    i = S                                      # i는 현재 방문한 정점, 시작점에서 시작

    while i != 0:                              # i가 0이 될 때까지 = 방문 할 곳이 없을때 까지
        for w in range(1, V+1):                # 인접한 정점을 찾기
            if arr[i][w] == 1 and visited[w] == 0:  # 인접하고, 방문한 적이 없으면
                stack.append(i)                # 방문 경로 저장
                i = w                          # 현재 방문한 정점을 w로 변경
                visited[w] = 1
                break
        else:                                  # 인접이 없는 경우
            if stack:                          # 지나온 stack에서 하나 꺼냄
                i = stack.pop()
            else:                              # stack이 비어있으면 끝
                i = 0

    if visited[G] == 1:                        # 목표지점인 G를 방문했으면
        ans = 1                                # 답은 1
    else:
        ans = 0

    print(f'#{tc} {ans}')

```

---

