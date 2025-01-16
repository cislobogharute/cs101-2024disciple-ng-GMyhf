岛屿周长

```
n,m=map(int,input().split())
k=0
sl=[]
for _ in range(n):
    sl.append(list(map(int,input().split())))
for i in range(n):
    for j in range(m):
        if sl[i][j]==1:
            k+=4
            if i<n-1 and sl[i+1][j]==1:
                k-=2
            if j<m-1 and sl[i][j+1]==1:
                k-=2
print(k)
```



螺旋矩阵



```
n = int(input())
s = [[401] * (n + 2)]
mx = s + [[401] + [0] * n + [401] for _ in range(n)] + s

dirL = [[0, 1], [1, 0], [0, -1], [-1, 0]]

row = 1
col = 1
N = 0
drow, dcol = dirL[0]

for j in range(1, n * n + 1):
    mx[row][col] = j
    if mx[row + drow][col + dcol]:
        N += 1
        drow, dcol = dirL[N % 4]

    row += drow
    col += dcol

for i in range(1, n + 1):
    print(' '.join(map(str, mx[i][1:-1])))
```

垃圾炸弹

```
d = int(input())
n = int(input())
c = {}
for i in range(n):
    x, y, z = map(int,input().split())
    for p in range(max(0, x - d), min(1024, x + d) + 1):
        for q in range(max(0, y - d), min(1024, y + d) + 1):
            c[(p, q)] = c.setdefault((p, q), 0) + z
a = list(c.values())
s = max(a)
print(a.count(s), s)
```



摆动数列

```
def sgn(x):
    if x == 0:
        return 0
    elif x > 0:
        return 1
    elif x < 0:
        return -1


n = int(input())
nums = list(map(int,input().split()))
delta = [sgn(nums[i+1]-nums[i]) for i in range(n-1)]

result = 1
pre = 0
for i in range(n-1):
    if delta[i] * pre < 0 or (pre == 0 and delta[i] != 0):
        result += 1
        pre = delta[i]
print(result)
```



boredom

```
n = int(input())
arr = list(map(int,input().split()))
dp = [0]*(max(arr) + 1)
cnt = [0]*(max(arr) + 1)
for each in arr:
    cnt[each] += 1

dp[0] = 0
dp[1] = cnt[1]
for i in range( 2, max(arr)+1 ):
    dp[i] = max( dp[i-1], dp[i-2] + cnt[i]*i )

print(max(dp))
```



田忌赛马

```
while True:
    n = int(input())
    if n == 0:
        break
    a = sorted([int(x) for x in input().split()], reverse=True)
    b = sorted([int(x) for x in input().split()], reverse=True)
    c = [[0]*(n+1) for _ in range(n+1)]
    for i in range(1, n+1):
        for j in range(1, n+1):
            if a[i-1] > b[j-1]:
                c[i][j] = max(c[i-1][j], c[i][j-1], c[i-1][j-1]+2)
            elif a[i-1] == b[j-1]:
                c[i][j] = max(c[i-1][j], c[i][j-1], c[i-1][j-1]+1)
            else:
                c[i][j] = max(c[i-1][j], c[i][j-1], c[i-1][j-1])
    print((c[n][n]-n)*200)
```