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
- `.delete()` szöveg törlésére
- `.insert()` szöveg beszúrására
Egy `Label`-lel jelezhetjük is, hogy mit várunk a felhasználótól. De valahogy végre is kell hajtanunk
a parancsokat, meg kell hivnunk a függvényeket. Foglalkozzunk először csak a `.get()`-tel. Ezt egy gombbal
fogjuk meghivni. Ezt a `Button` osztály `command` metódusával tehetjük meg. A következő a példa:
```python
import tkinter as tk

def get_value(): #This part for getting entry.
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
    command= lambda: get_value()# function added here
)

label.pack()
button.pack()
entry.pack()

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

A `Frame` osztály abban segit, hogy a ne a fenti feladatban tapasztalt módon kelljen a `Label`-ök és
`Button`-ok helyét meghatároznunk az ablakban. A `Frame`-re a legjobb egyfajta tárolóként, keretként
gondolni, ami tartalmazza a fent leirt widget-jeinket a megfelelő módon összecsoportositva.

Egy ablakon belül tehát lehet több `Frame` is, sőt, ez a lényeg. Igy lehet a különböző widgeteket
egymáshoz rendelni. A legegyszerűbb példa
```python
import tkinter as tk

window = tk.Tk()

frame_a = tk.Frame()
frame_b = tk.Frame()

label_a = tk.Label(master=frame_a, text="I'm in Frame A")
label_a.pack()

label_b = tk.Label(master=frame_b, text="I'm in Frame B")
label_b.pack()

frame_a.pack()
frame_b.pack()

window.mainloop()
```
ahol, bár nem látszik az ablakban és nem is kell, hogy látszódjon, a két `Label` különböző `Frame`-ben
vannak.

*Feladat*: próbáljuk meg kikommentelni az egyik `Frame` `.pack()` függvényét a `.mainloop()` felett.
*Feladat*: próbáljuk megcserélni a két `.pack()` sort.

Mind a négy eddig látott widgetnek van `master` attributuma, amivel hozzá lehet rendelni egy `Frame`-hez.
Egy kicsit lehet a `Frame`-eket szépiteni beépitett effektekkel. Ezek a következők:

| Kód | Hatás |
| -------------- | ------ |
| `tk.FLAT`   | Alapeset |
| `tk.SUNKEN` | Besüllyesztett hatás |
| `tk.RAISED` | Megemelt hatás  |
| `tk.GROOVE` | Nútolt szélek |
| `tk.RIDGE`  | Kiálló szélek |

Az ebben a részben áttekintett widgetek a Tkinter GUI alapegységei, amelyekből felépithetjük az
felületünket.

# Megjelenés beállitásai a Geometry manager-rel

Ebben a fejezetben a `Frame`-ek elhelyezését fogjuk áttekinteni. Az előző részben már találkoztunk egy
`Geomtery manager`-rel, ez volt a `.pack()`, igy ezzel fogjuk kezdeni.

## A `.pack()`

A `.pack()` metódus egy algoritmus ami meghatározott sorrendben elhelyezi a widgeteket a `Frame`-ben
vagy az ablakban. Két fő lépésből áll
1. Kiszámolja mekkora terület kell ahhoz, hogy a widget elférjen, és a fent maradó területet üres
hellyel tölti fel.
2. Elhelyezi a widgetet a terület közepén, hacsak nincs más hely specifikálva. (Ezért került a "Name"
a korábbi példában automatikusan középre.)

Lássuk ezeket egy egyszerű példán:
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=100, height=100, bg="red")
frame1.pack()

frame2 = tk.Frame(master=window, width=50, height=50, bg="white")
frame2.pack()

frame3 = tk.Frame(master=window, width=25, height=25, bg="green")
frame3.pack()

window.mainloop()
```
Ki is lehet tölteni az egész `Frame`-et az X irányba a `fill` kulcsszó argumentummal: `pack(fill=tk.X)`,
s igy nincs értelme megadni a `width` kulcsszót:
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, height=100, bg="red")
frame1.pack(fill=tk.X)

frame2 = tk.Frame(master=window, height=50, bg="white")
frame2.pack(fill=tk.X)

frame3 = tk.Frame(master=window, height=25, bg="green")
frame3.pack(fill=tk.X)

window.mainloop()
```
AAz is beállitható, hogy melyik oldalra kivanjuk igazitani a widgetet a `side` kulcsszó argumentummal.
Négy opció lehetséges:
- `tk.TOP`
- `tk.BOTTOM`
- `tk.LEFT`
- `tk.RIGHT`
Az alapértelmezett a `tk.TOP`. Az alábbi kódban még azt is kikötöttük, hogy Z irányban legyen folytonos
a kitöltés:
```python
import tkinter as tk

window = tk.Tk()

frame1 = tk.Frame(master=window, width=200, height=100, bg="red")
frame1.pack(fill=tk.Y, side=tk.LEFT)

frame2 = tk.Frame(master=window, width=100, bg="white")
frame2.pack(fill=tk.Y, side=tk.LEFT)

frame3 = tk.Frame(master=window, width=50, bg="green")
frame3.pack(fill=tk.Y, side=tk.LEFT)

window.mainloop()
```
*Feladat*: teszteljük, hogy mi történik az ablak átméretezésekor.

## A `.place()`

Ha pontosan szeretnénk megadni, hogy hova kerüljön a widget, akkor a `.place()`-t használjuk.
A következő példán látható a szintaxis
```python
import tkinter as tk

window = tk.Tk()

frame = tk.Frame(master=window, width=150, height=150)
frame.pack()

label1 = tk.Label(master=frame, text="I'm at (0, 0)", bg="red")
label1.place(x=0, y=0)

label2 = tk.Label(master=frame, text="I'm at (75, 75)", bg="green")
label2.place(x=75, y=75)

window.mainloop()
```
A manualitása és bizonyos fokú rendszerfüggősége miatt a `.place()` elég ritkán hasznos.

## A `.grid()`

ha sok widgetünk van, általában hasznos valamilyen négyzetrácsos mintába, gridbe rendezni őket.
A `.grid()` pont erre van, miközben a `.pack()` összes tulajdonságával is bir.
```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack()

window.mainloop()
```
Ez a kódrészlet `Frame`-ek 3x3-as gridjét adja, 1 egységnyi vastag közökkel, kiemelt widgetekkel.
Figyeljük meg, hogy minden `Label` a saját `Frame`-jéhez van rendelve.

Extra helyet hagyhatunk a `Label`-ök között ha `pad`-eket állitunk be.
```python
import tkinter as tk

window = tk.Tk()

for i in range(3):
    window.columnconfigure(i, weight=1, minsize=75)
    window.rowconfigure(i, weight=1, minsize=50)
    for j in range(3):
        frame = tk.Frame(
            master=window,
            relief=tk.RAISED,
            borderwidth=1
        )
        frame.grid(row=i, column=j, padx=5, pady=5)
        label = tk.Label(master=frame, text=f"Row {i}\nColumn {j}")
        label.pack(padx=5, pady=5)

window.mainloop()
```
A `columnconfigure()` és `rowconfigure()` megadja, hogyan viselkedjen a grid az ablak újraméretezésekor.

*Feladat*: Állitgassuk a paramétereket!

Alapértelmezetten widgetek a `grid` cellájuk közepén jelennek meg. Ezt át lehet állitani a `sticky`
kulcsszó segitségével, aminek az értékei az égtájak röviditései.
```python
import tkinter as tk

window = tk.Tk()
window.columnconfigure(0, minsize=250)
window.rowconfigure([0, 1], minsize=100)

label1 = tk.Label(text="A")
label1.grid(row=0, column=0, sticky="ne")

label2 = tk.Label(text="B")
label2.grid(row=1, column=0, sticky="sw")

window.mainloop()
```

Vagyis ami a `.pack()` esetében a `TOP` volt, az itt most `n`.

# Interaktivitás

Eddig láttuk, hogyan kell létrehozni egy ablakot és widgeteket elhelyezni benne. Most nézzük meg,
hogyan lehet ezeket használni. Ez a rész egy kicsit absztrakt, de kidolgozott példa követi a következő
fejezetben.

## Események és kezelésük

Ahogy azt korábban láttuk, ahhoz hogy történjen valami, az `window.mainloop()`-ot meg kell hivnunk.
Ekkor a program figyeli, hogy történik-e valami és ha igen, akkor lefuttatja a kód megfelelő részletét.
Ez a Tkinter része, nem kellett megirnunk, viszont ún. eseménykezelő (event handler) függvényeket
meg kell irnunk. Ez a függvény mindig meg lesz hivva, amikor egy adott esemény bekövetkezik, például
megnyomjuk az egyik billentyűt.

*Feladat*: Mi az esemény definiciója?

## A `.bind()`

A konkrét eseményt egy végrehajtandó utasitáshoz a `.bind()` köti. A szintaxis aránylag egyszerű
```python
import tkinter as tk

window = tk.Tk()

def handle_keypress(event):
    """Print the character associated to the key pressed"""
    print(event.char)

# Bind keypress event to handle_keypress()
window.bind("<Key>", handle_keypress)

window.mainloop()
```
A lenyomott billentyű a terminálban fog megjelenni. De működik egérkattintásra is. Lássunk erre
is egy példát:
```python
import tkinter as tk

window = tk.Tk()

def handle_click(event):
    print("The button was clicked!")

button = tk.Button(text="Click me!")

button.bind("<Button-1>", handle_click)

button.pack()

window.mainloop()
```
Sokféle esemény elképzelhető, ezekről egy lista található [itt](https://web.archive.org/web/20190512164300/http://infohost.nmt.edu/tcc/help/pubs/tkinter/web/event-types.html).

## A `command`

A kattintás esetén a már látott `command` egy egyszerűbb megközelités.

```python
import tkinter as tk


def increase():
    value = int(lbl_value["text"])
    lbl_value["text"] = f"{value + 1}"

def decrease():
    value = int(lbl_value["text"])
    lbl_value["text"] = f"{value - 1}"

window = tk.Tk()

window.rowconfigure(0, minsize=50, weight=1)
window.columnconfigure([0, 1, 2], minsize=50, weight=1)

btn_decrease = tk.Button(master=window, text="-", command=decrease)
btn_decrease.grid(row=0, column=0, sticky="nsew")

lbl_value = tk.Label(master=window, text="0")
lbl_value.grid(row=0, column=1)

btn_increase = tk.Button(master=window, text="+", command=increase)
btn_increase.grid(row=0, column=2, sticky="nsew")

window.mainloop()

```
Ebben a példában először definiáltuk a függvényeket, amiket majd a `Button`-ök fognak hivni a `command`
kulcsszó argumentukon keresztül. Ezek a függvények a `value` értékét növelik vagy csökkentik, amit a
`lbl_value` jelenit meg.

*Feladat*:
- Figyeljük meg a `columnconfigure` használatát!
- Mit jelent a `sticky="nsew"`

# Fahrenheit-Celsius átváltó (példa)

*Feladat*:
- Elemezzük végig, hogy mi történik az alább bemutatott kódban!
- Fejlesszük tovább!
	- Ellenőrizzük, hogy a megadott bemenet szám-e és figyelmeztessük a felhasználót ha nem az!
	- Legyen lehetőség a forditott irányba való átváltásra is.
	- Checkbox beépitése
 	- ...
	
	

```python
import tkinter as tk


def fahrenheit_to_celsius():
    fahrenheit = ent_temperature.get()
    celsius = (5 / 9) * (float(fahrenheit) - 32)
    lbl_result["text"] = f"{round(celsius, 2)} \N{DEGREE CELSIUS}"


window = tk.Tk()

window.title("Temperature Converter")
window.resizable(width=False, height=False)
frm_entry = tk.Frame(master=window)
ent_temperature = tk.Entry(master=frm_entry, width=10)
lbl_temp = tk.Label(master=frm_entry, text="\N{DEGREE FAHRENHEIT}")
ent_temperature.grid(row=0, column=0, sticky="e")
lbl_temp.grid(row=0, column=1, sticky="w")
btn_convert = tk.Button(
    master=window,
    text="\N{RIGHTWARDS BLACK ARROW}",
    command=fahrenheit_to_celsius  # <--- Add this line
)

lbl_result = tk.Label(master=window, text="\N{DEGREE CELSIUS}")
frm_entry.grid(row=0, column=0, padx=10)
btn_convert.grid(row=0, column=1, pady=10)
lbl_result.grid(row=0, column=2, padx=10)

window.mainloop()
```
