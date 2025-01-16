收到祝福的平方数

```
def is_blessed_id(A):

    squares = set()
    i = 1
    while i * i <= 10 ** 9:
        squares.add(i * i)
        i += 1

    digits = list(map(int, str(A)))

    def dfs(idx):
        if idx == len(digits):
            return True

        num = 0
        for i in range(idx, len(digits)):
            num = num * 10 + digits[i]
            if num in squares:
                if dfs(i + 1):
                    return True
        return False

    return "Yes" if dfs(0) else "No"

A = int(input())

print(is_blessed_id(A))
```



不同路径

```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1]*n] + [[1]+[0] * (n-1) for _ in range(m-1)]
        #print(dp)
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[-1][-1]
```



矩阵最大权值路径

```
def dfs(x, y, now_value):
    global max_value, opt_path
    if x == n - 1 and y == m - 1:
        if now_value > max_value:
            max_value = now_value
            opt_path = temp_path[:]
        return

    visited[x][y] = True

    for dx, dy in directions:
        next_x, next_y = x + dx, y + dy
        if 0 <= next_x < n and 0 <= next_y < m and not visited[next_x][next_y]:
            next_value = now_value + maze[next_x][next_y]
            temp_path.append((next_x, next_y))
            dfs(next_x, next_y, next_value)
            temp_path.pop()

    visited[x][y] = False


n, m = map(int, input().split())
maze = [list(map(int, input().split())) for _ in range(n)]

max_value = float('-inf')
opt_path = []
temp_path = [(0, 0)]
visited = [[False] * m for _ in range(n)]
directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

dfs(0, 0, maze[0][0])

for x, y in opt_path:
    print(x + 1, y + 1)
```

寻宝

```
import heapq


def bfs(x, y):
    d = [[-1, 0], [1, 0], [0, 1], [0, -1]]
    queue = []
    heapq.heappush(queue, [0, x, y])
    check = set()
    check.add((x, y))
    while queue:
        step, x, y = map(int, heapq.heappop(queue))
        if martix[x][y] == 1:
            return step
        for i in range(4):
            dx, dy = x + d[i][0], y + d[i][1]
            if martix[dx][dy] != 2 and (dx, dy) not in check:
                heapq.heappush(queue, [step + 1, dx, dy])
                check.add((dx, dy))
    return "NO"


m, n = map(int, input().split())
martix = [[2] * (n + 2)] + [[2] + list(map(int, input().split())) + [2] for i in range(m)] + [[2] * (n + 2)]
print(bfs(1, 1))
```

马走日

```
maxn = 10;
sx = [-2, -1, 1, 2, 2, 1, -1, -2]
sy = [1, 2, 2, 1, -1, -2, -2, -1]

ans = 0;


def Dfs(dep: int, x: int, y: int):

    if n * m == dep:
        global ans
        ans += 1
        return


    for r in range(8):
        s = x + sx[r]
        t = y + sy[r]
        if chess[s][t] == False and 0 <= s < n and 0 <= t < m:
            chess[s][t] = True
            Dfs(dep + 1, s, t)
            chess[s][t] = False;


for _ in range(int(input())):
    n, m, x, y = map(int, input().split())
    chess = [[False] * maxn for _ in range(maxn)]
    ans = 0
    chess[x][y] = True
    Dfs(1, x, y)
    print(ans)
```

连通区域

```
def dfs(matrix, row, col, visited):
    if row < 0 or row >= len(matrix) or col < 0 or col >= len(matrix[0]) \
            or matrix[row][col] != 'W' or visited[row][col]:
        return 0

    visited[row][col] = True
    size = 1

    for dr in [-1, 0, 1]:
        for dc in [-1, 0, 1]:
            size += dfs(matrix, row + dr, col + dc, visited)

    return size


def max_connected_area(matrix):
    max_area = 0
    visited = [[False for _ in range(len(matrix[0]))] for _ in range(len(matrix))]

    for row in range(len(matrix)):
        for col in range(len(matrix[0])):
            if matrix[row][col] == 'W' and not visited[row][col]:
                area = dfs(matrix, row, col, visited)
                max_area = max(max_area, area)

    return max_area


def main():
    T = int(input())
    for _ in range(T):
        N, M = map(int, input().split())
        matrix = [input().strip() for _ in range(N)]
        print(max_connected_area(matrix))


if __name__ == "__main__":
    main()
```