# Level 1

---

​																									




```python
def solution(strings, n):
    strings.sort() 
    return sorted(strings, key=lambda x:x[n])
```

---

​												

```python
def solution(strings, n):
    return sorted(strings, key=lambda x:(x[n],x))
```

---



```python

```

