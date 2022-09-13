# Level 1

---

​																									




```python
def solution(arr, divisor):
    answer = []
    
    for i in arr:
        if i % divisor == 0:
            answer.append(i)
    
    if answer == []:
        return [-1]
    else:
        return sorted(answer)
```

---

​												

```python
def solution(arr, divisor): return sorted([n for n in arr if n%divisor == 0]) or [-1]
```

---



```python
def solution(arr, divisor):
    arr = [x for x in arr if x % divisor == 0];
    arr.sort();
    return arr if len(arr) != 0 else [-1];
```

