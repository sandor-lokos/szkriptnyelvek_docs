A Pythonban alapesetben minden karakterlánc string-ként van értelmezve. Egy karakter egy string, de egy karakterlánc is string. Egy karakterlánc string-ek tömbjeként is felfogható:
```
msg = 'Triple quotes to write multiple line messages'
print(msg[0]+msg[1])
print(msg[0]+msg[1]+msg[2]+msg[3]+msg[4]+msg[5])
print msg
```
A példa kimenetének az első sora „Tr”, a második „Triple”, a harmadik kiírja az egész msg stringet. Látszik, hogy az msg tömbként és önálló egész stringként is felfogható. A későbbiekben ezen alapulnak olyan függvények, melyek darabolják vagy épp összerakják a stringeket.

Kereshetünk is string-ekben betűket vagy töredékeket:

```
text = "Example text here"
print(text.find('E'))
print(text.find('e')) # There are more. The first will be returned
print(text.find('A')) # -1 will be returned because there is not any A letter
print(len(text))
```