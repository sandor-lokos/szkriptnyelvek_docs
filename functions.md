A változók után, a függvények a legalapvetőbb egységei minden programnyelvnek, ezért fontos
velük részletesen megismerkedni. A második kérdés, amit egy új programnyelv
megismerésekor feltesz az ember az az, hogy hogyan kell függvényt definiálni. Az első az, hogy
hogyan kell változót definiálni.

# A függvény definíciója

C/C++ nyelveken egy függvény – a változókhoz hasonlóan – szintén van típusa, amely attól
függ, hogy milyen típust térít vissza a függvény. Egy `float` típusú függvény `float`-ot, 
egy `void` függvény semmit sem térít vissza. Pythonban – a változókhoz hasonlóan – a függvényeknek
sem kötelező megadni típust, de lehet. A definiálásukhoz egyszerűen a `def` kulcsszót használjuk 
függetlenül attól, hogy mit térítenek vissza, ha egyáltalán.
A függvényt ugyanúgy hívjuk meg, mint a legtöbb programnyelven, a függvény nevét leírva és
megadva a megfelelő argumentumait. (Mindez bizonyára nem ismeretlen, hisz eddig is
használtunk függvényeket, csak nem olyanokat, amelyeket mi definiáltunk.)
Tehát a szintaxis a következő:
```
def example_function(text_to_display):
	print(text_to_display)

example_function("Hello world!")
```
A kimenet:
```
> Hello world!
```
A `def` kulcsszót a függvény neve követi, majd zárójelben a függvény argumentuma(i). Ezt a
sort szintén kettősponttal zárjuk, majd egy tabulátorral behúzva megadjuk, hogy mit is csináljon
a függvény. A példában kiíratjuk az argumentumot. (Vegyük észre, hogy az argumentumnak
sincs típusa!) A függvényt a harmadik sorban használjuk, aminek az eredménye az
argumentumba írt szöveg megjelenése a terminálon.

Természetesen egy függvénynek nem csak egy argumentuma lehet:
```
def example_function(text_to_display, number1_to_add, number2_to_add):
	print(text_to_display)
	print(number1_to_add + number2_to_add)

example_function("Hello world!",1,2)
```
A kimenet ekkor:
```
> Hello world!
> 3
```
Az, hogy a Python nem erősen típusos nyelv könnyelműségre csábíthat, de vannak szabályok,
amik ugyanúgy érvényesek, mint a típusos nyelvekben. Ilyen szabály az is, hogy a függvénynek
pontosan annyi argumentuma kell, hogy legyen, mint amennyivel definiáltuk.
Ez persze sok hiba forrása lehet, amelynek debuggolása esetleg sok időt emészt fel, ezért
célszerű határozatlan számú argumentumot használni. Ezt már C/C++ jellegű nyelvekben is
meg lehetett tenni, ha az argumentum egy tömb vagy vektor. Például:
```
def example_function(text_to_display):
	print(text_to_display[0])
	print(text_to_display[1])
	print(text_to_display[4])
	
example_text_array = ["a", "b", "C", "d", "e"]
example_function(example_text_array)
```
A kimenet:
```
> a
> b
> e
```
De így is lehet csinálni:
```
def add_function( * args ):
	print(args[0]+args[1])

example_function(1, 2)
```
Ekkor a kimenet:
```
> 3
```
Az első variáció egy tömböt ad át a függvénynek, aminek a méretéről maga a függvény nem
tud. A második esetben is hasonló a helyzet azzal a különbséggel, hogy kell egy \* szimbólum,
ami jelöli, hogy az argumentumok száma bizonytalan, de minden bemenő argumentumot
tegyen be egy args nevű tömbbe. Mindkét esetben közös, hogy a függvény tartalma alapján
kiderül, hogy legalább hány argumentum van. Az első esetben ez öt, a második esetben kettő.
Több lehet, kevesebb azért nem, mert akkor a tömb indexek értelmetlenek.


# Kulcsszó argumentumok
C/C++ nyelvek esetén zavart okozhat, ha az argumentumokat összekeverjük, Pythonban
azonban ha keyword, azaz kulcsszó argumentumokat használunk, akkor a sorrend mindegy:
def example_function(text1, text2):
print(text1 + "\t" + text2)
example_function(text1="Hello world!", text2="Hello again!")
example_function(text2="Hello again!", text1="Hello world!")
> Hello world! Hello again!
> Hello world! Hello again!
Ezt akkor is megtehetjük, ha a fent bemutatott, tetszőleges számú argumentumos szintaxist
használjuk:
def example_function(**kwargs):
print(kwargs["text1"] + "\t" + kwargs["text2"])
example_function(text1="Hello world!", text2="Hello again!")
example_function(text2="Hello again!", text1="Hello world!")
> Hello world! Hello again!
> Hello world! Hello again!
A **kwargs tehát egyfajta dictionary-ként működik, amelynek az elemeit kulcsszavakkal
hívhatjuk meg. Érdemes megjegyezni a fenti lehetőséget, mert sok előre megírt csomag esetén
találkozhatunk ezzel a megoldással.
A kulcsszó argumentumok arra is használhatóak, hogy alapértelmezett értéket állítsunk be a
függvény egy paraméterének:
def example_function(text_to_display="Empty"):
print(text_to_display)
example_function()
example_function("Hey, Earth!")
> Empty
> Hey, Earth!
Ahogy azt szintén megszokhattuk, nem csak a print függvénnyel kaphatunk vissza értékeket a
függvényekből, hanem a return kulcsszóval is.
def multiplication(number1,number2):
return number1*number2
result = multiplication(2,2)
print(result)
> 4
Kényelmes megoldás, hogy egyszerre akár több értéket is visszatéríthetünk különösebb
trükközés nélkül:
def multiplication(number1,number2):
return number1*number2, number1, number2
result, num1, num2 = multiplication(2,2)
print(result, num1, num2)
> 4 2 2
A negyedik sorban a sorrendet be kell tartani! A függvények esetén is használható a pass
kulcsszó. Ez akkor lehet hasznos, ha egy függvényt még nem írtunk meg, de definiálni már
definiáltuk:
def myfunc():
pass
Rekurzió
A függvények egyik legjobb tulajdonsága, hogy rekurzívan használhatóak. Ez azt jelenti, hogy
egy függvény hívhatja önmagát. A rekurzióra egy egyszerű példa lehet egy szám faktoriálisának
kiszámítása:
4! = 4 ⋅ 3!
3! = 3 ⋅ 2!
2! = 2 ⋅ 1!
vagyis: 4! = 4 ⋅ 3 ⋅ 2 ⋅ 1
Ezt Pythonban a következőképpen írhatjuk:
def factorial(n):
if n == 0:
return 1
else:
return n * factorial(n-1)
print(factorial(4))
> 24
A függvényeknek ezt a tulajdonságát használhatjuk például keresésre egy listában:
def recursive_search(array,i,pattern):
if(array[i] == pattern):
return True
elif(i>0 and array[i] != pattern):
return recursive_search(array, i-1, pattern)
data = [1, 2, 3, 4, 5, 6, 7, 8, 9]
seached_number = 1
if(recursive_search(data, len(data)-1, seached_number) == True):
print("In the list")
else:
print("Not in the list")
Függvény, mint argumentum
Nagyon hasznos lehet, egy függvényt függvény argumentummal definiálni. Általában
bonyolultabb problémák esetén érdemes alkalmazni.
Előre definiált függvények esetén egyszerűen látható:
def shout(text):
return text.upper()
def whisper(text):
return text.lower()
def greet(func,text):
greeting = func(text)
print(greeting)
greet(shout,"Hi")
greet(whisper,"Hi")
> HI
> hi
Ebben az esetben van egy üvöltő (shout) és egy suttogó (whisper) függvényünk, amelyek egyegy
argumentumot kapnak, egy szöveget, amit csupa nagy vagy csupa kicsi betűvel térítenek
vissza. Ezeket a függvényeket az üdvözlő (greet) függvényben használhatjuk, mint bemenet.
Egy az egyben is beírhattuk volna a shout és a whisper függvényeket a greet függvény
argumentumába, például így:
def shout(text):
return text.upper()
def whisper(text):
return text.lower()
def greet(isShout,text):
if(isShout):
greeting = shout(text)
else:
greeting = whisper(text)
print(greeting)
greet(True,"Hi")
greet(False,"Hi")
A kimenet ugyanaz lesz. De mi a helyzet akkor, ha egy stutter függvényt is szeretnék
definiálni? Akkor nem csak a függvény implementálását kell megoldanunk, de a greet
függvényt is át kell írnunk. Sokkal egyszerűbb és kényelmesebb megoldás az első variációt
megvalósítani és a függvényt adni paraméterként, mint a függvényt egy bool változóval
kiválasztani.
Feladatok:
1. Módosítsa úgy az add_function-t, hogy az argumentumába írt tetszőleges mennyiségű számot összeadja és az eredményt kiírja a terminálra. (Pl. add_function(1, 2, 3, 4) írja ki, hogy 10.
2. Írjuk meg a multiplication függvényt a **kwargs szintaxist használva!
3. Írjuk meg a recursive_search függvényt úgy, hogy *args legyen az array helyett, az alapértelmezett i pedig 1 legyen.
4. Írjuk meg a korábbi Fibonacci-sorozat generátort rekurzívan.
[1] https://www.w3schools.com/python/python_functions.asp [2] https://www.geeksforgeeks.org/passing-function-as-an-argument-in-python/