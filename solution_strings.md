```python
f1 = open("script_1.txt", 'r')
lines = f1.readlines()
#print(lines)
i = 0
temp = lines[0]

for line in lines:
    line = line.replace('\n','')
    print(line)
    print(line.isalpha())
    print(line.isalnum())  # 2/a
    print(line.isnumeric())  # 2/b
    print(line.islower())  # 2/c
    i = i + 1
    if len(line) < len(temp):
        temp = line

print(temp)  # 2/d
f1.close()
```
