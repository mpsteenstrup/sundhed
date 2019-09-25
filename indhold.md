# Introduktion

Gennem de sidste år er registrering af personlige data blevet mere og
mere udbredt. Det er ikke længere kun topatleter som måler sig selv, men
i lige så høj grad motionister og folk til dagligt. Fokus på data fra
kroppen kan være med til at motivere til et sundere og mere aktivt liv,
men har også mulighed for at stresse. Vi vil i dette projekt se på
hvordan man måler på kroppen. Det vil vi gøre ved at programmere
microbit microcrontrollere.

# noter

  - bliver programmeret i python, med editoren mu,
    [Download](https://codewith.mu/en/download).

  - bagpå er den en restart knap, nogen gange skal man resterte når
    microbitten er blever flashed.

  - for at plotte data skal det være en tuple, dvs. en prentes med
    minimum to værdier, eks. (23, 2010)

  - Online editor, <https://python.microbit.org/v/1.1>.

  - Introduktion, [microbit.org](https://microbit.org/guide/python/)

# Getting startet

Vi skal i gang og det første er at lege lidt med dimsen, eller
mikrocontroleren som det jo er. Vi bruger introduktionen med linket
ovenfor og online editoren.

undersøg jeres microbit

  - Vælg <span class="upright">view the Hello World section</span> og
    kopier kodestumper ind i online editoren.

  - Download jeres program, .hex fil og overfør den til jeres microbit,
    drag and drop style.

  - hvis det ikke virker umiddelbart så restart med kappen bagpå.

# Skridttæller

Vi vil bruge vores microbit til at tælle skridt. Vi bryder processen ned
i følgende skridt, hø hø.

1.  lav en variabel hvor vi gemmer antallet

2.  mål accelerationen

3.  bestem hvornår et skridt er taget

4.  opdater variablen med +1

## ad. 1 og 4

Følgende kode laver variablen skridt og addere en når A bliver trykket.

    from microbit import *
    skridt = 0
    while True:
        if button_a.get_presses():
            skridt += 1
            sleep(100)
        display.show(skridt)

optælling

  - skriv koden ind i editoren, vær opmærksom på rigtigt indryk
    (tabukator eller to mellemrum).

  - test koden, gør den som I forventer?

  - find noget at lav om.

  ## ad. 2

Vores mikrobit kan måle accelerationen nemt.

    from microbit import *
    while True:
        sleep(20)
        t = accelerometer.get_values()
        print(t)

acceleration

  - Skriv koden ind og vælg knappen, Plotter, hvad ser I?

  - Undersøg hvad der er op og ned af de tre akser x, y, z.

  - vælg <span class="upright">`t = accelerometer.get_x()`</span>

  - tryk på <span class="upright">ctrl-c</span> for at stoppe programmet
    og vælg <span class="upright">REPL</span>, giver en konsol hvor man
    kan markere og kopiere.

  - Kopier noget ind i logger pro og lav en <span class="upright">new
    manual column \(\rightarrow\) Generate values</span>, x-aksen.

## ad 3

vi skal nu bestemme hvornår i har taget et skridt. Koden nedenfor tæller
hver gang man flipper microbitten.

    from microbit import *
    skridt = 0
    while True:
        sleep(20)
        t = accelerometer.get_x()
        if t>200:
            skridt +=1
            sleep(1000)
            print(skridt)

skridt

  - beskriv hvad \(t>200\) betingelsen gør, og prøv at lav om på den.

  - gør det samme med sleep(1000).

## Rigtige skridt

I har nu delelementerne til at lave en rigtig skridttæller. Der er en
del parametre som skal tilpasses og noget kode som skal skrives.

skridt

  - Brug graf plotteren til at undersøg accelerationen ved rigtig
    bevægelse.

  - udvælg en variabel og en værdi for hvornår der er taget et skridt.

  - implementer det i et samlet program som kan tælle skridt.

  - ud og test om jeres program faktisk måler rigtigt.

# Puls måler

Her skal vi gøre næsten det samme, følg linket for en introduktion,
[LINK](https://pulsesensor.com/pages/micro-bit-fun).

$\pi = 3.141$
