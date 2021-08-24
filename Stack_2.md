# :boom: Stack_2

---

​										

### Forth



Forth라는 컴퓨터 언어는 스택 연산을 기반으로 하고 있어 후위 표기법을 사용한다. 예를 들어 3+4는 다음과 같이 표기한다.
 

3 4 + .
 

Forth에서는 동작은 다음과 같다.
 

숫자는 스택에 넣는다.

연산자를 만나면 스택의 숫자 두 개를 꺼내 더하고 결과를 다시 스택에 넣는다.

‘.’은 스택에서 숫자를 꺼내 출력한다.

 

Forth 코드의 연산 결과를 출력하는 프로그램을 만드시오. 만약 형식이 잘못되어 연산이 불가능한 경우 ‘error’를 출력한다.
 

다음은 Forth 연산의 예이다.
 

| 코드    | 출력 |
| ------- | ---- |
| 4 2 / . | 2    |
| 4 3 - . | 1    |

 

 

**[입력]**
 

첫 줄에 테스트 케이스 개수 T가 주어진다. 1≤T≤50
 

다음 줄부터 테스트 케이스의 별로 정수와 연산자가 256자 이내의 연산코드가 주어진다. 피연산자와 연산자는 여백으로 구분되어 있으며, 코드는 ‘.’로 끝난다.

나눗셈의 경우 항상 나누어 떨어진다.

 

**[출력]**
 

\#과 1번부터인 테스트케이스 번호, 빈칸에 이어 계산결과를 정수로 출력하거나 또는 ‘error’를 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    expression = input().split()
    stack = []
    ans = 0

    for i in expression:
        try:
            if i == '.':
                ans = stack.pop()
            elif i in ['+', '-', '*', '/']:
                b = stack.pop()
                a = stack.pop()
                if i == '+':
                    stack.append(a+b)
                elif i == '-':
                    stack.append(a-b)
                elif i == '*':
                    stack.append(a*b)
                else:
                    stack.append(a//b)
            else:
                stack.append(int(i))
        except:     # 형식이 잘못되어 연산이 불가능한 경우
            ans = 'error'
            break
    else:       # for 문을 다 돌리고 문제 없으나, stack에 숫자가 남아있는 경우
        if stack:
            ans = 'error'

    print(f'#{tc} {ans}')
```

---

```python
T = int(input())
for tc in range(1, T+1):
    st = list(map(str, input().split()))
    stack = []
    error = 0
    for x in st:
        if x.isdigit():
            stack.append(x)
        else:
            try:
                if x == '+':
                    d2 = int(stack.pop())
                    d1 = int(stack.pop())
                    stack.append(d1 + d2)
                elif x == '*':
                    d2 = int(stack.pop())
                    d1 = int(stack.pop())
                    stack.append(d1 * d2)
                elif x == '/':
                    d2 = int(stack.pop())
                    d1 = int(stack.pop())
                    stack.append(d1 // d2)
                elif x == '-':
                    d2 = int(stack.pop())
                    d1 = int(stack.pop())
                    stack.append(d1 - d2)
            except:
                error = 1
                break
 
    if error or len(stack)!=1:
        print(f'#{tc} error')
    else:
        print(f'#{tc} {stack.pop()}')
```

​											

---

​						

### 미로



NxN 크기의 미로에서 출발지에서 목적지에 도착하는 경로가 존재하는지 확인하는 프로그램을 작성하시오. 도착할 수 있으면 1, 아니면 0을 출력한다.

주어진 미로 밖으로는 나갈 수 없다.
 

다음은 5x5 미로의 예이다.
 

13101

10101

10101

10101

10021

 

마지막 줄의 2에서 출발해서 0인 통로를 따라 이동하면 맨 윗줄의 3에 도착할 수 있는지 확인하면 된다.

 
 

**[입력]**
 

첫 줄에 테스트 케이스 개수 T가 주어진다. 1<=T<=50
 

다음 줄부터 테스트 케이스의 별로 미로의 크기 N과 N개의 줄에 걸쳐 미로의 통로와 벽에 대한 정보가 주어진다. 0은 통로, 1은 벽, 2는 출발, 3은 도착이다. 5<=N<=100

 

**[출력]**
 

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 계산결과를 정수로 출력하거나 또는 ‘error’를 출력한다.

---

```python
def f(i, j, N):
    if maze[i][j] == 3:
        return 1
    else:
        maze[i][j] = 1
        for di, dj in [(-1,0), (0, 1), (0, -1), (1,0)]:
            ni, nj = i + di, j + dj
            if 0 <= ni < N and 0 <= nj < N and maze[ni][nj] != 1:      # 3인 경우에도 이동해야 하므로 '!= 1'
                if f(ni, nj, N):          
                    return 1              
        return 0                          


T = int(input())
for tc in range(1, T+1):
    N = int(input())
    maze = [list(map(int, input())) for _ in range(N)]
    stats_i, start_j = 0, 0
    for i in range(N):
        for j in range(N):
            if maze[i][j] == 2:
                start_i, start_j = i, j

    print(f'#{tc} {f(start_i, start_j, N)}')
```

---

​														

### 가위바위보 토너먼트

---

```python
def tournament(i, j):     # i는 시작 인덱스, j는 끝 인덱스
    if i == j:            # 한명 남았을 때, 가위바위보
        return i
    else:                                        # 두 개의 그룹으로 나누고,
        A = tournament(i, (i + j) // 2)          # 재귀함수 형식으로 계속 그룹이 나뉨
        B = tournament((i + j) // 2 + 1, j)
        if npc[A] == npc[B]:                                  # 비기면 더 앞 순서인 사람 승리
            return A
        elif npc[A] - npc[B] == 1 or npc[A] - npc[B] == -2:   # A가 이기는 경우
            return A
        else:
            return B

T = int(input())
for tc in range(1, T + 1):
    N = int(input())
    npc = list(map(int, input().split()))
    print(f'#{tc} {tournament(0, N-1) + 1}')   # 인덱스 +1
```

​							

---



### 배열 최소 합

---

```python
def f(i, N, s):
    global min_sum

    if i == N:
        if min_sum > s:
            min_sum = s
    elif min_sum <= s:
        return
    else:
        for j in range(i, N):
            p[i], p[j] = p[j], p[i]
            f(i+1, N, s + arr[i][p[i]])
            p[i], p[j] = p[j], p[i]
        return

T = int(input())
for tc in range(1, T + 1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    min_sum = 10 * N * N
    p = list(range(N))
    f(0, N, 0)
    print(f'#{tc} {min_sum}')

```

---

​					

### **계산기 3**

문자열로 이루어진 계산식이 주어질 때, 이 계산식을 후위 표기식으로 바꾸어 계산하는 프로그램을 작성하시오.

예를 들어

“3+(4+5)*6+7”

라는 문자열로 된 계산식을 후위 표기식으로 바꾸면 다음과 같다.

"345+6*+7+"

변환된 식을 계산하면 64를 얻을 수 있다.

문자열 계산식을 구성하는 연산자는 +, * 두 종류이며 문자열 중간에 괄호가 들어갈 수 있다.

이 때 괄호의 유효성 여부는 항상 옳은 경우만 주어진다.

피연산자인 숫자는 0 ~ 9의 정수만 주어진다.

**[입력]**

각 테스트 케이스의 첫 번째 줄에는 테스트 케이스의 길이가 주어진다. 그 다음 줄에 바로 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 답을 출력한다.

---

```python
for tc in range(1, 11):
    n = int(input())
    arr = input()
    stack = []
    new = ''

    for i in arr:                               # step1, 후위 표기법 변환
        if i == '(':                            # 여는 괄호이면 icp가 제일 높으므로 무조건 push
            stack.append(i)
        elif i == ')':                          # 닫는 괄호이면 스택 top에 여는 괄호가 나올 때까지 pop
            while stack[-1] != '(':
                new += stack.pop()
            stack.pop()                         # 여는 괄호 만나면 pop 해서 괄호 두개 모두 없애줌
        elif i == '+':                          # '+'이면 스택이 있고 본인보다 우선순위가 낮은 연산자를 만날 때까지 pop
            while stack and stack[-1] != '(':   # 여기선 여는 괄호 밖에 없음
                new += stack.pop()
            stack.append(i)                     # pop 한 후 '+' 연산자 push
        elif i == '*':
            while stack and stack[-1] == '*':   # 본인보다 우선순위가 낮은 연산자를 만날 때까지 pop 이므로 본인 안나올때까지
                new += stack.pop()
            stack.append(i)
        else:                                   # 숫자는 모두 출력
            new += i

    for i in new:                               # step2, 후위 표기법 계산
        if i == '+':
            x1 = stack.pop()
            x2 = stack.pop()
            stack.append(x1 + x2)
        elif i == '*':
            x1 = stack.pop()
            x2 = stack.pop()
            stack.append(x1 * x2)
        else:                                   # 피연산자는 모두 스택에 push 계산을 위해 int처리해줌
            stack.append(int(i))

    ans = stack.pop()                           # 마지막 스택을 꺼내서 답 변수에 저장
    print(f'#{tc} {ans}')
```

