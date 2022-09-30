# Level 1

---

​																									




```python
def solution(lottos, win_nums):
    answer = []
    
    random = lottos.count(0)
    check = 0
    for i in lottos:
        if i in win_nums:
            check += 1
    
    if random+check ==0:
        answer.append(6)
    else:
        answer.append(7-(random+check))
    
    if check == 0:
        answer.append(6)
    else:
        answer.append(7-check)
    
    
    return answer
```

---

​												

```python

def solution(lottos, win_nums):

    rank=[6,6,5,4,3,2,1]

    cnt_0 = lottos.count(0)
    ans = 0
    for x in win_nums:
        if x in lottos:
            ans += 1
    return rank[cnt_0 + ans],rank[ans]
```

---



```python

```

