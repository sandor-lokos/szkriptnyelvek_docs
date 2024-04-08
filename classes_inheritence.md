Az objektum orientál programozás fő eleme az osztály. Egy osztály tulajdonképpen egy gyűjtemény, 
amely változókat és függvényeket tartalmaz, logikus egységben. Létrehozhatunk az osztályhoz tartozó 
példányokat, melyek rendelkezhetnek az osztályban definiált tulajdonságokkal, az osztály tagfüggvényei 
hathatnak rájuk, a változókat akár módosíthatják is. Az öröklődés fogalma is az osztályokhoz kapcsolódik, 
melyet az alábbiakban példákon keresztül fogunk megérteni. A lényeg röviden: az osztályok között is 
lehet hierarchia olyan értelemben, hogy egyes osztályok lehetnek rokoni viszonyban, osztozhatnak bizonyos 
tulajdonságokban, osztozhatnak függvényeken, változókon. Ez akkor hasznos, ha a függvényekből és 
változókból álló logikus gyűjtemény egy másikkal logikailag közösséget mutat. Példa lehet erre egy osztály,
amely kutyák tulajdonságait gyűjti egybe olyan függvények segítségével, melyek az állatok korát, színét, 
marmagasságát és beoltásuk dátumát tartalmazza. Továbbá tartalmazza az oltás típusát. Látható, hogy ez az 
osztály közösséget mutathat egy olyan osztállyal, amely a macskákat gyűjti egybe részben ilyen szempontok 
alapján. Igaz, hogy érdemes külön osztályt definiálunk a két fajra, mert logikailag különbözőek, de 
ugyanakkor az is igaz, hogy a tulajdonságaikat beállító függvények részben vagy egészben azonosak lehetnek.
Ebben az esetben tehát érdemes egy `Dog` és egy `Cat` nevű osztályt is létrehozni amelyek mindketten a `Pet` 
osztályból öröklődnek. A következő metakóddal írhatjuk le ezt az öröklődést:
```
class Pet:
	def age
	def height
	def color
	def shots_type
	def shots_date
class Dog(Pet):
	def self
class Cat(Pet):
	def self
```
Így a `Dog` és a `Cat` osztály is rendelkezik a Pet osztály függvényeivel. Pontosabban szólva a `Dog`
és a `Cat` osztály példányaira is hatnak a `Pet` osztály függvényei. Például így:
```
morzsi = Dog()
morzsi.age(6)
cirmi = Cat()
cirmi.age(3)
```
Ezzel beállítottuk morzsi kutya életkorát 6 évre. Persze az `age` függvényt definiálni kell még. Ha ez 
most még nem világos, nem kell megijedni, a későbbiekben mindezt részletesebben tárgyaljuk.

# Osztály
A fentieknek megfelelően tehát a legegyszerűbb osztály egy olyan, amely csak egy változót
tartalmaz:
```python
class MyFirstClass:
	x = 5

object1 = MyFirstClass()
print(object1.x)
object1.x = 7
print(object1.x)
```
Ennek az osztálynak nem sok hasznát vennénk a gyakorlatban, de a szintaxis első lényeges
eleme már látszik rajta, nevezetesen az, hogy egy osztályt a `class` kulcsszóval kell definiálni,
amit az osztály neve követ, majd kettőspontok után adjuk meg az osztály tartalmát. Jelen
esetben ez egyetlen `x` nevű változó melynek értéke 5. A negyedik sorban láthatjuk, hogy hogyan
lehet példányosítani az osztályt. Az `object1` a `MyFirstClass` osztály egy példánya. Ilyen
példányból bármennyit létre lehet hozni.

Az 5. sorban látszik, hogy hogyan lehet a példány tulajdonságához hozzáférni, a 6. sorban
pedig, hogy hogyan lehet azt módosítani. Mindez nem túl hasznos, de a szintaxis alapjai látszanak a
példán. Ahhoz, hogy az osztályokat pontosabban értsük, a konstruktor fogalmát kell tisztázni.
A konstruktor egy olyan függvény, ami mindig meghívódik, amikor egy példányt létrehozunk és beállítja
az alapvető paraméterek értékeit. Lássunk erre egy példát:
```python
class Dog:
	def __init__(self, name, age, color):
	self.age = age
	self.name = name
	self.color = color

morzsi = Dog("Morzsi",6,"barna")
print(morzsi.age)
print(morzsi.name)
print(morzsi.color)
```
Az első öt sorban definiáljuk az osztályt. A második sorban láthatjuk a konstruktor függvényt,
melyre az `__init__` név van lefoglalva a Pythonban. Ez a függvény előre definiált, nekünk csak
fel kell töltenünk argumentumokkal. Rögtön az első argumentum egy új kulcsszó. A `self`
kulcsszót arra használjuk, hogy az osztály elemeire hivatkozzunk. Itt, az első argumentumban
vezetjük be (nem kötelező a `self` nevet adni neki, de a PyCharm erre egészíti ki automatikusan
az `__init__` függvényt, minthogy ez egy elterjedt konvenció), és ezek után ezzel hivatkozunk az osztály 
tagjaira, ahogy azt a későbbiekben látni fogjuk. A másik három argumentum jelentése világos. 
A következő három sorban létrehozzuk az osztály tulajdonságait, azaz a változóit. Praktikusan ugyanazt
a nevet adjuk nekik, de ez sem kötelező. Itt látszik, hogy a self kulcsszót hogyan használjuk.
Az osztály definíciója után példányosítjuk, azaz létrehozunk egy `Dog` példányt, morzsit. A
konstruktornak megadjuk a paramétereket. Ez kötelező! A következő három sorban lekérjük a beállított 
értékeket, hozzáférünk a változókhoz. Létrehozhatunk további példányokat is:
```python
morzsi = Dog("Morzsi",6,"barna")
bodri = Dog("Bodri",3,"fekete")
fido = Dog("Fido",8,"feher")
print(morzsi.age)
print(bodri.name)
print(fido.color)
```
Példányok egyes tulajdonságait vagy a teljes példányt törölhetjük a `del` kulcsszóval:
```
del fido.age
del fido
```
Ami eddig talán nem volt feltűnő, de fontos lehet az alkalmazások szempontjából az az, hogy
a változók a program bármely pontján tartósan átírhatók. Korábban megszokhattuk, hogy az
osztályoknak kétféle változója/függvénye van: `private` és `public`. A `private` helyett időnként
előfordul a `protected` kulcsszó is. A Python nyelvben ilyen funkció nem érhető el, de
megoldható. Mi is volt a `private` változó lényege? Az, hogy az osztályon kívülről nem lehetett módosítani
az értékét. Ez úgy lehet megoldani, hogy a `__` dupla aláhúzás prefixumot tesszük a változó elé,
így megnehezítjük a változóhoz való hozzáférést:
```python
class A:
	def __init__(self):
		self.__var = 123
	def printVar(self):
		print(self.__var)
x = A()
x.__var # Ez hibat ad, így nem lehet hozzaferni a valtozohoz
x.printVar() # Igy mar jó lesz
```
Azonban ezt is könnyű megheckelni, ahogy az egész fenti konstrukció is inkább egy heck, mint
szándékos tulajdonság:
```python
print(x.__dict__)
x._A__var = 456
x.printVar()
```
A `x.__dict__` sorral irathajuk ki az `x` objektum tartalmát és megtudhatjuk, hogy a második sor
alapján lehet hozzáférni a `__var` változóhoz, amit meg is teszünk és így meg is változott az
értéke. A tanulság tehát az, hogy nincs igazi `private` változó a Python osztályok esetén, de tehetünk
erőfeszítést arra, hogy hasonló legyen. Az is igaz, hogy más meg tehet erőfeszítést arra, hogy
ezt figyelmen kívül hagyja.


# Öröklődés

Ahogy azt a bevezetésben már tárgyaltuk, az öröklődés egy osztályok közötti kapcsolat.
Öröklődés szülő és gyerek (parent and child/derived class) között van. Ezt a struktúrát akkor
érdemes kihasználni, ha vannak olyan osztályok, melyek több közös függvénnyel is
rendelkeznek. Ekkor a két osztály valamilyen logika szerint hasonló. Lássuk a fenti példát,
amikor is létrehozunk egy Pet nevű osztályt, amelyből öröklődik a `Dog` és a `Cat` nevű osztály.
```python
class Pet:
	def walk(self):
		print("walk")
		
class Dog(Pet):
	def bark(self):
		print("bark")
		
class Cat(Pet):
	pass

cirmi = Cat()
morzsi = Dog()
morzsi.walk()
morzsi.bark()
cirmi.walk()
cirmi.bark()
```
A kimeneten ekkor
```
> walk
> bark
> walk
cirmi.bark()
AttributeError: 'Cat' object has no attribute 'bark'
```
Három osztályt definiáltunk: a `Pet` osztályt, melynek egy tagfüggvénye van, a `walk()`. Ebből az
osztályból öröklődik a `Dog` és a `Cat` osztály. A `Dog` osztálynak is van egy tagfüggvénye, a `bark()`.
A `Cat` osztály üres. A példányosítás után, azaz amikor létrehoztuk Morzsit és Cirmit, a használat során
látszik, hogy a `Cat` osztály hiába üres, a `Pet` osztályban definiált `walk()` függvényt tudja használni. 
Morzsi szintén tudja használni a `walk()` függvényt. Viszont Cirmi nem tudja használni a `bark()`
függvényt, ahogy azt a hibaüzenet is jelzi, mert az olyan osztályban van, amelyhez semmi köze.
Testvérosztályok nem léteznek. Azt azonban megtehetjük, hogy a `Cat` függvényt még egy
„szinttel lejjebb” definiáljuk és nem a `Pet` hanem a `Dog` osztályból deriváljuk:
```
class Cat(Dog):
	pass
```
Ekkor már használhatja Cirmi a `bark()` és a `walk()` függvényt is. Utóbbi azt jelzi, hogy
többszörös öröklődés is lehetséges. A `walk()` függvény ugyanis a `Pet` osztály tagfüggvénye,
amely osztályból öröklődéssel használhatja a `Dog` osztály. De ha a `Dog` osztályból deriválunk
egy másikat, akkor az használhatja nemcsak a `Dog` osztály függvényeit, hanem azokat is,
amelyeket a `Dog` osztály használhat. Öröklődés nem csak egy osztályból lehetséges. Hozzuk létre a
`Mammal` osztályt, amelynek egyetlen tagfüggvénye lesz, a `live()`. Ebből az osztályból is öröklődjön
a `Cat` osztály, örökölve a `live()` tagfüggvényt:
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

cirmi = Cat()
morzsi = Dog()
morzsi.walk()
morzsi.bark()
cirmi.walk()
cirmi.bark()
cirmi.live()
```
A kimenet tehát
```
> walk
> bark
> walk
> bark
> heartbeat
```
Látható, hogy a `Cat` osztály, bár üres, az öröklődés révén minden definiált függvényhez
hozzáfér, azokat használhatja.