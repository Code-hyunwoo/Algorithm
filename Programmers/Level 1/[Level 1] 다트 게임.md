# Level 1

---

​																									




```python
def solution(dartResult):
    answer = []
    dartResult = dartResult.replace("10", 'A')
    bonus = {'S': 1, 'D': 2, 'T': 3}
    
    for i in dartResult:
        if i.isdigit() or i=='A':
            answer.append(10 if i=='A' else int(i))
        elif i in ('S','D','T'):
            num = answer.pop()
            answer.append(num**bonus[i])
        elif i =='#':
            answer[-1] *= -1
        elif i =='*':
            num = answer.pop()
            if len(answer):
                answer[-1] *= 2
            answer.append(num*2)
        
    return sum(answer)
```

---

​												

```python

```

---



```python

```

