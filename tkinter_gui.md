A Tkinter az egyik legelterjedtebb GUI Python modul, ha nem is a legszebb. A nativ ablakkezelőt használja,
cross-platform, de elég minimál dizájnt tesz lehetővé. Ugyanakkor könnyen kezelhető, gyorsan lehet eredményt
elérni úgyhogy érdemes megismerkedni vele.

# Az első program

A Tkinter modult nem kell telepiteni, a Python standard library része, vagyis egyszerűen csak be kell
importálni. Hozzunk létre egy üres ablakot.
```python
import tkinter as tk

window = tk.Tk()
window.mainloop()
```

# Widgetek

A `tk.Label` osztállyal különböző widgeteket adhatunk az ablakhoz. Például tegyünk egy kis szöveget az
ablakba. Ezt két sorban lehet megtenni. Az egyik a már emlitett `Label`, amit az elkészitás után valahogy
az ablakhoz kell adni. Erre most a `pack()` metódust használjuk:
```python
import tkinter as tk

window = tk.Tk()
greeting = tk.Label(text="Hello, User!")
greeting.pack()
window.mainloop()
```
Mindkét eddigi kódrészletet a `mainloop()` metódussal futtatunk le. Ez hivják *event loop*nak. Ez arra
figyel, hogy történik-e valami billentyűlenyomás vagy kattintás és blokkol minden kódot, ami utána
következik, amig be nem zárjuk az ablakot. Ennek később lesz jelentősége.

De az üres ablakok nem tól hasznosak egy GUI-ban, úgyhogy most tekintsük át, milyen widgetek vannak
még, amelyekkel dolgozni lehet.

| Widget osztály | Leirás |
| -------------- | ------ |
| `Label`  | Szöveg megjelenitése a képernyőn |
| `Button` | Gomb, ami tartalmazhat szöveget és végrehajthat valamit, amikor rákattintanak |
| `Entry`  | Egysoros bemenetet fogad  |
| `Text`   | Többsoros bemenetet fogad |
| `Frame`  | Négyszög alakú terület, amivel widgeteket lehet csoportositani |

Ezek csak a klasszikus widgetek, amelyekkel foglalkozni fogunk. Vannak themed widgetek is, amelyek
további lehetőségeket biztositanak a GUI egyénivé tételére.

## Szöveg megjelenitése

Ahogy láttuk, erre a `Label` osztály van, ami egyébként képet is meg tud jeleniteni. A megjelenitett
szöveget a felhasználó nem szerkesztheti. A fenti példában láttuk, hogyan lehet szöveget megjeleniteni.
További kulcsszó argumentumok is léteznek, amelyekkel tovább specifikálható a megjelenés. Például a
háttér és az előtér, vagyis jelen esetben a szöveg szintén megadhatjuk a `background` és `foreground`
argumentumokkal, amik helyett a röviditéseket is használhatjuk (`bg` és `fg`)
```python
import tkinter as tk

window = tk.Tk()
greeting = tk.Label(text="Hello, User!", fg="blue", bg="brown")
greeting.pack()
window.mainloop()
```
A legtöbb HTML szin név müködik a Tkinterrel, de a hexadecimális kódot is használhatjuk
```python
greeting = tk.Label(text="Hello, User!", fg="#0000FF", bg="#A52A2A")
```
Megadhatjuk az ablak méretét is
```python
import tkinter as tk

window = tk.Tk()
greeting = tk.Label(
    text="Hello, User!",
    foreground="#0000FF",
    background="#A52A2A",
    height=10,
    width=10)
greeting.pack()
window.mainloop()
```
Az ablak azért nem lesz négyzet, mert a méretek mértékegysége nem SI hanem szövegegység, vagyis a `0`
karakter az egység az adott operációs rendszer alapértelmezett betűtipusában.

## Kattintható gomb megjelenitése

A `Button` widget osztály való kattintható gombok létrehozására. A `Label`-hez hasonló módon lehet
konfigurálni ezt is
```python
import tkinter as tk

window = tk.Tk()
button = tk.Button(
    text="Click me!",
    width=25,
    height=5,
    bg="blue",
    fg="yellow",
)
button.pack()
window.mainloop()
```
Lássuk, hogyan lehet funkciót hozzáadni.

## Bemenetet kezelése

Egy ilyen widget használható olyan rövid stringek fogadására, mint név vagy email cim. Ez a tipusú
widget is nagyon hasonlóan konfigurálható, mint az előző kettő.
```python
import tkinter as tk

window = tk.Tk()
entry = tk.Entry(fg="black", bg="white", width=50)
entry.pack()
window.mainloop()
```
De igazából nem a stilus az érdekes, hanem hogy a beirt információkat kezeljük. Erre három fő metódus
van
- `.get()` szöveg fogadásra
- `.delele()` szöveg törlésére
- `.insert()` szöveg beszúrására
Egy `Label`-lel jelezhetjük is, hogy mit várunk a felhasználótól. De valahogy végre is kell hajtanunk
a parancsokat, meg kell hivnunk a függvényeket. Foglalkozzunk először csak a `.get()`-tel. Ezt egy gombbal
fogjuk meghivni. Ezt a `Button` osztály `command` metódusával tehetjük meg. A következő a példa:
```python
import tkinter as tk

def get_value(from, to): #This part for getting entry.
    name = entry.get()
    print(name)

window = tk.Tk()

# Label
label = tk.Label(
    text="Hello, User! Please add your name below!",
    fg="white", # Set the text color to white,
    bg="black", # Set the background color to black,
    width=40,
    height=5
)
label.pack()

# Entry
label = tk.Label(text="Name")
entry = tk.Entry()

# Button
button = tk.Button(
    text="Click me!",
    width=15,
    height=3,
    bg="blue",
    fg="yellow",
    command=lambda: get_value(1.0, tk.END) # function added here
)

label.pack()
entry.pack()
button.pack()

window.mainloop()
```
Látható, hogy a `.get()` függvényt nem közvetlenül használtuk, hanem egy függvényen keresztül, amit a
gomb `command` paraméterén keresztül hivtunk meg.

*Feladat*: próbáljunk implementálni egy Törlés és egy Beillesztés gombot amelyek a `.delete()` és
`.insert()` metódusokat használják.

## Több sor beolvasása

Ha több sort szeretnénk beolvasni, akkor az `Entry()` helyett a `Text()`-et kell használni. Próbáljuk
ki, mi történik, ha egyszerűen csak kicseréljük a függvényt.

Sajnos ilyenkor hibát kapunk
```python
TypeError: Text.get() missing 1 required positional argument: 'index1'
```
Ennek az az oka, hogy ilyenkor a `.get()` függvénynek meg kell adnunk egy kezdő és egy végindexet.
Jó eséllyel az egész szöveget szeretnénk beolvasni. A kezdő karaktert `1.0`-val jelöljük, az
utolsót pedig `tk.END`-del.

Ha azonban meg akarjuk tartani a flexibilitást, azaz szeretnénk ezeket az argumentumokat nem a
`.get()`-be, hanem a saját `get_value()` függvényünk argumentumaként definiálni, akkor persze
megtehetjük, de át is kell adnunk ezeket valahogy, amikor hivjuk ezt a függvényt a gombban.
Ezt legegyszerűbben egy `lambda`-val lehet megtenni, amiről a [funkcionális programozásról](https://github.com/sandor-lokos/szkriptnyelvek_docs/blob/main/functional.md)
szóló részben már volt szó. Lássuk tehát a módositott példát.
```python
import tkinter as tk

def get_value(start, end): #This part for getting entry.
    name = entry.get(start, end)
    print(name)

window = tk.Tk()

# Label
label = tk.Label(
    text="Hello, User! Please add your name below!",
    fg="white", # Set the text color to white,
    bg="black", # Set the background color to black,
    width=40,
    height=5
)
label.pack()

# Entry
label = tk.Label(text="Name")
entry = tk.Text()

# Button
button = tk.Button(
    text="Click me!",
    width=15,
    height=3,
    bg="blue",
    fg="yellow",
    command=lambda: get_value(1.0, tk.END)
)

label.pack()
entry.pack()
button.pack()

window.mainloop()
```

*Feladat*: Cserélgessük meg a `.pack()` sorokat. Mi történik?

## Frame-ek



# Megjelenés beállitásai a Geometry manager-rel

# Interaktivitás

# Fahrenheit-Celsius átváltó (példa)

