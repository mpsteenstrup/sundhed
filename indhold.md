## Introduktion

Gennem de sidste år er registrering af personlige data blevet mere og mere udbredt.
Det er ikke længere kun topatleter som måler sig selv, men i lige så høj grad motionister og folk til dagligt. Fokus på data fra kroppen kan være med til at motivere til et sundere og mere aktivt liv, men har også mulighed for at stresse. Vi vil i dette projekt se på hvordan man måler på kroppen. Det vil vi gøre ved at programmere microbit microcrontrollere.


´´´
from microbit import *
skridt = 0
while True:
    if button_a.get_presses():
        skridt += 1
        sleep(100)
    display.show(skridt)
´´´
