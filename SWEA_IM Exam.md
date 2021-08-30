# :boom:LED

---



```python

T = int(input())
for tc in range(1, T+1):
    N = int(input())
    led = list(map(int, input().split()))
    start = [0]*(N)
    min_push = 100
    push = 0
    for i in range(N):
        if led[i] == start[i]:
            continue
        else:
            push += 1
            for j in range(N):
                if (j+1) % (i+1) == 0:
                    if start[j] == 0:
                        start[j] = 1
                    else:
                        start[j] = 0
        if led == start:
            if min_push > push:
                min_push = push

    print('#{} {}'.format(tc, min_push))
```





5               
5      
1 1 0 0 1
6                  
0 1 1 1 0 0
7
1 1 1 1 1 1 1
10
0 1 0 1 0 1 0 1 0 1
20
0 0 0 0 1 0 0 1 0 1 0 1 0 1 0 1 1 1 0 0