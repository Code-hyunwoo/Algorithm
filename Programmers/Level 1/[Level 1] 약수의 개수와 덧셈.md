# Level 1

---

​																									




```python
def solution(left, right):
    answer = 0
    
    for i in range(left, right+1):
        count = 0
        for j in range(1, i+1):
            if i % j == 0:
                count += 1
        
        if count % 2 == 0:
            answer += i
        else:
            answer -= i
    return answer
```

---

​												

```python
def hide_numbers(s):
    return "*"*(len(s)-4) + s[-4:]
```

---



```python

```

