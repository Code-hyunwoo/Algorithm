# Level 1

---

​																									




```python
def solution(n):
    answer = 0
    numlist = list(str(n))
    numlist.sort(reverse=True)
    answer = int("".join(numlist))    
    return answer
```

---

​												

```python
def solution(n):
    return int("".join(sorted(list(str(n)), reverse=True)));
```

---



```python

```

