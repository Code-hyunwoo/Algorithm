# Level 1

---

​																									




```python
def solution(s):
    answer = ''
    
    word = s.split(" ")
    for i in word:
        for j in range(len(i)):
            if j % 2 == 0:
                answer += i[j].upper()
            else:
                answer += i[j].lower()
        answer += " "
    
    return answer[0:-1]
```

---

​												

```python


```

---



```python

```

