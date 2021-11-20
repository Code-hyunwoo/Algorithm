# :boom: 다트게임



```python
def solution(dartResult):
    answer = []

    for i in range(len(dartResult)):
        if dartResult[i].isdigit():
            if dartResult[i] == '1':
                if dartResult[i+1] == '0':				
                    answer.append(int(10))
                else:
                    answer.append(int(1))
            elif dartResult[i] == '0':
                if dartResult[i-1] == '1':
                    continue
                else:
                    answer.append(int(0))
            else:
                answer.append(int(dartResult[i]))
        else:
            if dartResult[i] == 'S':
                answer[-1] = answer[-1] ** 1
            elif dartResult[i] == 'D':
                answer[-1] = answer[-1] ** 2
            elif dartResult[i] == 'T':
                answer[-1] = answer[-1] ** 3
            elif dartResult[i] == '#':
                answer[-1] = answer[-1] * (-1)
            else: # 아차상 *이라면
                if len(answer) == 1:
                    answer[0] = answer[0] * 2
                elif len(answer) == 2:
                    answer[0] = answer[0] * 2
                    answer[1] = answer[1] * 2
                else:
                    answer[1] = answer[1] * 2
                    answer[2] = answer[2] * 2

    // answer = answer[0] + answer[1] + answer[2]

    return sum(answer)
```



​																		
