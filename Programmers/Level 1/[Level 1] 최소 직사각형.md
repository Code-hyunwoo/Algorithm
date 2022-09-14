# Level 1

---

​																									




```python
def solution(sizes):
    
    answer = 0
    garo = []
    sero = []
    
    for i in sizes:
        garo.append(i[0])
        sero.append(i[1])
    
    once = 0
    if max(garo) > max(sero):
        once = max(garo)
    else:
        once = max(sero)
        
        
    twice = 0
    for j in sizes:
        if twice < sorted(j)[0]:
            twice = sorted(j)[0]
            
    answer = once * twice
    
    return answer
```

---

​												

```python
def solution(sizes):
    return max(max(x) for x in sizes) * max(min(x) for x in sizes)
```

---



```python

```

