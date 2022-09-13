# Level 1

---

​																									




```python
def solution(arr):
    
    arr.remove(min(arr))
    
    if arr == []:
        return [-1]
    else:    
        return arr
```

---

​												

```python
def rm_small(mylist):
    return [i for i in mylist if i > min(mylist)]
```

---



```python

```

