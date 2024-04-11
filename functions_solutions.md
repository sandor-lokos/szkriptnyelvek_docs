```python
## Exercise 1
def add_function(*args):
    sum = 0
    for i in range(len(args)):
        sum += args[i]
    print(sum)

add_function(1, 2, 3, 4, 5, 6, 7)

## Exercise 2
def multiplication(**kwargs):
    return kwargs["number1"] * kwargs["number2"] * kwargs["number3"]

result = multiplication(number1=2, number2=2, number3=3)

print(result)


## Exercise 3
def recursive_search(*args,i=1,pattern):
    if(args[0][i] == pattern):
        return True
    elif(i>0 and args[0][i] != pattern):
        return recursive_search(args[0],i=i-1,pattern=pattern)

data = [1, 2, 3, 4, 5, 6, 7, 8, 9]
searched_number = 11
if(recursive_search(data,i=len(data)-1,pattern=searched_number)):
    print("In the list")
else:
    print("Not in the list")

## Exercise 4
def recursive_Fibonacci(n):
    if(n <= 1):
        return 1
    else:
        return recursive_Fibonacci(n-1) + recursive_Fibonacci(n-2)

nterms = input("Adjon meg a lepesek szamat: ")
if(int(nterms) < 1):
    # bonyolultabb ellenőrzést is lehet
    raise Exception("0-nal nagyobb szamot kell megadni!")
else:
    print("Fibonacci-sorozat:")
    for i in range(int(nterms)):
        print(recursive_Fibonacci(i))
```
