flowers

```
def count_ways(t, k, test_cases):
    MOD = 1000000007
    max_b = max(b for _, b in test_cases)

    dp = [0] * (max_b + 1)
    dp[0] = 1

    for i in range(1, max_b + 1):
        if i < k:
            dp[i] = 1
        else:
            dp[i] = (dp[i - 1] + dp[i - k]) % MOD

    prefix_sum = [0] * (max_b + 1)
    for i in range(1, max_b + 1):
        prefix_sum[i] = (prefix_sum[i - 1] + dp[i]) % MOD

    results = []
    for a, b in test_cases:
        result = (prefix_sum[b] - prefix_sum[a - 1]) % MOD
        results.append(result)

    return results


import sys

input = sys.stdin.read
data = input().split()

t = int(data[0])
k = int(data[1])
test_cases = []

index = 2
for _ in range(t):
    a = int(data[index])
    b = int(data[index + 1])
    test_cases.append((a, b))
    index += 2

results = count_ways(t, k, test_cases)
for result in results:
    print(result)
```



水淹七军

```
import sys

sys.setrecursionlimit(300000)
input = sys.stdin.read


def is_valid(x, y, m, n):
    return 0 <= x < m and 0 <= y < n


def dfs(x, y, water_height_value, m, n, h, water_height):
    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]

    for i in range(4):
        nx, ny = x + dx[i], y + dy[i]
        if is_valid(nx, ny, m, n) and h[nx][ny] < water_height_value:
            if water_height[nx][ny] < water_height_value:
                water_height[x][y] = water_height_value
                dfs(nx, ny, water_height_value, m, n, h, water_height)


def main():
    data = input().split()
    idx = 0
    k = int(data[idx])
    idx += 1
    results = []

    for _ in range(k):
        m, n = map(int, data[idx:idx + 2])
        idx += 2
        h = []
        for i in range(m):
            h.append(list(map(int, data[idx:idx + n])))
            idx += n
        water_height = [[0] * n for _ in range(m)]

        i, j = map(int, data[idx:idx + 2])
        idx += 2
        i, j = i - 1, j - 1

        p = int(data[idx])
        idx += 1

        for _ in range(p):
            x, y = map(int, data[idx:idx + 2])
            idx += 2
            x, y = x - 1, y - 1
            if h[x][y] <= h[i][j]:
                continue

            dfs(x, y, h[x][y], m, n, h, water_height)

        results.append("Yes" if water_height[i][j] > 0 else "No")

    sys.stdout.write("\n".join(results) + "\n")


if __name__ == "__main__":
    main()
```



数楼梯

```
fib=[]
import sys
n=int(input())
if n==0:
    print(0)
    sys.exit()
for i in range(n+1):
    if i ==0 or i==1:
        fib.append(1)
    else:
        fib.append(fib[i-2]+fib[i-1])
print(fib[n])
```



跳台阶

```
N=int(input())
print(2**(N-1))
```



小游戏

```
import sys

sys.setrecursionlimit(1000000)
d = [(0, -1), (0, 1), (-1, 0), (1, 0)]
H, L, ha, la, hb, lb, MIN = 0, 0, 0, 0, 0, 0, 0
b = 0


def dfs(h, l, dire, step):
    global H, L, hb, lb, MIN, b
    if h == hb and l == lb:
        if step < MIN:
            MIN = step
        return
    if step >= MIN:
        return
    for i in d:
        hh, ll = h + i[0], l + i[1]
        if hh >= 0 and hh <= H + 1 and ll >= 0 and ll <= L + 1 and b[hh][ll] == ' ':
            b[hh][ll] = 'X'
            if dire != i:
                dfs(hh, ll, i, step + 1)
            else:
                dfs(hh, ll, i, step)
            b[hh][ll] = ' '


k1 = 0
while True:
    k1 += 1
    L, H = map(int, input().split())
    if L == 0:
        break
    print("Board #{}:".format(k1))
    b = [[' '] * (L + 2)]
    for _ in range(H):
        b.append([' '] + list(input()) + [' '])
    b.append([' '] * (L + 2))
    k2 = 0
    while True:
        k2 += 1
        la, ha, lb, hb = map(int, input().split())
        MIN = float('inf')
        if la == 0:
            break
        b[hb][lb] = ' '
        dfs(ha, la, (0, 0), 0)
        b[hb][lb] = 'X'
        if MIN == float('inf'):
            print("Pair {}: impossible.".format(k2))
        else:
            print("Pair {}: {} segments.".format(k2, MIN))
    print()
```



最长回文

```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        lens = len(s)
        if s == s[::-1] or len(s) == 1:
            return s

        for i in range(1, lens - 1):

            for j in range(i + 1):

                substr = s[j:lens - i + j]
                if substr == substr[::-1]:
                    return substr
        return s[0]
```