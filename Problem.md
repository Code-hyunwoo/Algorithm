# :boom: Problem

---

​																																						

## 백만장자 프로젝트													

---

```python
T = int(input())
for tc in range(1, T+1):
    n = int(input())
    m = list(map(int, input().split()))
    money = 0                            # 최대 이익의 합 변수 설정

    for i in range(n):
        profit = 0                       # 미래에 팔았을 때 얻는 이익 변수 설정
        max_profit = 0                   # 이익들을 비교했을 때 최대 이익 변수 설정
        for j in range(i+1, n):
            if m[j] - m[i] > 0:
                profit = m[j] - m[i]
                if profit > max_profit:
                    max_profit = profit  # 이익 들 중에 최대만 기록해서
        money += max_profit              # 최대 이익 합 변수에 추가

    print(f'#{tc} {money}')
```

---

```python
T = int(input())
for tc in range(1, T+1):
    n = int(input())
    m = list(map(int, input().split()))
    max_profit = 0                     # 최대이익 이익들의 합
    best = m[-1]                       # 마지막 날 값을 최대라고 가정

    for i in range(n-1, -1, -1):       # 뒤에서부터 비교
        if m[i] > best:                # 마지막날보다 값이 크면
            best = m[i]                # 최대가격 변경
        else:
            max_profit += best - m[i]  # 아니면 최대에서 가격 빼서 이익 추가

    print(f'#{tc} {max_profit}')
```

---

​													

## 숫자 배열 회전

---

```python

def rotate(arr):                             # 90도 회전했을 때 새로운 배열을 정의하는 함수
    new_arr = [[0]*N for _ in range(N)]
    for i in range(N):
        for j in range(N):
            new_arr[i][j] = arr[N-j-1][i]    # 90도 회전에 따른 대칭점을 고려하여 설정
    return new_arr

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    arr = [list(map(int, input().split())) for _ in range(N)]

    rotate_90 = rotate(arr)                  # 주어진 행렬을 90도 회전한 배열
    rotate_180 = rotate(rotate_90)           # 90도에서 다시 90도 회전한 배열
    rotate_270 = rotate(rotate_180)          # 180도 에서 다시 90도 회전한 배열

    print(f'#{tc}')
    for i in range(N):                       # 문자열 속성 부여, join 으로 붙이고 띄어쓰기 주의
        print(''.join(map(str, rotate_90[i])), ''.join(map(str, rotate_180[i])), ''.join(map(str, rotate_270[i])))
```

---

​																		

## 스도쿠 검증

---

```python

T = int(input())

for tc in range(1, T+1):
    sdoku = [list(map(int, input().split())) for _ in range(9)]
    square = [0, 3, 6]                 # 사각형 검사를 위한 리스트
    ans = 1

    for i in range(9):                 # 가로행 검사
        x = [0] * 10                   # 카운팅을 위한 리스트 생성
        for j in range(9):
            x[sdoku[i][j]] += 1
        for k in range(1, 10):
            if x[k] != 1:              # 카운팅했을 때 1이 아니면
                ans = 0                # 답은 0이고 break 로 그만
                break
    if ans == 1:                       # 세로행 검사 (가로행 검사 통과했을 경우)
        for i in range(9):
            y = [0] * 10
            for j in range(9):
                y[sdoku[j][i]] += 1
            for k in range(1, 10):
                if y[k] != 1:
                    ans = 0
                    break
    if ans == 1:                        # 사각형 검사 (가로행과 세로행 모두 통과했을 경우)
        for i in square:
            for j in square:
                z = [0] * 10
                for k in range(3):
                    for q in range(3):
                        z[sdoku[i+k][j+q]] += 1
                for l in range(1, 10):
                    if z[l] != 1:
                        ans = 0
                        break

    print(f'#{tc} {ans}')
```

---

​																		

## 어디에 단어가 들어갈 수 있을까

---

```python

T = int(input())
for tc in range(1, T+1):
    N, K = map(int, input().split())
    arr = [list(map(int, input().split())) for _ in range(N)]
    ans = 0

    for i in range(N):                 # 가로행에 대한 검사
        check = 0
        for j in range(N):  
            if arr[i][j] == 1:         # 해당 인덱스 행렬 값이 1이면
                check += 1             # 카운팅
                if j == N-1:           # 마지막 열인 경우
                    if check == K:     # 카운팅이 단어 길이와 같으면
                        ans += 1       # 답 +1
            else:                      # 해당 인덱스 행렬 값이 0이면
                if check == K:         # 이전까지 카운팅한 값이 K인 경우
                    ans += 1           # 답 +1
                check = 0              # 카운팅 값 0 으로 초기화

    for i in range(N):                 # 세로행에 대한 검사, 가로와 방식 같음
        check = 0
        for j in range(N):
            if arr[j][i] == 1:
                check += 1
                if j == N-1:
                    if check == K:
                        ans += 1
            else:
                if check == K:
                    ans += 1
                check = 0

    print(f'#{tc} {ans}')

```

---

​																		

## 자기 방으로 돌아가기

---

```python

```

---

​																		

## 의석이의 세로로 말해요

---

```python

T = int(input())
for tc in range(1, T+1):
    arr = [input() for _ in range(5)]
    word = ''
    for i in range(15):            # 최대 길이가 15이하인 문자열이 주어지므로 범위는 15
        for j in range(5):         # 행이 계속 5개로 돈다.
            if len(arr[j]) > i:    # 열 인덱스 값 i가 입력 문자열들의 길이를 벗어나지 않는 범위안에 있으면
                word += arr[j][i]  # 문자열 읽기

    print(f'#{tc} {word}')
```

---

​																		

## 쇠막대기 자르기

---

```python

```

---

​																		

## 삼성시의 버스 노선

---

```python

```

---

​																		

