黑神话

```
def jiemi(k,s):
    jieguo=[]
    for char in s:
        if ord("a")<=ord(char)<=ord("z"):
            xiugaihou= chr((ord(char) - ord("a") - k) % 26 + ord("a"))
        elif ord("A")<=ord(char)<=ord("Z"):
            xiugaihou= chr((ord(char) - ord("A") - k) % 26 + ord("A"))
        else:
            xiugaihou=char
        jieguo.append(xiugaihou)
    return"". join(jieguo)
k=int(input())
s=input()
print(jiemi(k,s))
```



整数求和

```
s=input()
new_str = ""
for ch in s:
    if ch.isdigit():
       new_str += ch
    else:
       new_str += " "
sub_list = new_str.split()
num_list = list(map(int, sub_list))
res  =sum(num_list)
print(res)
```



身份证

```
l = [7, 9, 10, 5, 8, 4, 2, 1, 6, 3, 7, 9, 10, 5, 8, 4, 2]
n = int(input())

for _ in range(n):
    s = input()
    if len(s) != 18:
        print('NO')
        continue

    x = sum(int(s[i]) * l[i] for i in range(17)) % 11
    x = (12 - x) % 11
    if x == 10:
        x = 'X'
    if s[17] == str(x):
        print('YES')
    else:
        print('NO')
```



角谷

```
def jiaogucaixiang(n):
    if n == 1:
        print("End")
        return

    while n != 1:
        if n % 2 == 1:
            next_n = 3 * n + 1
            print(f"{n}*3+1={next_n}")
        else:
            next_n = n // 2
            print(f"{n}/2={next_n}")
        n = next_n

    print("End")



n=int(input())
jiaogucaixiang(n)
```



罗马数字

```
roman_to_int_map = {
    'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000
}

int_to_roman_map = [
    (1000, 'M'), (900, 'CM'), (500, 'D'), (400, 'CD'),
    (100, 'C'), (90, 'XC'), (50, 'L'), (40, 'XL'),
    (10, 'X'), (9, 'IX'), (5, 'V'), (4, 'IV'), (1, 'I')
]

def roman_to_int(s):
    total = 0
    prev_value = 0
    for char in s:
        value = roman_to_int_map[char]
        if value > prev_value:
            total += value - 2 * prev_value  # 处理特殊情况，如IV, IX
        else:
            total += value
        prev_value = value
    return total

def int_to_roman(num):
    result = []
    for value, symbol in int_to_roman_map:
        while num >= value:
            result.append(symbol)
            num -= value
    return ''.join(result)


def main():
    # 输入处理
    input_data = input().strip()
    if input_data.isdigit():
        num = int(input_data)
        print(int_to_roman(num))
    else:
        print(roman_to_int(input_data))

if __name__ == "__main__":
    main()
```