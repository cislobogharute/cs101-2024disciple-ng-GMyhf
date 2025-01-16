闰年

```
x = int(input())
if x % 4 == 0:
    if x%100==0 and x%400!=0:
        print("N")
    elif x%3200==0:
        print("N")
    else:
        print("Y")
elif x%4!=0:
    print("N")
else:
    print("Y")
```

鸡兔同笼

```
a=int(input())
if a%4==0:
    print(int(a/4),int(a/2))
elif a%2==0:
    print(int((a+2)/4),int(a/2))
else:
    print(0,0)
```

domino

```
m,n=[int(x) for x in input().split()]
print(int(m*n/2))
```

theatre

```
import math
n, m, a = [int(x) for x in input().split()]
l = math.ceil(n/a)
w = math.ceil(m/a)
print(l*w)
```

petya



```
m = input().lower()
n = input().lower()
if m == n:
    print(0)
elif m > n :
    print(1)
else:
    print(-1)
```



team

```
l=[]
for i in range(0, int(input())):
    j = input().split()
    m=0

    if j.count('1') >= 2:
        m+=1
        l.append(m)
print(sum(l))
```