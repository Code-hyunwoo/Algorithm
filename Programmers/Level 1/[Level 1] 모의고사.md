# Level 1

---

​																									




```python
def solution(answers):
    answer = []
    
    supo1 = [1,2,3,4,5]
    supo2 = [2,1,2,3,2,4,2,5]
    supo3 = [3,3,1,1,2,2,4,4,5,5]
    check1 = 0
    check2 = 0
    check3 = 0
    
    for i in range(len(answers)):
        if answers[i] == supo1[i%5]:
            check1 += 1
        if answers[i] == supo2[i%8]:
            check2 += 1
        if answers[i] == supo3[i%10]:
            check3 += 1
    
    answertop = max(check1, check2, check3)

    if answertop == check1:
        answer.append(1)
    if answertop == check2:
        answer.append(2)
    if answertop == check3:
        answer.append(3)
    
    return answer
```

---

​												

```python
def solution(answers):
    pattern1 = [1,2,3,4,5]
    pattern2 = [2,1,2,3,2,4,2,5]
    pattern3 = [3,3,1,1,2,2,4,4,5,5]
    score = [0, 0, 0]
    result = []

    for idx, answer in enumerate(answers):
        if answer == pattern1[idx%len(pattern1)]:
            score[0] += 1
        if answer == pattern2[idx%len(pattern2)]:
            score[1] += 1
        if answer == pattern3[idx%len(pattern3)]:
            score[2] += 1

    for idx, s in enumerate(score):
        if s == max(score):
            result.append(idx+1)

    return result
```

---



```python

```

