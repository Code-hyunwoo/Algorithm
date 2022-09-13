# :boom: 비밀지도



```python
def solution(n, arr1, arr2):
    map1 = []
    map2 = []
    answer = []

    code = ''

    for i in arr1:
        map1.append(bin(i)[2:])

        if len(map1[-1]) < n:
            map1[-1] = '0' * (n-len(map1[-1])) + map1[-1]

    for j in arr2:
        map2.append(bin(j)[2:])

        if len(map2[-1]) < n:
            map2[-1] = '0' * (n - len(map2[-1])) + map2[-1]

    for i in range(n):
        for j in range(n):
            if int(map1[i][j]) == 0 and int(map2[i][j]) == 0:
                code += ' '
            else:
                code += '#'

            if len(code) == n:
                answer.append(code)
                code = ''

    return answer

```







**N진수 - > 10 진수**

**int('101', 2) = 20**

**int('202', 3) = 51**





**10진수 - > 2, 8, 16 진수**

**bin(11)**

**oct(11)**

**hex(11)**



```python
answer = []
n = 5
arr1 = [9, 20, 28, 18, 11]
arr2 = [30, 1, 21, 17, 28]

for i, j in zip(arr1, arr2):
    a12 = str(bin(i | j)[2:])
    a12 = a12.rjust(n, '0')
    a12 = a12.replace('1', '#')
    a12 = a12.replace('0', ' ')
    answer.append(a12)

print(answer)
```

```
def solution(n, arr1, arr2):
    answer = []
    for i,j in zip(arr1,arr2):
        a12 = str(bin(i|j)[2:])
        a12=a12.rjust(n,'0')
        a12=a12.replace('1','#')
        a12=a12.replace('0',' ')
        answer.append(a12)
    return answer
```

