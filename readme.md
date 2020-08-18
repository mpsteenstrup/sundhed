Introduktion
============

Gennem de sidste år er registrering af personlige data blevet mere og
mere udbredt. Det er ikke længere kun topatleter som måler sig selv, men
i lige så høj grad motionister og folk til dagligt. Fokus på data fra
kroppen kan være med til at motivere til et sundere og mere aktivt liv,
men har også mulighed for at stresse. Vi vil i dette projekt se på
hvordan man måler på kroppen. Det vil vi gøre ved at programmere
microbit microcrontrollere.

Materialer
----------

-   microbit, gerne med fumlebræt.

-   Puls måler,
    [LINK](https://arduinotech.dk/shop/pulse-sensor-heart-rate-sensor-arduino-raspberry-pi/),
    de er desværre ret skrøbelige i lodningerne.

noter
=====

-   bliver programmeret i python, med editoren **mu**,
    [Download](https://codewith.mu/en/download).

-   bagpå er den en restart knap, nogen gange skal man resterte når
    microbitten er blever flashed.

-   for at plotte data skal det være en tuple, dvs. en prentes med
    minimum to værdier, eks. (23, 2010)

-   Online editor, <https://python.microbit.org/v/1.1>.

-   Dokumentation, [microbit.org](https://microbit.org/guide/python/)

Getting startet
===============

Vi skal i gang og det første er at lege lidt med dimsen, eller
mikrocontroleren som det jo er. Vi bruger dokumentationen med linket
ovenfor og online editoren.

undersøg jeres microbit

-   Vælg og kopier kodestumper ind i online editoren.

-   Download jeres program, .hex fil og overfør den til jeres microbit,
    drag and drop style.

-   hvis det ikke virker umiddelbart så restart med kappen bagpå.

Skridttæller
============

Vi vil bruge vores microbit til at tælle skridt. Vi bryder processen ned
i følgende skridt.

1.  lav en variabel hvor vi gemmer antallet

2.  opdater variablen med +1.

3.  mål accelerationen.

4.  bestem hvornår et skridt er taget.

Lav variabel og opdater den.
----------------------------

Vi vil gerne have styr på hvoran man laver en variabel og hvordan man
opdaterer værdien. Vi skal senere bruge den til at gemme antallet af
skridt. Følgende kode laver variablen skridt og addere en når knap A
bliver trykket.
```
from microbit import *
skridt = 0
while True:
    if button_a.get_presses():
        skridt += 1
        sleep(100)
    display.show(skridt)
```
optælling

-   skriv koden ind i editoren, vær opmærksom på rigtigt indryk
    (tabukator eller to mellemrum).

-   test koden, gør den som I forventer?

-   gennemgå kode, hvad gør de forskellige linjer.

-   Få microbitten til at tælle ned når knap B bliver trykket ned.

Måling af acceleration
----------------------

Vores mikrobit kan måle accelerationen nemt.
```
from microbit import *
while True:
    sleep(20)
    acc = accelerometer.get_values()
    print(acc)
```
acceleration

-   Skriv koden ind og vælg knappen, Plotter, hvad ser I?

-   Undersøg hvad der er op og ned af de tre akser x, y, z. (
    accelerationen er positiv ned når microbitten står stille.)

absolutte acceleration
----------------------

med får vi accelerationen i x,y,z retningen samtidigt. Hvis vi vil have
de enkelt kan vi eks få får vi x accelerationen. Accelerationen i x,y,z
giver en samlet acceleration som er en vektor i 3 dimensioner. Hvis vi
skal have et tal, en skalar, til vores trigger kan vi beregne længden af
denne vektor. Det gør I som I har lært i to dimensioner med brug af
pythagoras,
<img src="https://latex.codecogs.com/svg.latex?;
a = \sqrt{x^2+y^2+z^2}
" /> Hvis microbitten skal forstå de
skal I lave en variabel

<img src="https://render.githubusercontent.com/render/math?math=a^2 =x^2+y^2+z^2">

```
acc = (x**2+y**2+z**2)**0.5,
```

da ** er syntaksen for opløftet i og kvadratroden netop er at opløfte
i en halv.

Triggerværdi
------------

Vi skal nu bestemme hvornår i har taget et skridt. Koden nedenfor tæller
hver gang man flipper microbitten.
```
from microbit import *
skridt = 0
while True:
    sleep(20)
    x = accelerometer.get_x()
    if x>200:
        skridt +=1
        sleep(1000)
        print(skridt)
```

skridt

-   beskriv hvad x>200 betingelsen gør, og prøv at lav om på den.

-   gør det samme med sleep(1000).

 mu plotter og trigger værdi
----------------------------

Når I skal bruge accelerationen som triggerværdi og gerne vil bruge
plotter funktionen i mu editoren rammer I ind i problemer.

-   Plotter godtager kun tupler, dvs. minimim to værdier, eks. (22, 47).

-   Når I vil finde en værdi til at trigger på skal I bruge én værdi.

En løsning kan være
```
acc = (x**2+y**2+z**2)**0.5, ) # nu er acc en tuple og kan plottes
for acc[0]>500: # her vælger vi første værdi i acc tuplen.
                # I programmering tæller vi fra 0.
```

Rigtige skridt
--------------

I har nu delelementerne til at lave en rigtig skridttæller. Der er en
del parametre som skal tilpasses og noget kode som skal skrives.

skridt

-   brug graf plotteren til at undersøg accelerationen ved rigtig
    bevægelse.

-   udvælg en variabel og en værdi for hvornår der er taget et skridt.

-   implementer det i et samlet program som kan tælle skridt.

-   ud og test om jeres program faktisk måler rigtigt.

Puls måler
==========

Her skal vi gøre næsten det samme, følg linket for en introduktion,
[LINK](https://pulsesensor.com/pages/micro-bit-fun). I kan ikke bruge
koden som er vist på siden, det er JavaScript og ikke Python kode.

simpelt kredsløb/kode
---------------------

Her er en simpel kode til udlæsning af pulsmåleren, ved brug af Pin0,
```
from microbit import *
while True:
    sleep(20)
    signal = pin0.read_analog()
    y = (signal, )
    print(y)
```
Glidende gennemsnit
-------------------

Pulsmåleren giver meget forskellige værdier alt efter hvordan man holder
den. Vi har brug for at fjerne disse uønskede niveauhop. Vi kan fjerne
den ned et glidende gennemsnit her gennemsnittet over de sidste 100
datapunkter.
```
    from microbit import *
    i = 0
    n = 100
    l = [0]*n
    while True:
        sleep(20)
        signal = pin0.read_analog()
        l[i % n] = signal
        y = (signal - sum(l)/n, )
        i +=1
        print(y)
```

## Glidende gennemsnit

-   tape puls sensoren fast så den ikke rykker sig.

-   undersøg forskellige værdier af . Hvad sker der hvis i gør meget
    stor eller meget lille.

-   bestem et optimalt for jeres sensor.

### Det bankende hjerte

I har nu et signal som I kan bruge som I brugte accelerationen ved
skridttælleren. Hvis I vil have pulsen i pulslag per minut skal I tælle
op og dividere med tiden. Her skal I tilbage i dokumentationen for at
finde biblioteket *utime*. I kan også få hjertet til at slå på
microbitten ved at sætte et billede ind i et tidsinterval ved hvert
pulsslag. Der er generelt fri og rig mulighed for at prøve ting af.
