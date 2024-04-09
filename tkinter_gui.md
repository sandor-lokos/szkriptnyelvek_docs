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

## Widgetek

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



