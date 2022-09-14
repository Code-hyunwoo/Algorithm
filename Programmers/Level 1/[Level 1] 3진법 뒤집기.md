# Level 1

---

​																									




```python
def solution(n):
    answer = 0
    
    rev_base = ''

    while n > 0:
        n, mod = divmod(n, 3)
        rev_base += str(mod)
    
    answer = int(rev_base,3)
        
    return answer
```

---

​												

```python
def sumMatrix(A,B):
    answer = [[c + d for c, d in zip(a, b)] for a, b in zip(A,B)]
    return answer
```

---



```python

```

