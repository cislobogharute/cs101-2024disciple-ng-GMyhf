看病

```
def sort_patients(patient_list):
    elderly = [(id, age) for id, age in patient_list if age >= 60]
    non_elderly = [(id, age) for id, age in patient_list if age < 60]
    elderly.sort(key=lambda x: (-x[1], patient_list.index(x)))

    sorted_patients = elderly + non_elderly

    sorted_ids = [id for id, age in sorted_patients]
    return sorted_ids

def main():

    num_patients = int(input())
    patient_list = []
    for _ in range(num_patients):
        id, age = input().strip().split()
        age = int(age)
        patient_list.append((id, age))

    sorted_ids = sort_patients(patient_list)
    for id in sorted_ids:
        print(id)


if __name__ == "__main__":
    main()
```

矩阵

```
def parse_matrix(n, m, triples):
    matrix = {}
    for triple in triples:
        row, col, value = triple
        matrix[(row, col)] = value
    return matrix


def sparse_matrix_multiply(X, Y):
    n = len(X)
    result = {}

    for (x_row, x_col), x_value in X.items():
        for (y_row, y_col), y_value in Y.items():
            if x_col == y_row:  # Only multiply if the column of X matches the row of Y
                result_row, result_col = x_row, y_col
                if (result_row, result_col) in result:
                    result[(result_row, result_col)] += x_value * y_value
                else:
                    result[(result_row, result_col)] = x_value * y_value

    return result


def print_triples(triples):
    for triple in sorted(triples.items()):
        print(triple[0][0], triple[0][1], triple[1])


n, m1, m2 = map(int, input().split())
X_triples = [tuple(map(int, input().split())) for _ in range(m1)]
Y_triples = [tuple(map(int, input().split())) for _ in range(m2)]

X = parse_matrix(n, m1, X_triples)
Y = parse_matrix(n, m2, Y_triples)

result = sparse_matrix_multiply(X, Y)

print_triples(result)
```



打怪兽

```
from collections import defaultdict

cases = int(input())

for _ in range(cases):
    situation = "alive"
    n, m, b = map(int, input().split())
    a = defaultdict(list)

    for _ in range(n):
        x, y = map(int, input().split())
        a[x].append(y)

    # Process coordinates
    for x in sorted(a):
        if m >= len(a[x]):
            b -= sum(a[x])
        else:
            a[x].sort(reverse=True)
            b -= sum(a[x][:m])
        if b <= 0:
            situation = x
            break

    print(situation)
```



零钱

```
from math import inf
n,m=map(int,input().split())
zhonglei=list(map(int,input().split()))
dp=[0]+[inf for _ in range(m)]
for i in range(n):
    for j in range(zhonglei[i],m+1):
        dp[j]=min(dp[j],dp[j-zhonglei[i]]+1)
print(dp[m] if dp[m] != inf else-1)
```



翻译

```
tokens = [str(i) for i in input().split()]
dic = {"zero": 0, "one": 1, "two": 2, "three": 3, "four": 4, "five": 5, "six": 6,
       "seven": 7, "eight": 8, "nine": 9, "ten": 10, "eleven": 11, "twelve": 12,
       "thirteen": 13, "fourteen": 14, "fifteen": 15, "sixteen": 16, "seventeen": 17,
       "eighteen": 18, "nineteen": 19, "twenty": 20, "thirty": 30, "forty": 40,
       "fifty": 50, "sixty": 60, "seventy": 70, "eighty": 80, "ninety": 90,
       "hundred": 100, "thousand": 1000, "million": 1000000}

sign = 1
if tokens[0] == "negative":
    sign = -1
    del tokens[0]

total = 0
tmp = 0
for i in tokens:
    if i in ("thousand", "million"):
        total += tmp * dic[i]
        tmp = 0
        continue
    if i == "hundred":
        tmp *= dic[i]
    else:
        tmp += dic[i]

print(sign * (total + tmp))
```



寒假

```
n = int(input())
a = []
for i in range(n):
    x, y = map(int, input().split())
    a.append((x + 1, y + 1))
a = sorted(a, key = lambda _: _[0])
dp = [0] * 65
for i in range(n):
    for j in range(a[i][1], 62):
        dp[j] = max(dp[j], dp[a[i][0] - 1] + 1)
print(dp[61])
```