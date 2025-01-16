取石子（正确版）

```
def can_win(a, b):
    if a < b:
        return can_win(b,a)
    if a>=b*2:
        return True
    elif a==b:
        return True
    else:
        return not can_win(a-b,b)

a,b=map(int,input().split())
while a:
    if can_win(a,b):
        print('win')
    else:
        print('lose')
    a,b=map(int,input().split())
```

取石子（废案）

想投机取巧一下，被狠狠制裁了，提交上去显示WA，给了几十组的测试数据，甚至找不出是哪一组错了（捂脸

```
def can_win(a, b):
    if a < b:
        a, b = b, a

    while a > 0 and b > 0:
        if a == b:
            return "win"

        quotient = a // b

        if quotient >= 2:
            return "win"
        else:
            a = a - b
            a, b = b, a
            a = a - b
            a, b = b, a
            if a // b > 1:
                return "win"
            else:
                return "lose"


import sys

while True:
    try:
        a, b = map(int, sys.stdin.readline().split())
        if a == 0 and b == 0:
            break
        print(can_win(a, b))
    except ValueError:
        print("Invalid input. Please enter integers.")
```

potion

```
import heapq


def max_potions(n, potions):

    health = 0

    consumed = []

    for potion in potions:

        health += potion
        heapq.heappush(consumed, potion)
        if health < 0:
            if consumed:
                health -= consumed[0]
                heapq.heappop(consumed)


    return len(consumed)

n = int(input())
potions = list(map(int, input().split()))
print(max_potions(n, potions))
```

洋葱

```
n = int(input())
dui = [0] * ((n+1)//2+1)
for i in range(1, n+1):
    line = [0]+list(map(int, input().split()))
    for j in range(1, n+1):
        k = min(i, j, (n+1)-i, (n+1)-j)
        dui[k] += line[j]
print(max(dui))
```

快速堆猪

```
import heapq

class PigStack:
    def __init__(self):
        self.stack = []
        self.min_heap = []
        self.popped = set()

    def push(self, weight):
        self.stack.append(weight)
        heapq.heappush(self.min_heap, weight)

    def pop(self):
        if self.stack:
            weight = self.stack.pop()
            self.popped.add(weight)

    def min(self):
        while self.min_heap and self.min_heap[0] in self.popped:
            self.popped.remove(heapq.heappop(self.min_heap))
        if self.min_heap:
            return self.min_heap[0]
        else:
            return None

pig_stack = PigStack()

while True:
    try:
        command = input().split()
        if command[0] == 'push':
            pig_stack.push(int(command[1]))
        elif command[0] == 'pop':
            pig_stack.pop()
        elif command[0] == 'min':
            min_weight = pig_stack.min()
            if min_weight is not None:
                print(min_weight)
    except EOFError:
        break
```

走山路

```
import heapq
m, n, p = map(int, input().split())
martix = [list(input().split())for i in range(m)]
dir = [(-1, 0), (1, 0), (0, 1), (0, -1)]
for _ in range(p):
    sx, sy, ex, ey = map(int, input().split())
    if martix[sx][sy] == "#" or martix[ex][ey] == "#":
        print("NO")
        continue
    in_queue, heap, ans = set(), [], []
    heapq.heappush(heap, (0, sx, sy))
    in_queue.add((sx, sy, -1))
    while heap:
        tire, x, y = heapq.heappop(heap)
        if x == ex and y == ey:
            ans.append(tire)
        for i in range(4):
            dx, dy = dir[i]
            x1, y1 = dx+x, dy+y
            if 0 <= x1 < m and 0 <= y1 < n and martix[x1][y1] != "#" and (x1, y1, i) not in in_queue:
                t1 = tire+abs(int(martix[x][y])-int(martix[x1][y1]))
                heapq.heappush(heap, (t1, x1, y1))
                in_queue.add((x1, y1, i))
    print(min(ans) if ans else "NO")
```

变换的迷宫

```
from collections import deque

def bfs(x, y):
    visited = {(0, x, y)}
    dx = [0, 0, 1, -1]
    dy = [1, -1, 0, 0]
    queue = deque([(0, x, y)])
    while queue:
        time, x, y = queue.popleft()
        for i in range(4):
            nx, ny = x + dx[i], y + dy[i]
            temp = (time + 1) % k
            if 0 <= nx < r and 0 <= ny < c and (temp, nx, ny) not in visited:
                cur = maze[nx][ny]
                if cur == 'E':
                    return time + 1
                elif cur != '#' or temp == 0:
                    queue.append((time + 1, nx, ny))
                    visited.add((temp, nx, ny))
    return 'Oop!'


t = int(input())
for _ in range(t):
    r, c, k = map(int, input().split())
    maze = [list(input()) for _ in range(r)]
    for i in range(r):
        for j in range(c):
            if maze[i][j] == 'S':
                print(bfs(i, j))
```