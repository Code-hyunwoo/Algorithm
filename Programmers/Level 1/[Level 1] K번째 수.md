# Level 1

---

​																									




```python
def solution(array, commands):
    answer = []
    
    for i in range(len(commands)):
        a, b, c = commands[i][0],commands[i][1],commands[i][2]
        answer.append(sorted(array[a-1:b])[c-1])
    
    return answer
```

---

​												

```python
def solution(array, commands):
    return list(map(lambda x:sorted(array[x[0]-1:x[1]])[x[2]-1], commands))
```

---



```python
def solution(array, commands):
    answer = []
    for command in commands:
        i,j,k = command
        answer.append(list(sorted(array[i-1:j]))[k-1])
    return answer
```

