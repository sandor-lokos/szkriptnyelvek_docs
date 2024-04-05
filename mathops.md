A Pythonban alapesetben minden karakterlánc string-ként van értelmezve, így a matematikai
operátorok jelentése is bővebb, mint az erősen típusos nyelvekben [1]. Erre láttunk korábban
példát:
```
print("a"*10)
```
A kimenet:
```
> aaaaaaaaaa
```
egy egész szám, a \* pedig a szorzást jelenti.

Matematikában megszoktuk, hogy a szorzás két szám között értelmezett. Aki tanult
absztraktabb matematikát, úgymint a testek, gyűrűk, csoportok és egyebek matematikája, az
tudja, hogy a szorzás egy operáció, amelyet külön definiálni kell és a jelentése nem magától
értetődő. A valós (sőt, igazából a komplex) számok körében a szorzást valamilyen értelemben
az összeadást helyettesíti, vagyis azt jelenti, hogy egy számot hányszor egymás után adjak
össze. (Megfogalmazni is bonyolult a „szorzás” fogalma nélkül.)

Pythonban a szorzás fogalma szintaktikailag kötetlenebb. A számítógép nem tud a mi
matematikánkról, az összeadásról sem, így definiálhatjuk úgy, hogy jelentse az egymás után
leírást kivéve, ha az, amit le kellene írni szám, mert akkor végezze el a matematikai műveletet:
```
print("a"*10)
print(2*10)
```
A kimenet:
```
> aaaaaaaaaa
> 20
```
A fenti leírás kicsit dagályosnak tűnhet, de fontos megérteni, hogy a matematikai operátorok
jellege, éppen mert minden string, eltér az eddig tanultaktól. Vagyis a szorzásról elmondottak
nem csak a szorzásra, hanem a többi alapműveletre is érvényes, bár a szorzás esetén a
legnagyobb a különbség. Természetesen a típusosság ezen a ponton már számíthat. Pl. nincs
értelme a
```
print("aaaa"+10)
```
kifejezésnek, de annak, hogy
```
print("aaaa"+str(10))
```
már van. Az almát a banánnal nem lehet összeadni, de osztani sem. A kivonással is óvatosan
kell bánni:
```
print("aaaa"+"aa")
print("aaaa"-"aa")
```
A kimenet:
```
> aaaaaa
> TypeError: unsupported operand type(s) for -: 'str' and 'str'
```
*Feladat*: próbálgassuk ki, hogy mely alapműveletek milyen típusok között érvényesek!
Kiegészítés az osztáshoz: a Pythonban, ahogy a legtöbb nyelvben háromféle osztás van:
- float típusok között értelmezett
- int típusok között értelmezett
- maradékos osztás
Lássuk a szintaxist:
```
print(10/3)
print(10//3)
print(10%3)
```
A kimenet:
```
> 3.3333333333333335
> 3
> 1
```
*Feladat*: mikor lehet hasznos a második és a harmadik típusú osztás?
Az itt felsoroltakon kívül több, a szintaxist egyszerűsítő jelölés is van. Egy példa erre a növelő
operátor:
```
i=1
i=i+1
print(i)
i+=1
print(i)
i=+1
print(i)
```
A kimenet:
```
> 2
> 3
> 1
```
*Feladat*: magyarázzuk meg az utolsó kimenetet!

Matematikai operációk a logikai állítások is, melyek a vezérlési szerkezetek esetén lesznek
nagyon fontosak [2,3]. Három logikai műveletet értelmezhetünk, melyek a bool algebra részei

- vagy, melyet Pythonban az ```or``` kulcsszó valósít meg
- és, melyet Pythonban az ```and``` kulcsszó valósít meg
- tagadás, melyet Pyhonban a ```not``` kulcsszó valósít meg

Lássunk egy példát:
```
statement = False
if(statement):
	print ("Igaz")
if(not statement):
	print ("Hamis")
```
Egy biztos logikai állítás, ha megengedünk egy állítást, illetve a negáltját (tagadottját) is:

```
statement = False
if(statement or not statement):
	print ("Biztosan igaz!")
if(statement and not statement):
	print ("Sosem igaz!")
```

Utóbbi példában a ```statement``` logikai értéke nem számít. Az első ```if``` mindig teljesül, 
a második soha. Kis kiegészítés az egyenlőségjelekről:
```
i=1
if(i==1):
print("i=1")
```
Az első sor az értékadó egyenlőség, a második az összehasonlító egyenlőség. Ilyen összeadó
operátorok is vannak:
```
i=1
if( i==1 ):
	print("i=1")
if( i != 1 ):
	print("i not equal 1")
if( i > 1 ):
	print("i>1")
if( i < 1 ):
	print("i<1")
if( i <= 1):
	print("i <= 1")
if (i >= 1):
	print("i >= 1")
```
*Megjegyzés*: a fenti, összetett jelek sorrendje nem megcserélhető. Ez biztosítja, hogy
elkerüljünk olyan kellemetlen hibákat, mint az ```i != 1``` és ```i =! 1```.
(Mit is jelent az egyik és a másik? Veszítünk-e funkciót a kötöttséggel?)