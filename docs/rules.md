# Auktionsregler

Vi använder **engelsk auktion**: man budar öppet, och det högsta budet vinner när tiden går ut.
Vi säljer **begagnad elektronik**.

## Användare
- Man registrerar sig med e-post och lösenord.
- Samma e-post kan bara registreras en gång.
- Man loggar in med e-post och lösenord.

## Auktioner
- Alla inloggade användare får skapa auktioner.
- En auktion måste ha namn, beskrivning, startpris, sluttid och kategori.
- Startpriset måste vara minst 1 kr.
- Sluttiden måste ligga i framtiden.
- Kategorier: Mobiler, Datorer, Ljud, Spel, Kameror, Övrigt.

## Bud
- Man måste vara inloggad för att buda.
- Alla kan se det högsta budet medan auktionen pågår.
- Budgivarna är anonyma. Budhistoriken visar bara belopp och tid, aldrig vem som har budat.
- Man kan se vilka av buden som är ens egna.
- Ett bud måste vara större än 0 kr.
- Första budet måste vara minst lika stort som startpriset.
- Varje nytt bud måste vara minst 10 kr högre än det högsta budet.
- Man kan buda igen om någon annan har bjudit över en.
- Man kan inte buda om man redan har det högsta budet.
- Man kan inte buda på sin egen auktion.
- Bud som kommer in exakt på sluttiden eller senare nekas.

## Vinnare
- Högsta budet när tiden har gått ut vinner.
- Vinnaren betalar sitt eget bud.
- Om två bud är lika stora vinner det som kom först.
- Om auktionen inte har några bud finns det ingen vinnare.
- Efter att auktionen är avslutad visas vem som vann.

## Behörighet
- Alla, även de som inte är inloggade, får se auktioner och budhistorik (utan namn).
- Bara en admin får avbryta en auktion.
- En avbruten auktion har ingen vinnare.
