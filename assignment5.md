军备竞赛

```
p = int(input())
n = [int(x) for x in input().split()]
n.sort()

cnt = 0
left = 0
right = len(n) - 1

while left <= right:
    if n[left] <= p:
        cnt += 1
        p -= n[left]
        left += 1
    else:
        if right == left:
            break

        p += n[right]
        cnt -= 1
        if cnt < 0:
            cnt = 0
            break

        right -= 1

print(cnt)
```



生理周期

```
counter = 0
while True:
        p, e, i, d = map(int, input().split())
        if [p, e, i, d] == [-1, -1, -1, -1]:
          break
        counter +=1
        p %= 23
        e %= 28
        i %= 33
        origin = d
        d += 1
        while d % 23 != p or d % 28 != e or d % 33 != i:
            d += 1
        print(f'Case {counter}: the next triple peak occurs in {d-origin} days.')
```



排队实验

```
n = int(input())
*L, = map(int,input().split())
od = sorted(range(1, n+1), key = lambda x: L[x - 1])
L.sort()
t = sum((n-i-1) * L[i] for i in range(n)) / n

print(*od)
print('{:.2f}'.format(t))
```



砍树

```
n = int(input())
s = [[int(x) for x in input().split()] for i in range(n)]
count = 2
if n == 1:
    print(1)
else:
    for i in range(1, n - 1):
        if s[i][0] - s[i - 1][0] > s[i][1]:
            count += 1
        elif s[i + 1][0] - s[i][0] > s[i][1]:
            count += 1
            s[i][0] += s[i][1]

    print(count)
```



玛雅

```
Haab = {"pop": 0, "no": 1, "zip": 2, "zotz": 3, "tzec": 4, "xul": 5, "yoxkin": 6, "mol": 7, "chen": 8, "yax": 9, "zac": 10, "ceh": 11, "mac": 12, "kankin": 13, "muan": 14, "pax": 15, "koyab": 16, "cumhu": 17, "uayet": 18}
Tzolkin = {0: "imix", 1: "ik", 2: "akbal", 3: "kan", 4: "chicchan", 5: "cimi", 6: "manik", 7: "lamat", 8: "muluk", 9: "ok", 10: "chuen", 11: "eb", 12: "ben", 13: "ix", 14: "mem", 15: "cib", 16: "caban", 17: "eznab", 18: "canac", 19: "ahau"}
n = int(input())
print(n)
for _ in range(n):
    day, month, year = input().split()
    day = int(day.rstrip("."))
    total = int(year) * 365 + Haab[month] * 20 + day
    print(total % 13 + 1, Tzolkin[total % 20], total // 260)
```



雷达

```
import math

def solve(n, d, islands):
    if d < 0:
        return -1

    ranges = []
    for x, y in islands:
        if y > d:
            return -1
        delta = math.sqrt(d * d - y * y)
        ranges.append((x - delta, x + delta))

    if not ranges:
        return -1

    ranges.sort(key=lambda x:x[1])

    number = 1
    r = ranges[0][1]
    for start, end in ranges[1:]:
        if r < start:
            r = end
            number += 1

    return number

case_number = 0
while True:
    n, d = map(int, input().split())
    if n == 0 and d == 0:
        break

    case_number += 1
    islands = []
    for _ in range(n):
        islands.append(tuple(map(int, input().split())))

    result = solve(n, d, islands)
    print(f"Case {case_number}: {result}")
    input()
```