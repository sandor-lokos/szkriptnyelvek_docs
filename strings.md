# Stringek és műveleteik

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
Vagy épp kicserélhetjük a kisbetűket nagy betűkre és vica versa. De a hosszukat is kiírathatjuk.
Utóbbi függvényt (```len()```) azért is érdemes megjegyezni, mert nem a string hosszúságát adja
vissza valójában hanem a tömb hosszúságát, amit jelen esetben a text string jelent.
Adhatunk meg formázott string-eket is:

```
first_name = "John"
last_name = "Doe"
message = first_name + " [" + last_name + "] is a coder"
print(message)
msg = f'{first_name} [{last_name}] is a coder'
print(msg)
```

A gyakorlat szempontjából a legfontosabb string-függvények talán azok, amelyek a string-eket
manipulálni is képesek vagy bonyolultabb ellenőrzéseket tudnak végrehajtani rajtuk. A
teljesség igénye nélkül lássunk párat ezek közül:

```
isalpha()
isalnum()
islower()
isnumeric()
isprintable()
isupper()
replace()
find()
rfind()
split()
```

Még több izgalmas string függvény található [itt](https://www.w3schools.com/python/python_ref_string.asp), ahol ki is lehet próbálni őket.

# Beolvasás promptról

Van lehetőség a felhasználótól adatot bekérni a prompton, bár ez nem egy elterjedt gyakorlat.
Kisebb tesztelésre azonban hasznos lehet, ezért megemlitjük. Erre a célra az ```input()``` nevű
függvény áll rendelkezésre. Az alábbi példa mutatja, hogyan kell használni:

```
name = input('Enter Your Name: ')
print(name)

>> Enter Your Name: Steve
>> 'Steve'
```

Ennél fontosabb és elterjedtebb GUI-ról vagy fájlból beolvasni információkat. Utóbbit
tekintjük át a következő fejezetben.


# Fájlok beolvasása és kiirása

A továbbiakban minden feladat esetén szükségünk lesz fájlok olvasására és írására. Ez a feladat
– mint majdnem minden a Python nyelvben – egyszerű szintaxissal megoldható. Próbaképpen
töltsük le a ```script_1.txt``` fájlt a az e-learning rendszerből. Helyezzük el abba a mappába, amiben
a kódunk is van és futtassuk a következő parancsot:

```
f1 = open("script_1.txt", 'r')
```

Ezzel létrehoztunk egy f1 nevű objektumot. Írassuk ki:

```
f1 = open("script_1.txt", 'r')
print(f1)
>> <_io.TextIOWrapper name='script_1.txt' mode='r' encoding='cp1250'>
```

Ez sokat nem mond egyelőre. Minket jobban érdekel, hogy mi van a fájlban. Ezt az objektumot
így lehet olvasni:

```
print(f1.readlines())
```

Ez a parancs egy tömböt térít vissza, amelynek az elemi a fájl sorai. A nulladik sorban, akármi
is van, az adja a tömb nulladik elemét, az első az elsőt, stb. (Próbálja ki!)
Hogy tudjuk tehát karakterről karakterre olvasni akkor a fájlt? Emlékezzünk, hogy a Pythonban
minden string elsőre, s minden string egy tömb. Próbáljuk meg tehát így:

```
f1 = open("script_1.txt", 'r')
lines = f1.readlines()
line0 = lines[0]
aux_var = line0[11]
print(aux_var)
```

Az első sor megnyitja a fájlt, a második beolvassa a sorokat egy tömbbe, a harmadik a line0
stringet definiálja, az értéke pedig a tömb nulladik eleme. Ezután az aux_var az így definiált
line0 string, azaz tömb 12. elemét kapja, amit végül kiíratunk.
Ha string részleteket, vagy mintákat keresünk persze ezt az egészet érdemes ```for```-ciklussal
automatizálni, de erről majd a következő utána fejezetben lesz szó. Elöljáróban annyit, amennyi
a feladatok megoldásához szükséges:

```
f1 = open("script_1.txt", 'r')
for line in f1.readlines():
print(line[0])
f1.close()
```

Ez a kódrészlet beolvassa a ```script_1.txt``` fájlt és végigfut a sorain majd minden sornak a nulladik
elemét kiírja. Majd bezárjuk a fájlt. A line tehát kezelhető úgy, mint a fájlból egy sor.
A fájlba való kiíratás hasonlóan működik. Ha új fájlt kívánunk létrehozni, akkor a következőt
csináljuk:

```
file1 = open("new_file.txt", "w")
L = ["This is Delhi \n", "This is Paris \n", "This is London \n"]
file1.write("Hello \n")
file1.writelines(L)
file1.close()
file1 = open("new_file.txt","a")
file1.write("Today \n")
file1.close()
```

Az első sorban megnyitunk egy fájlt, amelyik új. A ```w``` jelzi, hogy írni fogjuk, ahogy korábban
az ```r``` jelezte, hogy olvasni fogjuk a fájlt. Ezek után definiálunk egy stringeket tartalmazó tömböt,
majd írunk a fájlba egy szót „Hello”. Ezután az L tömböt is beleírjuk, majd bezárjuk.
A következő három sorban hozzáadjuk a fájlhoz a „Today” szót. Megnyitjuk a fájlt; az a jelzi,
hogy append, azaz hozzárakás következik. Ezután írjuk bele a szót a fájlba, majd bezárjuk.

# Feladatok:
- Próbálja ki a 4. blokkban található string függvényeket!
- Töltse le az ```script_1.txt``` nevű példafájlt és olvassa be!
	- Állapítsa meg, hogy tartalmaz-e olyan sort, amely csupa alfanumerikus értékekből áll.
	- Állapítsa meg, hogy tartalmaz-e olyan sort, amely csupa numerikus értékekből áll.
	- Állapítsa meg, hogy tartalmaz-e olyan sort, amely csak kisbetűből áll.
	- Keresse meg a legrövidebb sort. A sorok számontartásához használhatja az ```i++``` indexelést.