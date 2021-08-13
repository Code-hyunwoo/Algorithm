# :boom: String

---

​					

### Ladder1

---



```python
def search(start):
    i = 99
    j = start
    while i > 0:  # 맨 윗줄에 도착하기 전까지 올라감
        i -= 1    # 위로 한 칸 이동
        if j > 0 and ladder[i][j-1] == 1: # 왼쪽 칸이 1이면
            while j > 0 and ladder[i][j-1]:  # 0을 만날 때 까지 이동
                j -= 1
        elif j < 99 and ladder[i][j+1] == 1: # 오른쪽 칸이 있고 1이면
            while j < 99 and ladder[i][j+1] == 1:
                j += 1
            # 좌우가 0이면 위로
    return j  # 0번행에 도착 했을 때의 열 리턴


for _ in range(10):
    tc = int(input())
    ladder = [list(map(int, input().split())) for _ in range(100)]

    for i in range(100):
        if ladder[99][i] == 2:
            start = i

    print(f'#{tc} {search(start)}')
```

---

​									

### GNS

숫자 체계가 우리와 다른 어느 행성이 있다. 아래는 이 행성에서 사용하는 0 ~ 9의 값을 순서대로 나타낸 것이다.

**"ZRO", "ONE", "TWO", "THR", "FOR", "FIV", "SIX", "SVN", "EGT", "NIN"**

0 ~ 9 의 값을 나타내는 단어가 섞여 있는 문자열을 받아 작은 수부터 차례로 정렬하여 출력하는 프로그램을 작성하라.

예를 들어 입력 문자열이 **"TWO NIN TWO TWO FIV FOR"** 일 경우 정렬한 문자열은 **"TWO TWO TWO FOR FIV NIN"** 이 된다.

**[입력]**

입력 파일의 첫 번째 줄에는 테스트 케이스의 개수가 주어진다.

그 다음 줄에 #기호와 함께 테스트 케이스의 번호가 주어지고 공백문자 후 테스트 케이스의 길이가 주어진다.

그 다음 줄부터 바로 테스트 케이스가 주어진다. 단어와 단어 사이는 하나의 공백으로 구분하며, 문자열의 길이 N은 100≤N≤10000이다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 정렬된 문자열을 출력한다.

---

```python
T = int(input())

for tc in range(1, T+1):
    x, N = input().split()
    N = int(N)
    arr = input().split()

    number_list = ["ZRO", "ONE", "TWO", "THR", "FOR", "FIV", "SIX", "SVN", "EGT", "NIN"]
    count_list = [0] * 10                    # 카운팅을 위한 리스트 생성

    for i in range(10):                      # 0부터 9까지 인덱스 범위에 대해서
        for j in range(N):                   # 모든 입력 된 배열을 순회
            if number_list[i] == arr[j]:     # 외계 숫자문자열과 입력값이 같다면
                count_list[i] += 1           # 카운팅

    print(f'#{tc}')
    for k in range(10):
        num = number_list[k] + " "           # 외계 문자열을 띄어쓰기를 포함한 새 변수 설정
        print(num * count_list[k], end='')   # 변수 * 카운팅한 값 출력
        print()
```

---

​				

### string

주어지는 영어 문장에서 특정한 문자열의 개수를 반환하는 프로그램을 작성하여라.

Starteatingwellwiththeseeighttipsforhealthyeating,whichcoverthebasicsofahealthydietandgoodnutrition.

위 문장에서 ti 를 검색하면, 답은 4이다.

**[제약 사항]**

총 10개의 테스트 케이스가 주어진다.

문장의 길이는 1000자를 넘어가지 않는다.

한 문장에서 검색하는 문자열의 길이는 최대 10을 넘지 않는다.

한 문장에서는 하나의 문자열만 검색한다. 

**[입력]**

각 테스트 케이스의 첫 줄에는 테스트 케이스의 번호가 주어지고 그 다음 줄에는 찾을 문자열, 그 다음 줄에는 검색할 문장이 주어진다.

**[출력]**

\#부호와 함께 테스트 케이스의 번호를 출력하고, 공백 문자 후 테스트 케이스의 답을 출력한다.

---

```python
T = 10
for tc in range(1, T+1):
    num = int(input())
    found = input()
    sentence = input()
    cnt = 0
    for i in range(len(sentence) - len(found) + 1):
        if sentence[i:i+len(found)] == found:
            cnt += 1

    print(f'#{tc} {cnt}')
```

​														

```python
T = 10
for tc in range(1, T+1):
    N = int(input())
    find_word = input()
    sentence = input()
    cnt = 0
    i = 0                                            # 문장의 인덱스
    j = 0                                            # 찾는 단어의 인덱스

    while i <= len(sentence)-len(find_word) + 1:     # 문장 인덱스가 이동할 수 있는 범위내에서 끝까지 반복
        if sentence[i] == find_word[j]:              # 문장 인덱스와 단어 인덱스가 같다면
            i += 1                                   # 문장 인덱스 1 이동

            if j == len(find_word)-1:                # 단어 인덱스가 마지막 인덱스라면
                cnt += 1                             # 찾는 단어를 찾았으니 카운트 추가
                j = 0                                # 추가 후 단어 인덱스 다시 0으로 초기화

            else:                                    # 찾는단어의 마지막 인덱스가 아니면 단어 인덱스 한 칸 이동
                j += 1
        else:                                        # 문장 인덱스와 단어 인덱스가 같지 않다면
            if j != 0:                               # 찾는 단어 인덱스 원점으로 돌리기
                j = 0
            else:                                    # 단어 인덱스도 원점이고, 값도 같지 않으면
                i += 1                               # 문장 인덱스 다음칸으로 이동

    print(f'#{tc} {cnt}')
```

​									

```python
T = 10
for tc in range(1, T+1):
    num = int(input())
    find = input()
    sentence = input()
    cnt = 0

    for i in range(len(sentence)-1):
        if sentence[i] == find[0]:
            check = 1
            for j in range(1, len(find)):
                if sentence[i+j] == find[j]:
                    check += 1
            if check == len(find):
                cnt += 1

    print(f'#{tc} {cnt}')
```

---



