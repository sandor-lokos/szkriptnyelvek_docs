Ebben a fejezetben az `openpyxl` modul egy-két lehetőségét nézzük meg. Ez a modul teszi lehetővé, hogy
Excel fájlokkal dolgozzunk Python szkriptekből.

# Excelfájl létrehozása, alapműveletek

## Létrehozás, cella értékadás

Kezdjük azzal, hogy importáljuk a modult és példányositunk egy objektumot.
```python
from os import getcwd
import openpyxl as pyxl

workbook = pyxl.Workbook()  ## Peldanyositas
sheet = workbook.active

sheet["A1"] = "Hello"
sheet["B1"] = "World"

for i in range(2, 10, 1):
    sheet.cell(row=i, column=1).value = i*"*"

sheet.cell(row=5, column=2).value = "Csillagok"

save_path = getcwd() + "/hello_world.xlsx"
workbook.save(filename=save_path)
```
Suba alatt használtunk egy másik modult is, az `os`-t, ami az operációs rendszerben végzett műveleteket
tartalmazza. Nem fogunk ezzel részletesebben foglalkozni, elég egyszerű feldolgozni, igy az olvasóra bizzuk
ezt. A [hivatalos dokumentációban](https://docs.python.org/3/library/os.html) elérhető az összes függvény.

A fenti kódrészletben tehát beimportáltuk az `openpyxl` modult mint `pyxl`. Példányositottunk egy munkauzetet
és aktiváltunk egy munkalapt (sheet). Majd az `A1` és `B1` cellákba beirtunk értékeket.

Aztán egy `for` ciklussal is irtunk értékeket cellába oszlopként és sorként hivatkozva rájuk a `value`
tagváltozón keresztül, végül pedig lementettük az Excelünket a `getcwd()` függvény segitségével, ami az
aktuális munkakönyvtár (get current working directory) elérési útját tériti vissza.

*Feladat*: készitsük el a 15x15-ös szorzótáblát!

## Betöltés és ábrázolás

Természetesen nem csak létrehozni, hanem beolvasni is tudunk Excel-eket. Ezt a `load_workbook()` segitségével
tudjuk megtenni. Ezután ugyanúgy tudunk hivatkozni a cellákra, azok értékeire, mint a fenti példában.

Használhatjuk továbbá az Excel beépitett ábrázoló eszközeit. Ezek az `openpyxl.chart`-ból elérhetőek.

Lássunk egy példát, amelyben beolvasunk egy Excel fájt, aminek két lapja is van. Az adatokat, amelyeket a
lapokon találunk, ábrázoljuk. Az Excel fájl itt elérhető.

```python
import openpyxl as pyxl
from openpyxl.chart import LineChart, BarChart, Reference
#from openpyxl.utils import FORMULAE

workbook = pyxl.load_workbook(filename="minta.xlsx")
sheet = workbook.worksheets[1]

sheet["B1"] = "=AVERAGE(A1:A200)"
sheet["B2"] = "=MAX(A1:A200)"

bar_chart = BarChart()
data = Reference(worksheet=sheet, min_row=1,max_row=201,min_col=1,max_col=1)
bar_chart.add_data(data, titles_from_data=False)
sheet.add_chart(bar_chart, "C1")

line_chart = LineChart()
data = Reference(worksheet=sheet, min_row=1,max_row=201,min_col=1,max_col=1)
line_chart.add_data(data,titles_from_data=False)
sheet.add_chart(line_chart,"C20")

workbook.save("minta.xlsx")
```



