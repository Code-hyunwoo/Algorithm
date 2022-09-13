# Level 1

---

​																									




```python
def solution(n):
    answer = 0
    num = n ** 0.5
    
    if num == int(num):
        answer = (num+1)**2
        
    else: answer = -1
    return answer
```

---

​												

```python
def nextSqure(n):
    for x in range(1,n) :
        if x ** 2 == n :
            return (x+1) ** 2
    return "no"
```

---



```python

```

