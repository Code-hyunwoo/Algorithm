# Level 1

---

​																									




```python
def solution(n):
    answer = []
    num = list(str(n))[::-1]
    
    for i in num:
        answer.append(int(i))

    return answer
```

---

​												

```python
def digit_reverse(n):
    return list(map(int, reversed(str(n))))
```

---



```python
def digit_reverse(n):
    return [int(i) for i in str(n)][::-1]
```

