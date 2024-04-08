Az életet és a kódok olvashatóságát tovább könnyíti, ha függvényeinket és osztályainkat egy
külön fájlban, a felhasználó számára nem szembeszökő módon tároljuk. Ezt könnyen
megvalósíthatjuk és mindössze az `import` kulcsszót kell ismernünk. Az előző osztályos példa
esetén például a következőképpen járhatunk el:
- Létrehozunk egy animals.py nevű fájl, amely tartalmazza az osztályok definícióit:
	```python
	class Mammal:
		def live(self):
			print("heartbeat")
	class Pet:
		def walk(self):
			print("walk")
	class Dog(Pet):
		def bark(self):
			print("bark")
	class Cat(Dog, Mammal):
		pass
	```
- És létrehozunk egy fájlt, amiben ezeket a függvényeket használjuk:
	```python
	import animals
	cirmi = animals.Cat()
	morzsi = animals.Dog()
	morzsi.walk()
	morzsi.bark()
	cirmi.walk()
	cirmi.bark()
	cirmi.live()
	```
	
Látszik, hogy az osztályokat tartalmazó fájl az import kulcsszóval tudtuk behívni, és a fájl nevét
használva tudtunk a példányosítani. Ha nagyon hosszú egy ilyen fájl neve vagy csak lusták vagyunk akkor
```python
import animals as ani

cirmi = ani.Cat()
morzsi = ani.Dog()
morzsi.walk()
morzsi.bark()
cirmi.walk()
cirmi.bark()
cirmi.live()
```
módon is eljárhatunk. Ezt előre definiált modulokkal is megtehetjük:
```python
import numpy as np

print(np.pi)
```

Azt is megtehetjük, hogy egy modulból csak egy-egy függvényt importálunk:
```python
from numpy import pi, sin
print(str(pi) + "\t" + str(sin(pi)))
```
Persze ezt saját osztályokkal és függvényekkel is megtehetjük, sőt az `as` kulcsszó ekkor is
használható:
```python
from animals import Cat as kitty
cirmi = kitty()
cirmi.walk()
```
A fenti két példában több fontos tanulság is van:
- Egy modulnak konstansát, tagfüggvényét és osztályát is be lehet hívni külön vagy
együtt, mindent az `import` kulcsszóval.
- Ha a `from … import` szerkezetet használjuk, akkor a kódban nem kell a `module.function`
szerkezetet követni, elég a függvény nevét használni. (Ez logikus is, hiszen azzal, hogy
megmondtuk az interpreternek hogy melyik modulból kérjük a függvényt, már nem kell
külön még egyszer megmondani a kódban.)
- Az `as` kulcsszó akkor is használható, ha nem az egész modult hívjuk be.
Vannak előre definiált modulok, amelyeket mindig a feladatnak megfelelően behívunk vagy
sem.