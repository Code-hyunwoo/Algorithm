# Level 1

---

​																									




```python
def solution(s):
    answer = ""
    
    number= {"zero": "0", "one":"1", "two":"2","three":"3","four":"4","five":"5","six":"6",
             "seven":"7","eight":"8", "nine":"9"}
    
    check = ""
    for i in s:
        if i.isdigit():
            answer += i
        elif i.isalpha():
            check += i
            if check in number.keys():
                answer += number[check]
                check = ""
        
    return int(answer)
```

---

​												

```python
num_dic = {"zero":"0", "one":"1", "two":"2", "three":"3", "four":"4", "five":"5", "six":"6", "seven":"7", "eight":"8", "nine":"9"}

def solution(s):
    answer = s
    for key, value in num_dic.items():
        answer = answer.replace(key, value)
    return int(answer)
```

---



```python

```

