Beautiful matrix

```
for i in range(5):
    arr = [int(x) for x in input().split()]
    for j in range(5):
        if arr[j] == 1:
            print(abs(2 - i) + abs(2 - j))
            exit()
```



Police recruit

```
n=int(input())
a=list(map(int,input().split()))
cnt=0
police=0
for i in a:
    if i==-1 and police==0:
        cnt+=1
        continue
    if i>0:
        police+=i
        continue
    police-=1

print(cnt)
```



Ride to school

```
import math

while True:
    n = int(input())
    if n == 0:
        break

    max_time = float("inf")
    for _ in range(n):
        speed, time = map(int, input().split())
        if time < 0:
            continue
        arrival_time = math.ceil((4500 / speed) * 3.6 + time)
        max_time = min(max_time, arrival_time)

    print(max_time)
```



水仙花

```
def shuixianhuashu(n):
    xulie=[int(d) for d in str(n)]
    lifanghe=sum(d**3 for d in xulie)
    return lifanghe==n
def xunzhaoguocheng(a,b):

    zuizhongshuixianhua=[]
    for i in range(a,b+1):
        if shuixianhuashu(i):
            zuizhongshuixianhua.append(i)

    return zuizhongshuixianhua

a, b = map(int, input().split())
zuizhongshuixianhua=xunzhaoguocheng(a,b)
if zuizhongshuixianhua:
    print(" ".join(map(str, zuizhongshuixianhua)))
else:
    print("NO")
```



校门外的树

```
L, m = map(int, input().split())

dp = [1]*(L+1)

for i in range(m):
    s, e = map(int, input().split())
    for j in range(s, e+1):
        dp[j] = 0

print(dp.count(1))
```



divisibility

```
t = int(input())
for _ in range(t):
    a, b = map(int, input().split())
    res = a % b
    if res == 0:
        print(0)
    else:
        print(b - res)
```