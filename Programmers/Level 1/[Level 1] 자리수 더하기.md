# Level 1

---

​																									


```python
def solution(n):
    answer = 0

    while n > 0:

        answer += n % 10
        n = n // 10
                
    return answer
```

---

​												

```python
def sum_digit(number):
    if number < 10:
        return number;
    return (number % 10) + sum_digit(number // 10) 
```

---



```python
def sum_digit(number):
    return sum([int(i) for i in str(number)])
```

