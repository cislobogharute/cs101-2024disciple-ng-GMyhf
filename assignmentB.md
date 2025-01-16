土豪

```
allmoney=list(map(int,input().split(',')))
dp1=[0]*len(allmoney)
dp2=[0]*len(allmoney)
dp1[0]=allmoney[0]
dp2[0]=allmoney[0]

for i in range(1,len(allmoney)):
    dp1[i] = max(dp1[i - 1] + allmoney[i], allmoney[i])
    dp2[i] = max(dp1[i - 1], dp2[i - 1] + allmoney[i], allmoney[i])
print(max(dp2))
```



股民老张

```
an=map(int,input().split())
minvalue=float('inf')
maxvalue=0
for i in an:
    minvalue=min(i,minvalue)
    maxvalue=max(maxvalue, i-minvalue)

print(maxvalue)
```



双十一

```
result = float("inf")
n, m = map(int, input().split())
store_prices = [input().split() for _ in range(n)]
you= [input().split() for _ in range(m)]
la=[0]*m
def dfs(i,sum1):
    global result
    if i==n:
        jian=0
        for i2 in range(m):
            store_j=0
            for k in you[i2]:
                a,b=map(int,k.split('-'))
                if la[i2]>=a:
                    store_j=max(store_j,b)
            jian+=store_j
        result=min(result,sum1-(sum1//300)*50-jian)
        return
    for i1 in store_prices[i]:
        idx,p=map(int,i1.split(':'))
        la[idx-1]+=p
        dfs(i+1,sum1+p)
        la[idx-1]-=p
dfs(0,0)
print(result)
```



孤岛

```
from collections import deque

def dfs(x, y, grid, n, queue, directions):
    """ Mark the connected component starting from (x, y) as visited using DFS. """
    grid[x][y] = 2  # Mark as visited
    queue.append((x, y))
    for dx, dy in directions:
        nx, ny = x + dx, y + dy
        if 0 <= nx < n and 0 <= ny < n and grid[nx][ny] == 1:
            dfs(nx, ny, grid, n, queue, directions)

def bfs(grid, n, queue, directions):
    """ Perform BFS to find the shortest path to another component. """
    distance = 0
    while queue:
        for _ in range(len(queue)):
            x, y = queue.popleft()
            for dx, dy in directions:
                nx, ny = x + dx, y + dy
                if 0 <= nx < n and 0 <= ny < n:
                    if grid[nx][ny] == 1:
                        return distance
                    elif grid[nx][ny] == 0:
                        grid[nx][ny] = 2  # Mark as visited
                        queue.append((nx, ny))
        distance += 1
    return distance

def main():
    n = int(input())
    grid = [list(map(int, input())) for _ in range(n)]
    directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]
    queue = deque()

    # Start DFS from the first '1' found and use BFS from there
    for i in range(n):
        for j in range(n):
            if grid[i][j] == 1:
                dfs(i, j, grid, n, queue, directions)
                return bfs(grid, n, queue, directions)

if __name__ == "__main__":
    print(main())
```



炸鸡排

```
n, k = map(int, input().split())
t = list(map(int, input().split()))
t.sort()
s = sum(t)
while True:
    if t[-1] > s / k:
        s -= t.pop()
        k -= 1
    else:
        print(f'{s / k:.3f}')
        break
```



国王游戏

```
n=int(input())
a0,b0=map(int,input().split())
numbers=[]
for _ in range(n):
    a,b=map(int,input().split())
    numbers.append((a,b))
numbers.sort(key=lambda x:(x[0]*x[1]))
result=0
for i in range(n):
    result=max(result,a0//numbers[i][1])
    a0*=numbers[i][0]
print(result)
```