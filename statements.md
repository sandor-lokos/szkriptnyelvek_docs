A korábbiakban láttunk példát vezérlési szerkezetekre. Ilyen volt az ```if-else``` és a ```for``` is. Ezek a
speciális függvények a Python előre definiált függvényei, a használatuk félig-meddig kötött.

# Az if-statement

Korábban már láttunk példát az ```if``` szerkezetre. Ez egy olyan függvény, amely egy, ```bool``` típusú
argumentumot vár. Ha az argumentum ```True```, akkor végrehajtja a függvénybeli utasítást, ha
nem nem. Azt is specifikálhatjuk, hogy mi történjen, ha nem ```True```, azaz ```False``` az argumentum
az ```else``` kulcsszóval. Általánosan tehát így néz ki a szintaxis:
```python
statement = True
if(statement == True):
	print("Igaz")
else:
	print("Hamis")
```
De egyszerűsíthetjük is a kódot:
```python
statement = True
if(statement):
	print("Igaz")
else:
	print("Hamis")
```
Érdemes tudni az ```elif``` elágazási lehetőségről. Ezt akkor használhatjuk, ha több opciót is
szeretnénk megvizsgálni.
```python
i=2
if( i == 1 ):
print("i is equal to 1")
elif( i > 1 ):
print("i is greater than 1")
elif( i < 1):
print("i is less then 1")
```

# A ciklusok, break, continue

Ahogy azt a korábban tanult nyelvekben megszokhattuk, a ```for``` ciklus arra használható, hogy
egy műveletet többször, egymás után megismételjünk. A Pythonban is ```for```-nak hívják ezt
a szerkezetet és hasonlóan működik:
```python
for i in range(10):
	print(i)
```
A ```range()``` függvénynek háromféle definíciója van:
- egy argumentummal: ```range(10)``` jelentése 0, 1, ..., 9
- két argumentummal: ```range(2,5)``` jelentése 2, 3, 4
- három argumentummal: ```range(1, 6, 2)``` jelentése 1, 3, 5
Látszik, hogy az első kettő lehetőség a harmadik speciális esete.
*Feladat*: írjuk át az első két ```range()``` függvényt „három-argumentumossá”!

Hasonlóan egy tömb elemein is értelmezhető a ciklus:
```python
array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
for elements in array:
	print(elements)
```
(A tömbök használata a következő fejezet témája.)

*Kérdés*: mit kapunk a következő kódrészletből?
```python
for elements in "array":
	print(elements)
```

Előfordulhat, hogy nem akarunk az előre megadott range-en végigfutni, csak addig, amíg egy
feltétel nem teljesül, amikor is szeretnék kilépni a for-ciklusból. Erre való a break kulcsszó:
```python
array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
for elements in array:
	if(elements == 4):
		break
	print(elements)
```	
*Kérdés*: Mit kapunk a következő kódból?
```python
array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
for elements in array:
	print(elements)
	if(elements == 4):
		break
```
De az is lehet, hogy egyszerűen csak nem akarjuk figyelembe venni az egyik elemet az
iterációban. Erre pedig a continue kulcsszó való.
```python
array = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
for elements in array:
	if(elements == 4):
		continue
	print(elements)
```
A ```for```-ciklus egyfajta ```while()``` függvényként is felfogható, így pl. a
```python
for i in range(0,3):
	print(i)
```
Ciklus értelmezhető úgy, hogy „írjuk ki az ```i```-t amíg az a 0-3 range-ben van”. Ha így
fogalmazunk, akkor értelmezhető az is, hogy ez a feltétel már nem teljesül. Vagyis folytathatjuk
a mondatot: „range-ben van, és ha ez már nem igaz, akkor pedig írja ki, hogy Finished!”. Ezt
megtehetjük:
```python
for i in range(0,3):
	print(i)
else:
	print("Finished")
```

A ```while``` nagyon hasonló a ```for``` ciklushoz használhatósága tekintetében, de a szintaxis más.
Úgy is gondolhatunk rá, mint egy ```for```-ciklus – ```if```-statement keverékre. Lássunk egy egyszerű
példát amiből megértjük a különbségeket:
```python
i = 0
while(i < 6):
	print(i)
	i+=1
```

Fontos különbségek vehetők észre a ```for``` ciklushoz képest:
- Előre definiálni kell az indexet.
- A léptetésről magunknak kell gondoskodni
- A ```while()``` argumentuma egy logikai állítás
A ```break``` és ```continue``` kulcsszavak ugyanúgy használhatók, mint a ```for``` esetén.

# Egy furcsa if-statement -- az if(__name__ == __main__) idiom

Sok kódban (github: 12.4 M találat), amit az internet találni előfordul a következő, furcsán kinéző ```if```
```python
if __name__ == "__main__":
```
amit elsőre akár a C/C++ nyelvek felől érkezve még egy ```int main()``` jellegű függvénynek is
nézhetünk, pedig szintaktikailag ez csak egy ```if```.

Röviden arra való ez a szerkezet, hogy a kódban el tudjuk különiteni azokat a részeket,
amelyeket szkriptként akarunk futtatni és azokat amelyeket modulként behivni máshol.
Például:
```python
def echo(text, repetitions):
	echoed_text = ""
	for i in range(repetitions, 0, -1):
		echoed_text += f"{text[-i:]}\n"
	return f"{echoed_text.lower()}."

if __name__ == "__main__":
	text = input("Yell something at a mountain: ")
	print(echo(text))
```

Ebben a kódrészletben definiáltunk egy ```echo``` nevű függvényt, ami az argumentumában megadott 
string utolsó betűit ismétli meg. Alatta a furcsa if található, amiben bekérünk a terminálról valami 
szöveget, amit aztán átadunk a függvénynek. Ha lefuttatjuk, ezt látjuk: 
```
> Yell something at a mountain: Ahoy 
hoy
oy
y
.
```

Ugyanakkor meghivhatjuk ezt a függvényt egy másik fájlból is (ld. később a moduloknál) igy: 
```python
from strange_if import echo 
print(echo("Please help me I'm stuck on a mountain"))
```
A ```strange_if``` a fájl neve, amibe mentettem az előző kódrészletet. Itt az echo argumentumát 
nem bekérjük, hanem megadjuk (valamit meg kell adni, különben hibát kapunk). Persze itt is lehetne 
bekérni az ```input()``` függvénnyel, de nem ez a cél, nem ezért van egy külön modulban a függvény, 
hanem azért, hogy más kódokban használhassuk, mint egy rutint. Ha ezt a kódrészletet lefuttatjuk, 
akkor ezt látjuk: 
```
ain
in
n
.
```
anélkül, hogy inputot kellene megadnunk. De mit látunk, ha eltüntetjük a furcsa if-et az előző kódból?
```
Yell something at a mountain: asasaas
aas
as
s
. 
ain
in
n
.
```
Az a rész is lefut, amit igazából nem is akarunk.

Összefoglalva tehát az ```if __name__ == "__main__"``` szerkezetben olyan kódrészleteket tárolunk, 
amelyeket csak akkor akarunk, hogy lefussanak, ha az adott kódot szkriptként futtatjuk.

*Magyarázat*: Felmerülhet, hogy mikor is lesz igaz ez a furcsa ```if```. Mikor egyenlő a
```__name__``` és a ```"__main__"```? Ez akkor lesz igaz, ha a Python interpreter a kódot a 
legfelsőbb szinten futtatja (top-level code), azaz a futtatott kód az, ami minden más modult importál,
vagyis ez a fő kód. Ekkor az interpreter a ```global __name__``` változót beállitja ```"__main__"```-re.

*Feladat*:
- Próbáljuk használni a ```break``` és ```continue``` kulcsszavakat!
- Csináljunk egy Fibonacci-sorozat generátort!
- Számoljuk ki minél pontosabban az aranymetszés-arányt (golden ratio)! Ezt a fenti sorozat utolsó és utolsó előtti generált elemének hányadosa adja meg


Hasznos linkek:
- https://www.w3schools.com/python/python_conditions.asp
- https://www.w3schools.com/python/python_for_loops.asp
- https://www.w3schools.com/python/python_while_loops.asp
- http://nyelvek.inf.elte.hu/leirasok/Python/index.php?chapter=5
- https://realpython.com/if-name-main-python
- https://en.wikipedia.org/wiki/Fibonacci_number