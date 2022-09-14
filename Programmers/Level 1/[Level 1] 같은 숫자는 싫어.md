# Level 1

---

​																									




```python
def solution(arr):
    answer = []
    
    for i in arr:
        
        if answer == []:
            answer.append(i)
        elif answer[-1] != i:
            answer.append(i)
        else:
            pass
        
    return answer
```

---

​												

```python
def no_continuous(s):
    a = []
    for i in s:
        if a[-1:] == [i]: continue
        a.append(i)
    return a
```

---



```python

```

