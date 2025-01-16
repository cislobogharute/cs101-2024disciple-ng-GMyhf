全排列

```
def dfs(idx, n, used, temp, result):
    if idx == n + 1:
        result.append(temp[:])
        return

    for i in range(1, n + 1):
        if not used[i]:
            temp.append(i)
            used[i] = True
            dfs(idx + 1, n, used, temp, result)
            used[i] = False
            temp.pop()


def generate_permutations(n):
    result = []
    used = [False] * (n + 1)
    dfs(1, n, used, [], result)

    for perm in result:
        print(" ".join(map(str, perm)))
n = int(input())
generate_permutations(n)
```



汉诺塔

```
def moveHanoi(n, from_rod, to_rod, mid_rod):
    if n == 0:
        return
    moveHanoi(n - 1, from_rod, mid_rod, to_rod)
    print(f"{from_rod}->{to_rod}")
    moveHanoi(n - 1, mid_rod, to_rod, from_rod)

n = int(input())
print(2**n-1)
moveHanoi(n, 'A', 'C', 'B')
```



八皇后

```
list1 = []

def queen(s):
    if len(s) == 8:
        list1.append(s)
        return
    for i in range(1, 9):
        if all(str(i) != s[j] and abs(len(s) - j) != abs(i - int(s[j])) for j in range(len(s))):
            queen(s + str(i))

queen('')
samples = int(input())
for k in range(samples):
    print(list1[int(input()) - 1])
```



cut ribbons

```
n,a,b,c=map(int,input().split())
max_segments=0
if a==1 or b==1 or c==1:
    print(n)
else:
    for i in range(n // a + 1):
        remaining = n - i * a
        for j in range(remaining // b + 1):
            new_remaining = remaining - j * b
            if new_remaining % c == 0:
                segments = i + j + new_remaining // c
                max_segments = max(max_segments, segments)

    print(max_segments)
```



小偷

```
n,b=map(int, input().split())
price=[0]+[int(i) for i in input().split()]
weight=[0]+[int(i) for i in input().split()]
bag=[[0]*(b+1) for _ in range(n+1)]
for i in range(1,n+1):
    for j in range(1,b+1):
        if weight[i]<=j:
            bag[i][j]=max(price[i]+bag[i-1][j-weight[i]], bag[i-1][j])
        else:
            bag[i][j]=bag[i-1][j]
print(bag[-1][-1])
```



拦截导弹

```
def max_intercepted_missiles(k, heights):
    dp = [1] * k

    # Fill the dp array
    for i in range(1, k):
        for j in range(i):
            if heights[i] <= heights[j]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)


if __name__ == "__main__":

    k = int(input())
    heights = list(map(int, input().split()))

    result = max_intercepted_missiles(k, heights)
    print(result)
```