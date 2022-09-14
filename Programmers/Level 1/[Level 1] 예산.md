# Level 1

---

​																									




```python
def solution(d, budget):
    answer = len(d)
    
    total = sum(d)
    dlist = sorted(d,reverse=True)
    
    for i in range(len(d)):
        
        if total > budget:
            if total - dlist[i] <= budget:
                return answer-1
            else:       
                total -= dlist[i]
                answer -= 1 
        else:
            return answer

```

---

​												

```python
def solution(d, budget):
    d.sort()
    while budget < sum(d):
        d.pop()
    return len(d)
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

