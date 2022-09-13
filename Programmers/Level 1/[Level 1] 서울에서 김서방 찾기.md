# Level 1

---

​																									




```python
def solution(seoul):
    
    index = seoul.index("Kim")
    answer = '김서방은 '+ str(index) +'에 있다'
    return answer
```

---

​												

```python
def findKim(seoul):
    return "김서방은 {}에 있다".format(seoul.index('Kim'))
```

---



```python
def findKim(seoul):
    kimIdx = 0
    # 함수를 완성하세요
    for i in range(len(seoul)):
        if seoul[i]=="Kim":
            return "김서방은 {}에 있다".format(i)
```

