# Level 1

---

​																									




```python
def solution(phone_number):
    answer = ''
    
    for i in range(len(phone_number)):
        if i < len(phone_number)-4:
            answer += "*"
        else:
            answer += phone_number[i]
        
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

