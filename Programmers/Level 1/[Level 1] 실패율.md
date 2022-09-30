# Level 1

---

​																									




```python
def solution(N, stages):
    answer = []
    arr =[]
    for i in range(1,N+1):
        start = 0
        fail = 0
        for j in stages:
            if j >= i:
                start += 1
            if j == i:
                fail += 1
                
        if start != 0:
            arr.append(fail/start)
        else:
            arr.append(0)
            
    answer = sorted(range(1,len(arr)+1), key=lambda k: arr[k-1], reverse=True)
    return answer
```

---

​												

```python

```

---



```python

```

