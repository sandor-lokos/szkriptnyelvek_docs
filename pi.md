Az alábbiakban egy olyan kódot fogunk végig elemezni, amely a &pi értékét számitja ki egy közelitő formula
segitségével. Ez a [Chudnovsky-algoritmus](https://en.wikipedia.org/wiki/Chudnovsky_algorithm), de megnézzük
a [Ramanujan--Sato-algoritmust](https://en.wikipedia.org/wiki/Ramanujan%E2%80%93Sato_series) is. Épp ez lesz
a lényeg: mindkét közelitő formula olyan matematikai eszközöket kiván, amelyek iskertek lehetnek, de függvényeket
kell hozzá implementálni. Vagyis tipikus esete ez az öröklődésnek. Aztán össze is hasonlitjuk az eredményeket,
amihez pedig egy olyan függvényt használunk, ami nem része egy osztálynak sem.

Nézzük meg, hogy mi hogyan van implementálva. Ha valakit érdekel a &pi generálás, nézze meg ezt a
[weboldalt](http://www.numberworld.org/y-cruncher/news/2024.html#2024_3_13).

Jöjjön a kód:
```python
import numpy as np


class methods:
    def __init__(self):
        pass
    def sumInt(self, a, b, expression ):
        res = 0
        for i in range(a,b,1):
            res += expression(i)
        return res

    def prodInt(self,a, b):
        i = a
        while i < b:
            a *= i+1
            i = i+1
        return a
    def factorial(self, a):
        return self.prodInt(1, a)


class ChudnovskysPi(methods):
    def __init__(self, acc):
        self.acc = acc

    def pifunc(self, x):
        return (((-1) ** x) * self.factorial(6 * x) * (545140134 * x + 13591409)
                / (self.factorial(3 * x) * self.factorial(x) ** 3 * (640320) ** (3 * x + 1.5)))


    def ownPi(self):
        RecPi = np.longdouble(self.sumInt(0, self.acc, self.pifunc))
        return np.longdouble(1./(12*RecPi))


class RamanujansPi(methods):
    def __init__(self, acc):
        self.acc = acc
    def pifunc(self, x):
        return self.factorial(4*x)*(26390*x+1103) / (self.factorial(x)**4 * 396**(4*x))


    def ownPi(self):
        RecPi = np.longdouble(self.sumInt(0, self.acc, self.pifunc))
        return np.longdouble(99**2/(2*np.sqrt(2)*RecPi))



def compare(a, b):
    return 1-round(np.log10(abs(a-b)))

calc_pi = ChudnovskysPi(2)
another_pi = RamanujansPi(3)

print(f'pi of NumPy = {np.pi}')
print(f'pi of Chudnovsky\'s algorithm = {calc_pi.ownPi()}')
print(f'pi of Ramanujan\'s algorithm = {another_pi.ownPi()}')
```