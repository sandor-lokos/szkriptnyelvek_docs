Ahogy azt korábban is láttuk, a Python minden változót stringként értelmez első körben és ha
egy string hosszabb, mint egyetlen karakter, akkor azt stringek listájaként is fel lehet fogni. A
lista egy a négy tömb típus közül a Pythonban. Ezeket fogjuk ebben a részben végig tárgyalni.

# List-ek

Kezdjük azzal a típussal, amivel már találkoztunk. A lista egy olyan tömb típus a Pythonban,
ami rendezett, változtatható és megengedi, hogy egy elem kétszer is szerepeljen. Példát ilyen
listára már sokat láttunk, de azért felsorolunk néhányat.
```
example_list1 = ["a", "b", "c"]
example_list2 = "abc"
example_list3 = [1,2,3,4]
example_list4 = ["a", 1, "b", 2, "c", 3]
```
Egy ilyen lista elemire az indexeikkel lehet hivatkozni. Pl.
```
example_list1 = ["a", "b", "c"]
print(example_list1[1])
```
A kimenet:
```
> b
```
Több, listákra vonatkozó függvény is létezik, melyek közül néhányat már ismerünk. Ilyen
függvények a lista hosszát visszatérítő ```len()``` és a lista végére egy elemet hozzárakó ```append()```.
A függvényekről egy teljes lista található [itt](https://www.programiz.com/python-programming/methods/list).
Tekintsük át a fontosabbakat:
- ```append()```: a lista végéhez ad egy, az argumentumában megadott elemet
- ```insert()```: megadott indexszel beilleszt egy elemet a listába
- ```index()```: megkeres egy elemet a listában és visszatéríti az indexét (opcionálisan a listának csak egy részében keres
- ```remove()```: eltávolítja az argumentumában lévő elemet
- ```pop()```: eltávolítja az argumentumában lévő indexnek megfelelő elemet
- ```sort()```: sorrendbe állítja az elemeket ABC vagy növekvő érték szerint (opcionális ```key```-argumentumokkal fordított sorrend is lehetséges)
Most lássunk egy-egy példát ezekre:
```
example_list = ["A",1,3,5,7,9,2,4,6,8,"B"]
print(len(example_list))
```
A kimenet:
```
> 11
```
```
print(example_list)
```
A kimenet:
```
> ['A', 1, 3, 5, 7, 9, 2, 4, 6, 8, 'B']
```
```
example_list.append(11)
example_list.insert(10,10)
print(example_list)
```
A kimenet:
```
> ['A', 1, 3, 5, 7, 9, 2, 4, 6, 8, 10, 'B', 11]
```
```
example_list.remove("A")
index_of_B = example_list.index("B")
example_list.pop(index_of_B)
print(example_list)
```
A kimenet:
```
> [1, 3, 5, 7, 9, 2, 4, 6, 8, 10, 11]
```
```
example_list.sort()
print(example_list)
```
A kimenet:
```
> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
```
```
example_list.sort(reverse=True)
print(example_list)
```
A kimenet:
```
> [11, 10, 9, 8, 7, 6, 5, 4, 3, 2, 1]
```
Egyszerű, de hasznos és szintaktikailag egyszerű funkciók sora érhető el listákhoz, melyek
közül jónéhánnyal már találkoztunk, így itt csak példa szintjén említjük:
```
example_list = ["apple", "banana", "cherry"]
# loop on a list
for x in example_list:
	print(x)


# check if an element is in the list
if "apple" in example_list:
	print("Yes, 'apple' is in the fruits list")

	
# "adding" two list
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]
list3 = list1 + list2
print(list3)


# can append too
list1 = ["a", "b", "c"]
list2 = [1, 2, 3]

for x in list2:
	list1.append(x)
print(list1)
```

# Tuple-ök

A tuple egy olyan tömbtípus, amelynek _nem_ tudjuk az elemeit megváltoztatni. A fenti
függvények ugyan nem használhatóak, mivel azok mind valamilyen változást idéznek elő, de
az index műveletek ugyanúgy működnek, mint ahogy azt megszoktuk:
```
thistuple = ("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")
print(thistuple[2:-1])
```
Természetesen van mód a tuple tartalmának megváltoztatására, de csak közvetett módszerrel:
```
x = ("1", "2", "3")
print(x)
```
A kimenet:
```
> ('1', '2', '3')
```
```
y = list(x)
y[1] = "3"
x = tuple(y)
print(x)
```
A kimenet:
```
> ('1', '3', '3')
```
Látható, hogy úgy tudtuk csak megváltoztatni a tuple egy elemét, ha azt listává konvertáltuk,
majd vissza tuple-é. Ez nem egy bevett gyakorlat. Ha tudjuk, hogy változtatni akarjuk egy
tömbünk elemét, akkor eleve listaként definiáljuk. Ha nem akarjuk megváltoztatni, akkor
pedig tuple-ként.
A megváltoztathatatlanságból eredő megkötéseken kívül minden ugyanúgy alkalmazható a
tuple-ök esetén, mint a list-eknél.

# Halmazok avagy set-ek

A halmazok olyan tömb típusok, amelyeken nincs rendezés, vagyis elemek gyűjteménye.
Ennek megfelelően el lehet belőlük elemeket távolítani, hozzájuk is lehet adni, de az indexhez
kapcsolódó műveleteknek nincs értelmük. Nézzünk néhány példát:
```
example_set = {"A", "B", "C"}
example_set.add("D")
example_set.update(["E", "F", "G"])
example_set.remove("A")
example_set.discard("B")
print(example_set)
```
Vegyük észre, hogy elemet kétféleképpen is adhatunk egy halmazhoz attól függően, hogy egy
vagy több elemet szeretnénk egyszerre hozzáadni.
A példán nem látszik, de a ```remove()``` és a ```discard()``` függvények között fontos különbség van,
amely a felhasználás szempontjából lényeges lehet. A ```remove()``` függvény hibát ad, ha a
törölni kívánt elem nem létezik, míg a ```discard()``` nem. Ez akkor lehet fontos, hogyha csak
akkor akarunk egy elemet törölni, ha az létezik a listában, de ha nem az sem baj, haladhatunk
tovább. Ilyen esetben a ```remove()``` függvény feleslegesen akasztja meg a futtatást, amelyet csak
egy ```if``` statement-tel tudnánk elkerülni (ld. feladatok).

A halmazokkal matematikai halmazműveleteket is végezhetünk, úgymint az unió, metszet, stb.
Ezek nem túl hasznosak, így nem térünk ki rájuk, de a halmazokon használható függvények
teljes listája megtalálható [itt](https://www.w3schools.com/python/python_sets.asp) megtalálható.


# Dictionary-k

A dictionary Pythonban leginkább a C/C++-os ```struct```-hoz hasonló, általában különböző típusú
változók rendezett és változtatható tartalmú tömbje.
```
thisdict = {
"brand": "Ford",
"model": "Mustang",
"year": 1964
}
print(thisdict)
```
A kimenet:
```
> {'brand': 'Ford', 'model': 'Mustang', 'year': 1964}
```
Elemekhez hozzáférni úgy lehet, mint a listák esetén, de index helyett a kulcsszavakat lehet
használni:
```
print(thisdict.get("model"))
```
A kimenet:
```
> Mustang
```
```
print(thisdict["model"])
```

```
> Mustang
```
```
thisdict["year"] = 2018
print(thisdict.get("year"))
```

```
> 2018
```
A ```for``` looppal a kulcsszavakat és az azokhoz tartozó értékeket is elérhetjük:
```
for x in thisdict:
	print(str(x) + ": " + str(thisdict[x]))
```

```
> brand: Ford
> model: Mustang
> year: 2018
```
Figyeljünk fel a szintaxisbeli különbségre!
Az egyértelműség kedvéért használhatjuk a ```values()``` és az ```items()``` kulcsszavakat.
```
for x in thisdict.values():
	print(x)
```

```
> Ford
> Mustang
> 2018
```
```
for x, y in thisdict.items():
	print(x, y)
```

```
> brand Ford
> model Mustang
> year 2018
```

Ellenőrizhetjük, hogy létezik-e egy adott kulcsszó, illetve újakat is definiálhatunk:
```
if "model" in thisdict:
	print("Yes, 'model' is one of the keys in the thisdict dictionary")
if "color" not in thisdict:
	thisdict["color"] = "red"
print(thisdict)
```

```
> Yes, 'model' is one of the keys in the thisdict dictionary
> {'brand': 'Ford', 'model': 'Mustang', 'year': 1964, 'color': 'red'}
```

Törölni több függvénnyel is lehet. Ezek közül az egyik a ```del```, amivel azonban vigyázni kell,
mert az egész dictionary-t ki tudja törölni:

```
del thisdict["model"]
print(thisdict)
```

```
> {'brand': 'Ford', 'year': 1964, 'color': 'red'}
```
```
del thisdict
print(thisdict)
```

```
> NameError: name 'thisdict' is not defined
```

A dictionary-k esetén használható összes függvényekről egy lista [itt]( https://www.w3schools.com/python/python_dictionaries.asp) található.

# Feladatok:
- Írjunk a remove() függvény segítségével olyan kódot, ami helyettesítené a discard() függvényt!
- Írjunk egy programot, ami összegzi egy lista elemeit!
- Írjunk olyan programot, amelyik megtalálja egy lista vagy tuple legnagyobb elemét
- Írjunk olyan programot, amelyik megszámolja egy listában az olyan stringeket, amelyeknek az első és az utolsó karaktere azonos. Legyen a lista a következő:  ```x = ["1211" , "abcdae" , "xyz" , "abba", "11", "ffgtt"]``` . A várt eredmény: 3.
- Írjunk olyan programot, amely eltávolítja egy listából a duplumokat. Pl.: 
```x=[1, 2, 3, 4, 4, 5, 6, 7, 8, 8, 1, 2]``` -> ```y=[1, 2, 3, 4, 5, 6, 7, 8]```. (Segítség: használjuk ki a halmazok azon tulajdonságát, hogy nem tartalmazhatnak duplumot.)
- Készítsünk telefonkönyvet! Olvassunk be egy nevet, majd egy telefonszámot. Ezt ismételjük meg 5 név – telefonszám párra és rendezzük ezeket egy dictionary-ba. Írassuk ki a teljes telefonkönyvet!

## Beadható feladat:
Módosítsuk az utolsó feladatot úgy, hogy a telefonkönyv adatbevitele egy kulcsszóra álljon le. Ez lehet például a „end”, mint név, vagy ha „name” és „number” input is üres.