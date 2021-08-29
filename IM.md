# :boom: IM 대비

---



### 토글

​			

```python

T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]

    for k in range(1, M+1):
        for i in range(N):
            for j in range(N):
                if M % k == 0 or k == M:                # M이 k의 배수 이거나 k가 M 인 경우
                    if arr[i][j] == 0:                  # 전체를 토글
                        arr[i][j] = 1
                    else:
                        arr[i][j] = 0
                else:                                   # 그냥 k초 일 경우
                    if i+j+2 == k or (i+j+2) % k == 0:  # 문제가 첫 항이 1부터 시작한다는 점을 유의
                        if arr[i][j] == 0:              # 행열의 합이 k와 같거나 k의 배수인 경우 해당 행열 토글 
                            arr[i][j] = 1
                        else:
                            arr[i][j] = 0
    cnt = 0
    for a in range(N):             
        for b in range(N):
            if arr[a][b] == 1:
                cnt += 1

    print(f'#{tc} {cnt}')

```

---



### 파리퇴치 3

​				

```python

T = int(input())
for tc in range(1, T+1):
    N, M = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]

    max_kill = 0

    # 1. 십자 모양 스프레이

    for i in range(N):
        for j in range(N):
            kill = 0
            for a in range(-(M-1), M, 1):         # 선택한 행렬의 가로줄 뿌리기. 범위 설정이 중요
                if 0 <= i+a < N:                  # 가로로 뿌릴 구역이 범위내에 있으면
                    kill += arr[i+a][j]           # 파리퇴치
            for b in range(-(M-1), M, 1):         # 선택한 행렬의 세로줄 뿌리기
                if 0 <= j+b < N:
                    kill += arr[i][j+b]
            kill -= arr[i][j]                     # 선택한 행렬이 두 번 뿌려졌으므로 한번 제외
            if max_kill < kill:                   # 최댓값 비교
                max_kill = kill

    # 2. x자 모양 스프레이

    for i in range(N):
        for j in range(N):
            kill = 0
            for a in range(-(M-1), M, 1):         # 선택한 행렬의 좌상향 방향으로 뿌리기
                if 0 <= i+a < N and 0 <= j+a < N: # 뿌릴 구역이 범위내에 있으면
                    kill += arr[i+a][j+a]
            for b in range(-(M-1), M, 1):         # 선택한 행렬의 우상향 방향으로 뿌리기
                if 0 <= i+b < N and 0 <= j-b < N: # 뿌릴 구역 범위내 변수 주의하기
                    kill += arr[i+b][j-b]
            kill -= arr[i][j]                     # 선택한 행렬이 두 번 뿌려졌으므로 한번 제외
            if max_kill < kill:
                max_kill = kill

    print(f'#{tc} {max_kill}')
```

---

```python
def plus(area, x, y, n, m): # + 모양
    cnt = area[y][x]
    for i in range(1, m):
        for dx, dy in [[0, 1], [0, -1], [1, 0], [-1, 0]]: # 방향
            nx, ny = x + i*dx, y + i*dy
            if 0<= nx < n and 0<= ny < n :
                cnt += area[ny][nx]
    return cnt
 
 
def cross(area, x, y, n, m): # x 모양
    cnt = area[y][x]
    for i in range(1, m):
        for dx, dy in [[-1, -1], [1, -1], [-1, 1], [1, 1]]: # 방향
            nx, ny = x + i*dx, y + i*dy
            if 0<= nx < n and 0<= ny < n :
                cnt += area[ny][nx]
    return cnt
 
 
T = int(input())
for tc in range(1, T+1):
    n, m = map(int, input().split())
    area = [list(map(int, input().split())) for _ in range(n)]
     
    res = 0
    for y in range(n):
        for x in range(n):
            res1, res2 = plus(area, x, y, n, m), cross(area, x, y, n, m)
            res = max(res, res1, res2)
             
    print(f'#{tc} {res}')
```

---

​																			

​																

### 오목 판정

​				

```python
def check(table, N):
    di = [0, 1, 1, 1]
    dj = [1, 0, 1, -1]
    for i in range(N):
        for j in range(N):
            if table[i][j] == 'o':
                for k in range(4):
                    cnt = 1
                    ni = i + di[k]
                    nj = j + dj[k]
                    while True:
                        if 0 <= ni < N and 0 <= nj < N and table[ni][nj] == 'o':
                            cnt += 1
                            ni += di[k]
                            nj += dj[k]
                        else:
                            break
                    if cnt == 5:
                        return 'YES'
    return 'NO'


T = int(input())

for tc in range(1, T + 1):
    N = int(input())
    table = [list(input()) for _ in range(N)]

    print('#{} {}'.format(tc, check(table, N)))
```

---

​				

```python

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    omok = [list(input()) for _ in range(N)]
    ans = 'NO'
    for i in range(N):
        for j in range(N):
            if omok[i][j] == 'o':                   # 선택한 행렬이 o 일 때 출발
                cnt = 1                             # 오목 카운트 1
                # 가로 확인
                for k in range(j+1, N):             # 오른쪽으로 끝까지 확인
                    if omok[i][k] == 'o':           # 다음 열이 o이면 카운트, 오목 카운트 확인
                        cnt += 1
                        if cnt >= 5:                # 오목 카운트가 5가 되면
                            ans = 'YES'
                            break                   # 중단
                        else:
                            continue
                    else:                           # 다음 열이 o이 아니면 그만.
                        cnt = 1
                        break
                else:                               # 가로행을 다 돌았는데, 오목은 아니나 돌로 끝나는 경우
                    cnt = 1                         # 다음 세로 확인을 위해 카운트 초기화 해줘야함

                # 세로 확인
                for q in range(i+1, N):
                    if omok[q][j] == 'o':
                        cnt += 1
                        if cnt >= 5:
                            ans = 'YES'
                            break
                        else:
                            continue
                    else:
                        cnt = 1
                        break
                else:
                    cnt = 1

                # 대각선(우상향) 확인
                for a in range(1, N):                 # 선택한 행렬에서 오른쪽위 대각선으로 오목이 되는 경우 확인
                    if 0 <= i-a < N and 0 <= j+a < N: # 범위 내에 있을 때
                        if omok[i-a][j+a] == 'o':
                            cnt += 1
                            if cnt >= 5:
                                ans = 'YES'
                                break
                            else:
                                continue
                        else:
                            cnt = 1
                            break
                    else:                             # 범위를 나가서 끝나는 경우 카운트를 1로 초기화하고 끝내야함
                        cnt = 1
                        break
                # 대각선(좌상향) 확인
                for b in range(1, N):                 # 선택한 행렬에서 왼쪽위 대각선으로 오목이 되는 경우 확인
                    if 0 <= i-b < N and 0 <= j-b < N:
                        if omok[i-b][j-b] == 'o':
                            cnt += 1
                            if cnt >= 5:
                                ans = 'YES'
                                break
                            else:
                                continue
                        else:
                            cnt = 1
                            break
                    else:                             # 범위를 나가서 끝나는 경우 카운트를 1로 초기화하고 끝내야함
                        cnt = 1
                        break
    print(f'#{tc} {ans}')

```



---



### 타일로봇	

​									

```python

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [[0] * 10 for _ in range(10)]
    cnt = 0
    for _ in range(N):
        x1, y1, x2, y2 = map(int, input().split())

        for i in range(x1, x2+1):
            for j in range(y1, y2+1):
                if arr[i][j] == 0:
                    arr[i][j] = 1
                    cnt += 1

    print('#{} {}'.format(tc, cnt))
```









### 정곤이의 단조 증가하는 수

​				

```python

def danjo(n):
    a = []
    while n > 0:
        a.append(n % 10)   # 모든 자릿수를 1의 자리부터 하나씩 리스트에 추가
        n = n // 10

    for i in range(1, len(a)):            # 리스트를 돌면서
        if a[i] <= a[i-1]:                # 앞 항이 바로 뒷 항보다 크거나 같은경우
            continue                      # 계속 진행
        else:                             # 중간에 그렇지 않다면
            return 0                      # 단조가 아님
    return 1                              # for문 다 돌았으면 단조

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    num = list(map(int, input().split()))
    maxV = -1                             # 단조가 없으면 -1 출력해야 되니까 -1로 설정

    for i in range(N-1):
        tmpV = 0
        for j in range(i+1, N):
            if danjo(num[i] * num[j]) == 1:    # 단조이면
                tmpV = num[i] * num[j]         # 값 저장
                if tmpV > maxV:                # 최댓값 찾기
                    maxV = tmpV


    print(f'#{tc} {maxV}')
```

---

```python
def check(num): # 단조 증가 판단
    number = list(str(num))
    for i in range(len(number)-1):
        if number[i] > number[i+1] :
            return 0
    return 1
 
 
T = int(input())
for tc in range(1, T+1):
    n = int(input())
    nums = list(map(int, input().split()))
     
    res = -1
    for i in range(n-1):
        for j in range(i+1, n):
            num = nums[i]*nums[j]
            if num <= res:
                continue
             
            if check(num) and res < num: # 단조 증가이면서 값이 더 큰 경우 변환
                res = num
    print(f'#{tc} {res}')
```

---

​																											

### 퍼펙트 셔플

​																				

```python
T = int(input())
for tc in range(1, T+1):
    N = int(input())
    card = list(input().split())
    new = []
    if N % 2 == 0:   # N이 짝수 일 때,
        for i in range(N // 2):
            new.append(card[i])
            new.append(card[(N // 2) + i])
    else:            # N이 홀수 일 때,
        for i in range(N // 2):
            new.append(card[i])
            new.append(card[(N // 2) + i + 1])
        new.append(card[N//2])

    print('#{}'.format(tc), end=' ')
    for k in range(N):
        print('{}'.format(new[k]), end=' ')
    print()
```

​																												

### 스도쿠 검증

​																														

```python

T = int(input())
for tc in range(1, T+1):
    sdoku = [list(map(int, input().split())) for _ in range(9)]
    check = [0] + [1]*9

    cnt = 0
    for i in range(9):
        count_a = [0] * 10
        count_b = [0] * 10
        for j in range(9):
            count_a[sdoku[i][j]] += 1
            count_b[sdoku[j][i]] += 1
        if count_a == check:
            cnt += 1
        if count_b == check:
            cnt += 1

    nemo_start = [0, 3, 6]
    for i in nemo_start:
        for j in nemo_start:
            count_c = [0] * 10
            for k in range(3):
                for q in range(3):
                    count_c[sdoku[i+k][j+q]] += 1
                if count_c == check:
                    cnt += 1
    if cnt == 27:
        ans = 1
    else:
        ans = 0

    print('#{} {}'.format(tc, ans))
```

---



### 진기의 최고급 붕어빵

​				

```python

T = int(input())
for tc in range(1, T+1):
    N, M, K = map(int, input().split())
    guest = list(map(int, input().split()))
    guest.sort()          # 손님들을 도착 시간에 따라 오름차순 정렬
    boong = 0             # 붕어빵 갯수
    t = 0                 # 시간초
    ans = 'Possible'      # 불가능 뜨지 않으면 다 가능하다는 의미
    cnt = 0               # 붕어빵을 사간 손님수 카운트

    while t <= guest[-1]:                      # 마지막 손님이 올 때까지 실행
        if t > 0 and t % M == 0:               # t가 0 보다 크고, M의 배수 일 때마다
            boong += K                         # 붕어빵 K개씩 생성
        for i in range(N):
            if guest[i] == t:                  # 게스트가 해당 시간에 왔을 때
                if boong != 0:                 # 붕어빵이 있으면
                    boong -= 1                 # 붕어빵 하나 빼고
                else:                          # 붕어빵이 없으면
                    ans = 'Impossible'         # 불가능
                    break
        t += 1

    print(f'#{tc} {ans}')
```

---

```python
T = int(input())
for tc in range(1, T+1):
    N, M, K = map(int, input().split())
    guest = list(map(int, input().split()))
    guest.sort()       # 손님들을 도착 시간에 따라 오름차순 정렬
    ans = 'Possible'   # 불가능한 경우가 없으면 가능하다는 의미

    for i, time in enumerate(guest, start=1):    # 정렬된 손님리스트에 대하여
        if (time//M)*K < i:        # 손님이 오는 시간을 M으로 나눈 몫에 만들 수 있는 붕어빵 K을 곱했을 때
            ans = 'Impossible'     # i(== 손님수) 보다 만든 붕어빵의 총합이 작으면 불가능
            break

    print(f'#{tc} {ans}')
```

​																	

### Magnetic

​				

```python
T = 10
for tc in range(1, T+1):
    N = int(input())
    table = [list(map(int, input().split())) for _ in range(N)]
    cnt = 0    # 교착 상태 카운트
    # 1은 N극, 2는 S극
    for i in range(N):
        mag = 0                      # 열 바뀌면 초기화
        for j in range(N):           # 한 열씩 검사
            if table[j][i] == 1:     # N극 자성체이면
                mag = 1              # 자력 1인 상태로 내려감
            elif table[j][i] == 2:   # 그다음 열 조사할 때, S극 자성체이면,
                if mag == 1:         # 만약 자력이 1인 상태라면
                    cnt += 1         # 둘이 만나서 교착 됨
                    mag = 0          # 교착되고 자력 0으로 초기화

    print('#{} {}'.format(tc, cnt))
```

