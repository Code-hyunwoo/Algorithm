# Level 1

---

​																									




```python
def solution(s):
    answer = True
    
    Pcount = 0
    Ycount = 0
    
    for i in s:
        if i == "p" or i == "P":
            Pcount += 1
        elif i == "y" or i == "Y":
            Ycount += 1
            
    if Pcount == Ycount:
        answer = True
    else: 
        answer = False

    return answer
```

---

​												

```python
def numPY(s):
    return s.lower().count('p') == s.lower().count('y')
```

---



```python

```

