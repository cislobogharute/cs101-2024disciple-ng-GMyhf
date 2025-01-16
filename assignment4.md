Sale

```
m,n=map(int,input().split())
a=list(map(int,input().split()))
a.sort(reverse=False)
money=0
for i in range(n):
    if a[i]>0:
        break
    money+=a[i]

print(-money)
```



Twin

```
n = int(input())
a = list(map(int, input().split()))
a.sort(reverse=True)
b = 0
c = sum(a)
k = 0
for i in a:
    b += i
    k += 1
    if b > c/2:
        break
print(k)
```



Taxi

```
input()
a,b,c,d=map(input().count,("1","2","3","4"))
print(d+c+(b*2+max(0,a-c)+3)//4)
```