# :boom:Array

---

### 색칠하기

그림과 같이 인덱스가 있는 10x10 격자에 빨간색과 파란색을 칠하려고 한다.

N개의 영역에 대해 왼쪽 위와 오른쪽 아래 모서리 인덱스, 칠할 색상이 주어질 때, 칠이 끝난 후 색이 겹쳐 보라색이 된 칸 수를 구하는 프로그램을 만드시오.

주어진 정보에서 같은 색인 영역은 겹치지 않는다.



**[입력]**


첫 줄에 테스트 케이스 개수 T가 주어진다.  ( 1 ≤ T ≤ 50 )

다음 줄부터 테스트케이스의 첫 줄에 칠할 영역의 개수 N이 주어진다. ( 2 ≤ N ≤ 30 )

다음 줄에 왼쪽 위 모서리 인덱스 r1, c1, 오른쪽 아래 모서리 r2, c2와 색상 정보 color가 주어진다. ( 0 ≤ r1, c1, r2, c2 ≤ 9 )

color = 1 (빨강), color = 2 (파랑)

 

**[출력]**


각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [[0]*10 for _ in range(10)]                      # 10 x 10 2차원 배열 생성
    purple = 0                                             # 보라색 변수 설정

    for _ in range(N):                                     # input N에 따른 반복
        x1, y1, x2, y2, color = map(int, input().split())  # 좌표 및 색 설정
        for x in range(x1, x2 + 1):
            for y in range(y1, y2 + 1):
                arr[x][y] += color                         # 영역 색칠
                if arr[x][y] == 3:                         # 보라색 되면 바로 count
                    purple += 1

    print(f'#{tc} {purple}')
```

---

​																				

### 부분집합의 합

1부터 12까지의 숫자를 원소로 가진 집합 A가 있다. 집합 A의 부분 집합 중 N개의 원소를 갖고 있고, 원소의 합이 K인 부분집합의 개수를 출력하는 프로그램을 작성하시오.

해당하는 부분집합이 없는 경우 0을 출력한다. 모든 부분 집합을 만들어 답을 찾아도 된다.


예를 들어 N = 3, K = 6 경우, 부분집합은 { 1, 2, 3 } 경우 1가지가 존재한다.

 


**[입력]**


첫 줄에 테스트 케이스 개수 T가 주어진다. ( 1 ≤ T ≤ 50 )


테스트 케이스 별로 부분집합 원소의 수 N과 부분 집합의 합 K가 여백을 두고 주어진다. ( 1 ≤ N ≤ 12, 1 ≤ K ≤ 100 )

 

**[출력]**


각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

---

```python
T = int(input())

for tc in range(1, T+1):
    A = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
    N, K = map(int, input().split())
    ans = 0                                 # 부분집합 길이가 N, 합이 K인 부분집합 개수

    for i in range(1 << 12):                # 12개의 원소를 가진 모든 부분 집합 개수
            subset_sum = 0                  # 부분집합의 합
            subset_len = 0                  # 부분집합의 길이
            for j in range(12):
                if i & (1 << j):            # i의 j번 비트가 1이면 부분집합 포함
                    subset_sum += A[j]      # 부분집합 합에 추가
                    subset_len += 1         # 부분집합 길이 증가
            if subset_len == N and subset_sum == K:
                ans += 1

    print(f'#{tc} {ans}')
```

---

​																						

### 이진탐색

코딩반 학생들에게 이진 탐색을 설명하던 선생님은 이진탐색을 연습할 수 있는 게임을 시켜 보기로 했다.

짝을 이룬 A, B 두 사람에게 교과서에서 각자 찾을 쪽 번호를 알려주면, 이진 탐색만으로 지정된 페이지를 먼저 펼치는 사람이 이기는 게임이다.

예를 들어 책이 총 400쪽이면, 검색 구간의 왼쪽 l=1, 오른쪽 r=400이 되고, 중간 페이지 c= int((l+r)/2)로 계산한다.

찾는 쪽 번호가 c와 같아지면 탐색을 끝낸다.

A는 300, B는 50 쪽을 찾아야 하는 경우, 다음처럼 중간 페이지를 기준으로 왼쪽 또는 오른 쪽 영역의 중간 페이지를 다시 찾아가면 된다.

책의 전체 쪽수와 두 사람이 찾을 쪽 번호가 주어졌을 때, 이진 탐색 게임에서 이긴 사람이 누구인지 알아내 출력하시오. 비긴 경우는 0을 출력한다.

 


**[입력]**


첫 줄에 테스트 케이스 개수 T가 주어진다. 1<=T<=50


테스트 케이스 별로 책의 전체 쪽 수 P, A, B가 찾을 쪽 번호 Pa, Pb가 차례로 주어진다. 1<= P, Pa, Pb <=1000


**[출력]**


각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, A, B, 0 중 하나를 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    P, Pa, Pb = map(int, input().split())
    cnt_list = []

    for i in (Pa, Pb):
        cnt = 0                             # 탐색 횟수 변수 설정
        start = 1
        end = P
        while start <= end:
            middle = int((start + end)/2)
            cnt += 1                        # 탐색 횟수마다 추가
            if middle == i:
                cnt_list.append(cnt)        # 탐색 완료시 리스트에 횟수 추가
                break
            elif middle > i:
                end = middle
            else:
                start = middle

    if cnt_list[0] == cnt_list[1]:          # A, B 순으로 탐색했으므로 첫 항은 A
        winner = 0
    elif cnt_list[0] < cnt_list[1]:         # 탐색 횟수가 적으면 게임에서 이김
        winner = 'A'
    else:
        winner = 'B'

    print(f'#{tc} {winner}')
```

---

​																

### 특별한 정렬

보통의 정렬은 오름차순이나 내림차순으로 이루어지지만, 이번에는 특별한 정렬을 하려고 한다.

N개의 정수가 주어지면 가장 큰 수, 가장 작은 수, 2번째 큰 수, 2번째 작은 수 식으로 큰 수와 작은 수를 번갈아 정렬하는 방법이다.

예를 들어 1부터 10까지 10개의 숫자가 주어지면 다음과 같이 정렬한다.


10 1 9 2 8 3 7 4 6 5


주어진 숫자에 대해 특별한 정렬을 한 결과를 10개까지 출력하시오

 


**[입력]**


첫 줄에 테스트 케이스 개수 T가 주어진다. 1<=T<=50

다음 줄에 정수의 개수 N이 주어지고 다음 줄에 N개의 정수 ai가 주어진다. 10<=N<=100, 1<=ai<=100

 

**[출력]**


각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 특별히 정렬된 숫자를 10개까지 출력한다.

---

```python
T = int(input())

for tc in range(1, T+1):
    N = int(input())
    num = list(map(int, input().split()))

    for i in range(N):
        if i % 2 == 0:                         # 짝수 index 일 때 최댓값
            max_idx = i                        # 최대값이라 가정
            for j in range(i+1, N):
                if num[max_idx] < num[j]:
                    max_idx = j
            num[i], num[max_idx] = num[max_idx], num[i]
                                               # if 조건문을 통해 최댓값을 찾고 for문 밖에서 바꿔줘야 함
        else:                                  # 홀수 index 일 때 최솟값
            min_idx = i                        # 최솟값이라 가정
            for j in range(i+1, N):
                if num[min_idx] > num[j]:
                    min_idx = j
            num[i], num[min_idx] = num[min_idx], num[i]
                                         
    print(f'#{tc}', end=' ')
    for k in range(10):
        print(num[k], end=' ')
    print()

```

---

​										

### **사각형 찾기**

크기가 NxN인 2차원 배열 내부에 1로 채워진 사각 영역이 있다. 사각형의 가로 세로 칸수를 곱한 값을 출력하는 프로그램을 만드시오. 사각형이 여러 개인 경우 곱이 가장 큰 경우를 출력한다.

다음은 N=10인 2차원 배열의 예로, 곱은 12가 된다.

0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0 
0 0 0 1 1 0 0 0 0 0 
0 0 0 1 1 0 0 0 0 0 
0 0 0 1 1 0 0 0 0 0 
0 0 0 1 1 0 0 0 0 0 
0 0 0 1 1 0 0 0 0 0 
0 0 0 1 1 0 0 0 0 0 
0 0 0 0 0 0 0 0 0 0

입력
첫 줄에 테스트케이스 개수 T가 주어진다.

다음 줄부터 테스트케이스 별로 첫 줄에 N, N 줄에 걸쳐 N개의 0또는 1이 주어진다.

 1<=T<=50, 10 <= N <= 100

출력
\#에 이어 1번 부터인 테스트케이스번호, 빈칸에 이어 답을 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    ans = 0

    for i in range(N):                            # 모든 배열을 순회
        for j in range(N):
            width = 1                             # 가로 기본값 1 설정
            height = 1                            # 세로 기본값 1 설정
            if arr[i][j] == 1:                    # 요소 값이 1일 때,
                for k in range(j+1, N):           # 가로 길이 구하기
                    if arr[i][k] == 1:
                        width += 1
                    else:
                        break

                for l in range(i+1, N):           # 세로 길이 구하기
                    if arr[l][j] == 1:
                        height += 1
                    else:
                        break

                area = width * height             # 가로, 세로 곱 구하기
                if area > ans:                    # 최댓값 설정
                    ans = area

    print(f'#{tc} {ans}')
```

---

​											

### 가로 세로의 최대합

[가로세로 합]

N x N 배열에서 한 칸을 선택했을 때 그 칸을 포함하는 가로 행과 세로 열에 포함된 값들의 총합이 최대가 되는 경우를 찾고 싶다.

그림1과 2는 N = 4인 배열의 예이다.  그림 1은 (3행, 1열)의 위치를 포함하는 행과 열의 합 **15** 가 최대가 되고, 그림 2는 (2행, 2열)을 포함하는 **16** 이 최대가 된다.



[입력]

첫 줄에 테스트케이스 수가 주어진다.

다음으로 배열의 크기 N(1<= N <= 30)이 주어진다.

다음 N개의 줄에 공백으로 구분된 N개의 정수 aij값이 주어진다. (0<= aij <=100)

 

[출력]

'#'과 케이스 번호를 출력하고 총합이 최대가 되는 값을 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]
    maxV = 0                            # 최댓값 설정

    for i in range(N):                  # 행 선택
        for j in range(N):              # 열 선택
            sum_tmp = 0                 # 행, 열의 합 기본 0 설정
            for k in range(N):
                sum_tmp += arr[i][k]    # 선택된 행의 합
                sum_tmp += arr[k][j]    # 선택된 열의 합
            sum_tmp -= arr[i][j]        # 중복되어 더해지는 [행][열] 요소 빼기 !위치 주의
            if sum_tmp > maxV:          # 최댓값 조정
                maxV = sum_tmp

    print(f'#{tc} {maxV}')
```

---

​											

### 부분 배열의 합

크기가 NxN인 배열의 부분 배열인 nxm 배열 원소의 합 중 가장 큰 값을 출력하시오.

 

다음은 N=5, n=2, m=3일 때 오른쪽 아래의 부분 배열 영역을 나타낸다. 

부분 배열은 주어진 NxN 배열을 벗어나지 않는 모든 경우에 대해 고려해야한다.


입력
첫 줄에 테스트케이스개수 T가 주어지고, 다음 줄 부터 각 테스트 케이스 별로 N, n, m이 주어진다. 이후 N개의 줄 각각 N개의 1 또는 0이 주어진다.

10<=N<=100, 1<=n, m

출력
\#에 이어 1번부터인 테스트케이스 번호, 빈칸에 이어 답을 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    N, n, m = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]
    maxV = 0

    for i in range(N-n+1):                # 부분 배열 시작점의 행의 범위를 길이 n 에 따라 제한
        for j in range(N-m+1):            # 부분 배열 시작점의 열의 범위를 길이 m 에 따라 제한
            sum_tmp = 0
            for k in range(i, i+n):       # 시작점을 기준으로 n길이 만큼 행의 범위 조정
                for q in range(j, j+m):   # 시작점을 기준으로 m길이 만큼 열의 범위 조정
                    sum_tmp += arr[k][q]  # 부분 배열의 합
            if sum_tmp > maxV:
                maxV = sum_tmp            # 최대 값 설정

    print(f'#{tc} {maxV}')
```

---

​																		

### Ladder1



점심 시간에 산책을 다니는 사원들은 최근 날씨가 더워져, 사다리 게임을 통하여 누가 아이스크림을 구입할지 결정하기로 한다.

김 대리는 사다리타기에 참여하지 않는 대신 사다리를 그리기로 하였다.

사다리를 다 그리고 보니 김 대리는 어느 사다리를 고르면 X표시에 도착하게 되는지 궁금해졌다. 이를 구해보자.

아래 <그림 1>의 예를 살펴보면, 출발점 x=0 및 x=9인 세로 방향의 두 막대 사이에 임의의 개수의 막대들이 랜덤 간격으로 추가되고(이 예에서는 2개가 추가됨) 이 막대들 사이에 가로 방향의 선들이 또한 랜덤하게 연결된다.

X=0인 출발점에서 출발하는 사례에 대해서 화살표로 표시한 바와 같이, 아래 방향으로 진행하면서 좌우 방향으로 이동 가능한 통로가 나타나면 방향 전환을 하게 된다.

방향 전환 이후엔 다시 아래 방향으로만 이동하게 되며, 바닥에 도착하면 멈추게 된다.

문제의 X표시에 도착하려면 X=4인 출발점에서 출발해야 하므로 답은 4가 된다. 해당 경로는 별도로 표시하였다.



**[제약 사항]**

한 막대에서 출발한 가로선이 다른 막대를 가로질러서 연속하여 이어지는 경우는 없다.

**[입력]**

입력 파일의 첫 번째 줄에는 테스트 케이스의 번호가 주어지며, 바로 다음 줄에 테스트 케이스가 주어진다.

총 10개의 테스트 케이스가 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 도착하게 되는 출발점의 x좌표를 출력한다.



---

```python
for _ in range(10):
    tc = int(input())
    ladder = [list(map(int, input().split())) for _ in range(100)]

    for a in range(100):
        if ladder[99][a] == 2:
            X = a                                         # 도착점 X 좌표 찾기

    i, j = 99, X                                          # 도착점 좌표에서 시작

    while i != 0:                                         # 0행으로 올때까지 반복
        if (j-1) >= 0 and ladder[i][j-1] == 1:            # 왼쪽이동,  범위안 & 왼쪽이 1인 경우
            j -= 1
            while (j-1) >= 0 and ladder[i-1][j] == 0:     # 계속 왼쪽이동, 범위안 & 위가 0인 경우
                j -= 1
            else:                                         # 막히면 위로 이동
                i -= 1
        elif (j+1) <= 99 and ladder[i][j+1] == 1:         # 오른쪽이동, 범위안 & 오른쪽이 1인 경우
            j += 1
            while (j+1) <= 99 and ladder[i-1][j] == 0:    # 계속 오른쪽이동, 범위안 & 위가 0인 경우
                j += 1
            else:                                         # 막히면 위로 이동
                i -= 1
        else:                                             # 왼쪽 오른쪽 모두 이동 안되면 위로 이동
            i -= 1

    print(f'#{tc} {j}')


```

---



### 풍선팡



종이 꽃가루가 들어있는 풍선이 M개씩 N개의 줄에 붙어있고, 어떤 풍선을 터뜨리면 안에 든 종이 꽃가루 개수만큼 상하 좌우의 풍선이 추가로 터지게 되는 게임이 있다.

예를 들어 풍선에 든 꽃가루가 1개씩일 때, 가운데 풍선을 터뜨리면 상하좌우의 풍선이 추가로 1개씩 터지면서 총 5개의 꽃가루가 날리게 된다.

NxM개의 풍선에 들어있는 종이 꽃가루 개수A가 주어지면, 한 개의 풍선을 선택했을 때 날릴 수 있는 꽃가루의 합 중 최대값을 출력하는 프로그램을 만드시오.

(3<=N, M<=100)

 

**입력**

첫 줄에 테스트케이스 수 T, 다음 줄부터 테스트케이스 별로 첫 줄에 N과 M, 이후 N줄에 걸쳐 M개씩 풍선에 든 종이 꽃가루 개수가 주어진다.

 

**출력**

\#과 테스트케이스 번호, 빈칸에 이어 종이 꽃가루의 최대 개수를 출력한다.

---

```python

T = int(input())

for tc in range(1, T+1):
    N, M = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]

    max_pollen = 0  

    dx = [-1, 1, 0, 0]                                  # 상 하 좌 우
    dy = [0, 0, -1, 1]

    for i in range(N):
        for j in range(M):
            pollen = arr[i][j]                          # 기준풍선 설정
            for k in range(4):                          # 네 방향에 대하여
                for q in range(1, arr[i][j]+1):         # 1부터 기준풍선의 든 값만큼
                    ni, nj = i + dx[k]*q, j + dy[k]*q   # 추가로 터질 풍선을 찾음
                    if 0 <= ni < N and 0 <= nj < M:     # 이 값이 범위안 유효값이면
                        pollen += arr[ni][nj]           # 꽃가루 변수에 추가
            if pollen > max_pollen:                     # 최댓값 비교
                max_pollen = pollen

    print(f'#{tc} {max_pollen}')
```

---

​									

### 파리 퇴치



N x N 배열 안의 숫자는 해당 영역에 존재하는 파리의 개수를 의미한다.

아래는 N=5 의 예이다.

M x M 크기의 파리채를 한 번 내리쳐 최대한 많은 파리를 죽이고자 한다.

죽은 파리의 개수를 구하라!

예를 들어 M=2 일 경우 위 예제의 정답은 49마리가 된다.

**[제약 사항]**

\1. N 은 5 이상 15 이하이다.

\2. M은 2 이상 N 이하이다.

\3. 각 영역의 파리 갯수는 30 이하 이다.


**[입력]**

가장 첫 줄에는 테스트 케이스의 개수 T가 주어지고, 그 아래로 각 테스트 케이스가 주어진다.

각 테스트 케이스의 첫 번째 줄에 N 과 M 이 주어지고,

다음 N 줄에 걸쳐 N x N 배열이 주어진다.


**[출력]**

출력의 각 줄은 '#t'로 시작하고, 공백을 한 칸 둔 다음 정답을 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)

---

```python
	
T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]
    max_kill = 0                          # 최대킬 변수 설정

    for i in range(N-M+1):                # 파리채 기준점의 행
        for j in range(N-M+1):            # 파리채 기준점의 열
            kill = 0                      # 값 비교를 위한 변수 설정
            for k in range(M):            # 기준점 기준으로 M-1까지 순회하며 값 추가
                for q in range(M):
                    kill += arr[i+k][j+q]
            if kill > max_kill:           # 최댓값 비교
                max_kill = kill

    print(f'#{tc} {max_kill}')
```

---





