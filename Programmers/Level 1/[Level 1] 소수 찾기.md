# Level 1

---

​																									




```python
def solution(arr1, arr2):
    answer = []
    
    for i in range(len(arr1)):
        for j in range(len(arr1[0])):
            arr1[i][j] += arr2[i][j]
        
    return arr1
```

---

​												

```python
def sumMatrix(A,B):
    answer = [[c + d for c, d in zip(a, b)] for a, b in zip(A,B)]
    return answer
```

---



```python

```

