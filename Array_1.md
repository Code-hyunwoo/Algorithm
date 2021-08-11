# :boom: Array



#### 연습문제 1	



NxN배열에서 각 요소에 대해서, 그 요소와 이웃한 요소와의 차의 절대값에 대한 합을 구한 후, 

총 합을 구하는 프로그램을 만드시오.

다음에서 7에 이웃한 요소는 2, 6, 12, 8이다.

입력

첫 줄에 테스트케이스 T, 다음 줄부터 테스트케이스 별로 첫 줄에 N, 

다음 줄부터 N개의 줄에 공백으로 구분된 1이상 99이하의 정수가 N개씩 제공된다.

1<=T<=10, 5<=N<=20
 출력

\#과 테스트케이스 번호, 빈칸에 이어 모든 원소에 대한 이웃한 숫자와의 차의 절대값에 대한 총 합을 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]        # 기본 2차원 리스트
    ans = 0                                                          # 모든 원소에 대해, 주변 원소와의 차이의 절대값의 합

    for i in range(N):
        for j in range(N):                                           # 모든 원소에 대한 접근
            for di, dj in [(0, -1), (0, 1), (-1, 0), (1, 0)]:        # 상하좌우
                ni, nj = i + di, j + dj                              # i, j의 주변 ni, nj
                if 0 <= ni < N and 0 <= nj < N:
                    ans += abs(arr[i][j] - arr[ni][nj])

    print(f'#{tc} {ans}')
```

---

​																															

#### 연습문제 2



10개의 정수를 입력 받아 부분 집합의 합이 0이 되는지 확인하는 프로그램을 만드시오.

 

입력

첫 줄에 테스트케이스 T, 다음 줄부터 테스트케이스 별로 절대값 1이상 20이하의 정수 10개가 제공된다.

1<=T<=10


출력

\#과 테스트케이스 번호, 빈칸에 이어 부분집합의 합이 0이되는 경우가 있으며 1, 아니면 0을 출력한다.

---

```python
def f(A):
    for i in range(1, 1<<10):     # 10개 원소의 포함 여부 표시
        s = 0
        for j in range(10):
            if i & (1<<j):        # i의 j번 비트가 1이면 A[j]원소가 부분집합에 포함
                s += A[j]
                if s == 0:        # 부분집합을 완성 후 확인
                    return 1
    return 0

T = int(input())
for tc in range(1, T+1):
    arr = list(map(int, input().split()))
    print(f'#{tc} {f(arr)}')
```

​															

### 연습 문제 3

달팽이는 1부터 N*N까지의 숫자가 시계방향으로 이루어져 있다.

다음과 같이 정수 N을 입력 받아 N크기의 달팽이를 출력하시오.

**[제약사항]**

달팽이의 크기 N은 1 이상 10 이하의 정수이다. (1 ≤ N ≤ 10)


**[입력]**

가장 첫 줄에는 테스트 케이스의 개수 T가 주어지고, 그 아래로 각 테스트 케이스가 주어진다.

각 테스트 케이스에는 N이 주어진다.


**[출력]**

각 줄은 '#t'로 시작하고, 다음 줄부터 빈칸을 사이에 두고 달팽이 숫자를 출력한다.

(t는 테스트 케이스의 번호를 의미하며 1부터 시작한다.)

---

```python
T = int(input())

for tc in range(1, T+1):
    N = int(input())
    arr = [[0]*N for _ in range(N)]  # 0 으로 채워진 2차원 배열

    di = [0, 1, 0, -1]               # 방향(k)에 따라 더해줄 값
    dj = [1, 0, -1, 0]
    number = 1                       # 시작 숫자
    i, j = 0, -1                     # 시작 행, 열
    k = 0                            # 방향(0 = 우, 1 = 하, 2 = 좌, 3 = 상)

    while number <= N*N:
        ni, nj = i+di[k], j+dj[k]    # 하나씩 이동한 새로운 행, 열의 값

        # 새로운 행, 열 값이 정해진 범위 안에 유효하고 그 값이 처음 간 0의 값일때
        if 0 <= ni <= N-1 and 0 <= nj <= N-1 and arr[ni][nj] == 0:
            arr[ni][nj] = number
            i, j = ni, nj
            number += 1
        else:
            k = (k+1) % 4

    print(f'#{tc}')
    for i in range(N):
        print(*arr[i], end=" ")
        print()
```

​														

​																										

---

### Sum



다음 100X100의 2차원 배열이 주어질 때, 각 행의 합, 각 열의 합, 각 대각선의 합 중 최댓값을 구하는 프로그램을 작성하여라.

다음과 같은 5X5 배열에서 최댓값은 29이다.



**[제약 사항]**

총 10개의 테스트 케이스가 주어진다.

배열의 크기는 100X100으로 동일하다.

각 행의 합은 integer 범위를 넘어가지 않는다.

동일한 최댓값이 있을 경우, 하나의 값만 출력한다.

**[입력]**

각 테스트 케이스의 첫 줄에는 테스트 케이스 번호가 주어지고 그 다음 줄부터는 2차원 배열의 각 행 값이 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 답을 출력한다.

---

```python
for _ in range(10):
    tc = int(input())   # Test Case 번호
    arry = [list(map(int, input().split())) for _ in range(100)]    # 숫자 배열 입력
 
    max_sum = 0     # 열, 행, 대각선 합중 가장 큰값을 나타낼 변수.
 
    cross_sum_a = 0     # 왼쪽에서 오른쪽으로 가는 대각선의 합을 저장할 변수
    cross_sum_b = 0     # 오른쪽에서 왼쪽으로 가는 대각선의 합을 저장할 변수
    for i in range(100):
        row_sum = 0     # 각 행의 합을 저장
        column_sum = 0  # 각 열의 합을 저장
        for j in range(100):
            row_sum += arry[i][j]
            column_sum += arry[j][i]
 
        cross_sum_a += arry[i][i]
        cross_sum_b += arry[i][99-i]
 
        if row_sum > max_sum:
            max_sum = row_sum
        if column_sum > max_sum:
            max_sum = column_sum
 
    if cross_sum_a > max_sum:
        max_sum = cross_sum_a
    if cross_sum_b > max_sum:
        max_sum = cross_sum_b
 
    print(f'#{tc} {max_sum}')
```

​																							

---

```python
for _ in range(10):
    tc = int(input())
    N = [list(map(int, input().split())) for _ in range(100)]
    max_a = 0  # 행의 최대값
    sum_a = 0  # 행의 합
    max_b = 0  # 열의 최대값
    sum_b = 0  # 열의 합
    max_c = 0  # 대각선1의 합
    max_d = 0  # 대각선2의 합
    ans = 0    # 최댓값

    # 각 행의 합
    for i in range(len(N)):
        sum_a = 0
        for j in range(len(N[i])):
            sum_a += N[i][j]
            if sum_a > max_a:
                max_a = sum_a

    # 각 열의 합
    for j in range(len(N[0])):
        sum_b = 0
        for i in range(len(N)):
            sum_b += N[i][j]
            if sum_b > max_b:
                max_b = sum_b

    # 대각선1의 합
    for i in range(len(N)):
        for j in range(len(N)):
            if i == j:
                max_c += N[i][j]

    # 대각선2의 합
    for i in range(len(N)):
        for j in range(len(N)):
            if i + j == len(N)-1:
                max_d += N[i][j]

    # 최대값 비교
    if max_a > ans:
        ans = max_a
    if max_b > ans:
        ans = max_b
    if max_c > ans:
        ans = max_c
    if max_d > ans:
        ans = max_d

    print(f'#{tc} {ans}')

```

