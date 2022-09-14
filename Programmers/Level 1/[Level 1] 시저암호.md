# Level 1

---

​																									




```python
def solution(s, n):
    s= list(s)
    for i in range(len(s)):
        if s[i].isupper():
            s[i] = chr((ord(s[i])-ord('A') + n) % 26 + ord('A'))
        elif s[i].islower():
            s[i] = chr((ord(s[i])-ord('a') + n) % 26 + ord('a'))

    return "".join(s)

문자열은 수정 불가능한 자료 구조로, 인덱스를 통해서 수정할 수 없다.
따라서, 이런 경우는 리스트 변환하여 수정 후 다시 문자열로 변환한다. 
"AB" -> ["A","B"]
"a b" -> ["a", " ", "b"]
```

---

​												

```python
def caesar(s, n):
    lower_list = "abcdefghijklmnopqrstuvwxyz"
    upper_list = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

    result = []

    for i in s:
        if i is " ":
            result.append(" ")
        elif i.islower() is True:
            new_ = lower_list.find(i) + n
            result.append(lower_list[new_ % 26])
        else:
            new_ = upper_list.find(i) + n
            result.append(upper_list[new_ % 26])
    return "".join(result)
```

---



```python
def solution(d, budget):
    d.sort()
    cnt = 0
    # if sum(d) == budget :
    #     answer = len(d)
    # elif sum(d) < budget :
    #     for i in d :
    #         budget -= i
    #         cnt += 1
    #         answer = cnt
    # else :
    for i in d :
        budget -= i
        if budget < 0 :
               break
        cnt += 1
    answer = cnt
    return answer
```

