# :boom: String

---

​													

### 문자열 비교



두 개의 문자열 str1과 str2가 주어진다. 문자열 str2 안에 str1과 일치하는 부분이 있는지 찾는 프로그램을 만드시오.

예를 들어 두 개의 문자열이 다음과 같이 주어질 때, 첫 문자열이 두번째에 존재하면 1, 존재하지 않으면 0을 출력한다.
 

ABC

ZZZZZ**ABC**ZZZZZ

두번째 문자열에 첫번째 문자열과 일치하는 부분이 있으므로 1을 출력.
 

ABC

ZZZZ**A**Z**BC**ZZZZZ

문자열이 일치하지 않으므로 0을 출력.

 
 

**[입력]**
 

첫 줄에 테스트 케이스 개수 T가 주어진다. (1≤T≤50)
 

다음 줄부터 테스트 케이스 별로 길이가 N인 문자열 str1과 길이가 M인 str2가 각각 다른 줄에 주어집니다. (5≤N≤100, 10≤M≤1000, N≤M)

 

**[출력]**
 

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

---

```python
T = int(input())
for tc in range(1, T+1):
    str1 = input()
    str2 = input()
    ans = 0

    for i in range(len(str2)-len(str1)+1):
        if str1[0] == str2[i]:
            check = 1
            for j in range(1,len(str1)):
                if str1[j] == str2[i+j]:
                    check += 1
            if check == len(str1):
                ans = 1
    print(f'#{tc} {ans}')
```

---

​																

### 글자수



두 개의 문자열 str1과 str2가 주어진다. 문자열 str1에 포함된 글자들이 str2에 몇 개씩 들어있는지 찾고, 그중 가장 많은 글자의 개수를 출력하는 프로그램을 만드시오.

예를 들어 str1 = “ABCA”, str2 = “ABABCA”인 경우, str1의 A가 str2에 3개 있으므로 가장 많은 글자가 되고 3을 출력한다.

파이썬의 경우 딕셔너리를 이용할 수 있다.


**[입력]**

첫 줄에 테스트 케이스 개수 T가 주어진다. 1≤T≤50

다음 줄부터 테스트 케이스 별로 길이가 N인 문자열 str1과 길이가 M인 str2가 각각 다른 줄에 주어진다. 5≤N≤100, 10≤M≤1000, N≤M

**[출력]**

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

---

```python
T = int(input())

for tc in range(1, T+1):
    str1 = input()
    str2 = input()
    max_cnt = 0

    for i in range(len(str1)):
        cnt = 0
        for j in range(len(str2)):
            if str1[i] == str2[j]:
                cnt += 1
        if cnt > max_cnt:
            max_cnt = cnt

    print(f'#{tc} {max_cnt}')
```

---

​									

### 회문



ABBA처럼 어느 방향에서 읽어도 같은 문자열을 회문이라 한다. NxN 크기의 글자판에서 길이가 M인 회문을 찾아 출력하는 프로그램을 만드시오.

회문은 1개가 존재하는데, 가로 뿐만 아니라 세로로 찾아질 수도 있다.
 

예를 들어 N=10, M=10 일 때, 다음과 같이 회문을 찾을 수 있다.



**[입력]**
 

첫 줄에 테스트 케이스 개수 T가 주어진다. 1≤T≤50

다음 줄부터 테스트케이스의 첫 줄에 N과 M이 주어진다. 10≤N≤100, 5≤M≤N

다음 줄부터 N개의 글자를 가진 N개의 줄이 주어진다.

 

**[출력]**
 

각 줄마다 "#T" (T는 테스트 케이스 번호)를 출력한 뒤, 답을 출력한다.

---

```python
T = int(input())

for tc in range(1, T+1):
    N, M = map(int, input().split())
    arr = [input() for _ in range(N)]    # input 값을 어떻게 저장할 지 고민하고 적어야함
    ans = 0
    for i in range(N):                   # 행에 대한 검사
        for j in range(N-M+1):
            X_word = arr[i][j:j+M]
            if X_word == X_word[::-1]:
                ans = X_word
                break

    if ans == 0:                         # 행에서 못찾았다면,
        for i in range(N):               # 열에 대한 검사 진행
            for j in range(N-M+1):
                Y_word = ''
                for k in range(M):
                    Y_word += arr[k+j][i]
                if Y_word == Y_word[::-1]:
                    ans = Y_word

    print(f'#{tc} {ans}')
```

---

​																																		

### 백만장자 프로젝트

​													

25년 간의 수행 끝에 원재는 미래를 보는 능력을 갖게 되었다. 이 능력으로 원재는 사재기를 하려고 한다.

다만 당국의 감시가 심해 한 번에 많은 양을 사재기 할 수 없다.

다음과 같은 조건 하에서 사재기를 하여 최대한의 이득을 얻도록 도와주자.

  \1. 원재는 연속된 N일 동안의 물건의 매매가를 예측하여 알고 있다.
  \2. 당국의 감시망에 걸리지 않기 위해 하루에 최대 1만큼 구입할 수 있다.
  \3. 판매는 얼마든지 할 수 있다.

예를 들어 3일 동안의 매매가가 1, 2, 3 이라면 처음 두 날에 원료를 구매하여 마지막 날에 팔면 3의 이익을 얻을 수 있다.


**[입력]**

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 테스트 케이스 별로 첫 줄에는 자연수 N(2 ≤ N ≤ 1,000,000)이 주어지고,

둘째 줄에는 각 날의 매매가를 나타내는 N개의 자연수들이 공백으로 구분되어 순서대로 주어진다.

각 날의 매매가는 10,000이하이다.


**[출력]**

각 테스트 케이스마다 ‘#x’(x는 테스트케이스 번호를 의미하며 1부터 시작한다)를 출력하고, 최대 이익을 출력한다.


**[예제 풀이]**

1번째 케이스는 아무 것도 사지 않는 것이 최대 이익이다.

2번째 케이스는 1,2일에 각각 한 개씩 사서 세 번째 날에 두 개를 팔면 10의 이익을 얻을 수 있다.

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

### 가장 빠른 문자열 타이핑

​																								

어떤 문자열 A를 타이핑하려고 한다.

그냥 한 글자씩 타이핑 한다면 A의 길이만큼 키를 눌러야 할 것이다.

여기에 속도를 조금 더 높이기 위해 어떤 문자열 B가 저장되어 있어서 키를 한번 누른 것으로 B전체를 타이핑 할 수 있다.

이미 타이핑 한 문자를 지우는 것은 불가능하다.

예를 들어 A=”asakusa”, B=”sa”일 때, 다음 그림과 같이 B를 두 번 사용하면 5번 만에 A를 타이핑 할 수 있다.



A와 B가 주어질 때 A 전체를 타이핑 하기 위해 키를 눌러야 하는 횟수의 최솟값을 구하여라.


**[입력]**

첫 번째 줄에 테스트 케이스의 수 T가 주어진다.

각 테스트 케이스마다 첫 번째 줄에 두 문자열 A, B가 주어진다. A의 길이는 1이상 10,000이하, B의 길이는 1이상 100이하이다.


**[출력]**

각 테스트 케이스마다 A 전체를 타이핑 하기 위해 키를 눌러야 하는 횟수의 최솟값을 출력한다.

---

```python
T = int(input())

for tc in range(1, T+1):
    A, B = input().split()

    cnt = 0
    start = 0                              # 시작 맨앞 변수 설정
    while start < len(A)-len(B)+1:         # 시작점에서 문자열 B 길이에 따른 범위까지
        if A[start:start+len(B)] == B:     # 슬라이싱 했을 때 같으면
            cnt += 1                       # 횟수 추가
            start += len(B)                # 이게 중요 포인트, 찾으면 그 길이만큼 넘어가야함. for 문은 오류발생 쉬움
        else:
            start += 1                     # 같지 않으면 다음으로 넘어감

    ans = len(A) - (len(B) * cnt) + cnt    # 문자열 B 길이*횟수 만큼 빼주고 대신 횟수 추가

    print(f'#{tc} {ans}')

```

---

​																																

### 회문2

​																																					

---

```python
for tc in range(1,11):
    n = int(input())
    arr = [input() for _ in range(100)]

    max_long = 0

    for i in range(100):                  # 행 조사
        for j in range(100):              # 시작점
            for k in range(j+1, 100):     # 끝
                check = 0
                while check < k-j+1:      # k-j+1은 회문의 길이. 회문의 길이와 check 가 같아질 때 까지.
                    if arr[i][j+check] == arr[i][k-check]:
                        check += 1
                    else:                 # 같지 않으면 중간에 중단됨
                        break
                if check == (k-j+1):      # 중단되서 나온게 아니라 회문길이와 체크가 같아서 나왔다면,
                    if k-j+1 > max_long:  # 회문 길이를 최대 길이와 비교해서 설정
                        max_long = k-j+1

    for i in range(100):                  # 열 조사
        for j in range(100):              # 시작점
            for k in range(j+1, 100):     # 끝
                check = 0
                while check < k-j+1:      # 행과 방식이 같음
                    if arr[j+check][i] == arr[k-check][i]:
                        check += 1
                    else:
                        break
                if check == (k-j+1):
                    if k-j+1 > max_long:
                        max_long = k-j+1

    print(f'#{tc} {max_long}')
```

---

