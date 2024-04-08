
Amint azt korábban láttuk, a Pythonban többféle hiba is lehetséges. Ezeket a kód futtatása
közben az interpreter közli velünk. Például
```python
print("Error" + 3)
print("Error" + 3)
TypeError: can only concatenate str (not "int") to str
```
Ez egy `TypeError`, azaz típushiba, ami azt jelenti, hogy nem vettük figyelembe egy vagy több
változó típusát valamilyen művelet végrehajtása során. Ebben a konkrét példában össze
akartunk adni egy `string`-et egy `int`-tel, amint azt az interpreter jelzi is nekünk.
Többféle ilyen hiba is van, melyekre egy teljes lista található [itt](https://docs.python.org/3/library/exceptions.html).
A Python egyik hátránya, hogy ezek a hibák futási időben derülnek ki, ha nem voltunk elég körültekintőek és
például tipus nélkül definiáltuk a függvényünket. Arról, hogy hogyan lehet tipusosan definiálni, [itt](https://github.com/sandor-lokos/szkriptnyelvek_docs/blob/main/functions.md#a-tipusosan-defini%C3%A1lt-f%C3%BCggv%C3%A9nyek-type-hints) beszéltünk.
Mégis tudunk tenni azért, hogy ez a lehető legkevésbé legyen kellemetlen.
Az ilyen „beépített” hibákat, azaz az olyanokat, amelyeket az interpreter felismer, a try-except
szerkezettel tudjuk kezelni. Erre egy egyszerű példa a következő:
```python
try:
	print(x)
except:
	print("x is not defined")
	print("Something's funny")
```
Aminek a kimenete:
```
> x is not defined
> Something's funny˛
```
Az előnye ennek a szerkezetnek, hogy a kód nem akad meg a hibánál, a második `print` is
végrehajtódik, de a hibáról értesülünk!
Több exception-t is megadhatunk:
```python
try:
	print(x)
except TypeError:
	print("x is not the appropriate type")
except NameError:
	print("x is not defined")
except:
	print("Something's funny")
```
Ami a következőt adja
```
> x is not defined
```
Érezhető, hogy a `try-except` egyfajta `if-else` szerkezet. Nem meglepő tehát, hogy az `else`
kulcsszó is használható:
```python
try:
	print("Hello")
except:
	print("Something went wrong")
else:
	print("Nothing went wrong")
```
```
> Hello
> Nothing went wrong
```
Előfordulhat, hogy egy utasítást végre szeretnénk hajtani, függetlenül attól, hogy mi a `try-except`
végeredménye. Ezt a `finally` kulcsszóval tehetjük meg:
```python
try:
	print(x)
except:
	print("Something went wrong")
finally:
	print("The 'try except' is finished")
```
```
> Something went wrong
> The 'try except' is finished
```
Mi magunk is meghatározhatunk `exception`-öket. Ez fontos lehet akkor, ha egy változó értékét
egy adott tartományban szeretnénk tartani. Például:
```python
import numpy

def square_root(x):
	if(x < 0):
		raise Exception("Only positive numbers are allowed!")
	return numpy.sqrt(x)
	
print(square_root(3))
print(square_root(-1))
```
```
> 1.7320508075688772
> raise Exception("Only positive numbers are allowed!")
> Exception: Only positive numbers are allowed!
```
Előre definiált hibatípusokat is használhatunk persze:
```python
x = "hello"
if not type(x) is int:
	raise TypeError("Only integers are allowed")
```
Ekkor ezt látjuk
```
> raise TypeError("Only integers are allowed")
> TypeError: Only integers are allowed
```
*Feladat*: az előző részben írt rekurzív Fibonacci-sorozat generátort írjuk át úgy, hogy
ellenőrizzük a bemenetet. Ha nem konvertálható számmá, vagy ha 1-nél kisebb, akkor adjunk
hibát!

## Hasznos linkek

- https://docs.python.org/3/library/exceptions.html
- https://docs.python.org/3/tutorial/errors.html
- https://www.w3schools.com/python/python_try_except.asp