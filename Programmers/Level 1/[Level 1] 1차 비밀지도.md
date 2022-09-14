# Level 1

---

​																									




```python
def solution(n, arr1, arr2):
    answer = []
    new1 = []
    new2 = []
    for i in range(n):
        new1.append(bin(arr1[i])[2:])
        new2.append(bin(arr2[i])[2:])
    
    for j in range(n):
        
        if len(new1[j]) != n:
            new1[j] = "0"*(n-len(new1[j])) + new1[j]
        if len(new2[j]) != n:
            new2[j] = "0"*(n-len(new2[j])) + new2[j]        
        check = ""
        for k in range(n):
            if new1[j][k] == "0" and new2[j][k] =="0":
                check += " "
            else:
                check += "#"
        answer.append(check)
        
    return answer
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
val = "77".rjust(5, "0")
print(val)

val = "77777".rjust(5, "0")
print(val)

val = "123".rjust(5, "a")
print(val)

val = "123".rjust(3, "a")
print(val)

00077
77777
aa123
123

val = "222".ljust(3, "0")
print(val)

val = "222".ljust(15, "a")
print(val)

222
222aaaaaaaaaaaa

zfill
이는 0을 왼쪽에 채워주는 역할을 한다.
val = "2".zfill(3)
print(val)

val = "50000".zfill(5)
print(val)

val = "123".zfill(5)
print(val)

002
50000
00123
```

