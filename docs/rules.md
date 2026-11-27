# Auktionsregler

Vi använder **engelsk auktion**: man budar öppet, och det högsta budet vinner när tiden går ut.
Vi säljer **begagnad elektronik**.

## Användare
- Man registrerar sig med e-post, användarnamn och lösenord.
- E-post och användarnamn måste vara unika.
- Användarnamn: 3–30 tecken, bokstäver, siffror och understreck.
- Lösenord: minst 8 och högst 128 tecken.
- Man loggar in med användarnamn och lösenord.
- E-post visas aldrig för andra användare.

## Roller
- Det finns två roller: användare och admin.
- Admin-konton skapas av oss i seed-skriptet (kolumnen `is_admin`). Det går inte att bli admin via API:et.
- Admin loggar in på samma sätt som andra användare.

## Auktioner
- Alla inloggade användare får skapa auktioner.
- En auktion måste ha namn, beskrivning, startpris, kategori och längd.
- Startpriset väljs av säljaren och måste vara minst 1 kr.
- Längden väljs av säljaren och måste vara 1–7 dagar.
- En ny auktion är **ej startad**. Den startar när säljaren trycker start.
  Då sätts starttiden till "nu" och sluttiden till starttid + längd.
- Bara säljaren kan starta sin auktion, och den kan bara startas en gång.
- Kategorier: Mobiler, Datorer, Ljud, Spel, Kameror, Övrigt.

## Status
| Status     | När                             | Vem ser den        |
|------------|---------------------------------|--------------------|
| Ej startad | Skapad men inte startad         | Säljaren och admin |
| Pågående   | Starttid ≤ nu < sluttid         | Alla               |
| Avslutad   | Nu ≥ sluttid                    | Alla               |
| Avbruten   | En admin har avbrutit auktionen | Säljaren och admin |

## Bud
- Man måste vara inloggad för att buda.
- Man kan bara buda på pågående auktioner.
- Bud som kommer in exakt på sluttiden eller senare nekas.
- Beloppet får ha högst två decimaler och vara högst 1 000 000 kr.
- Första budet måste vara minst lika stort som startpriset.
- Varje nytt bud måste vara minst **20 kr** högre än det högsta budet
  (högsta bud 100 kr → nästa bud minst 120 kr).
- Man kan inte buda om man redan har det högsta budet.
- Man kan inte buda på sin egen auktion.
- Budhistoriken visar bara belopp och tid. Budgivarna är anonyma, även efter avslut.
- Man kan se vilka av buden som är ens egna.

## Samtidiga bud
- Bud på samma auktion behandlas ett i taget. Om två bud kommer samtidigt
  kontrolleras det andra mot det första, så två lika stora bud kan inte uppstå.
- Skulle två bud ändå vara lika stora vinner det som sparades först.

## Vinnare
- Det högsta budet när tiden har gått ut vinner, och vinnaren betalar sitt eget bud.
- Om det bara finns ett bud vinner det budet.
- Om auktionen saknar bud finns det ingen vinnare.
- När auktionen är avslutad ser alla att den är avslutad och slutpriset.
- Vinnarens användarnamn visas bara för säljaren (och admin).
- Vinnaren ser själv att hen har vunnit, i listan över auktioner hen har budat på.
- En avbruten auktion har ingen vinnare.

## Admin
- Admin ser alla auktioner i alla statusar.
- Admin kan avbryta en auktion som är ej startad eller pågående.
  En avslutad auktion kan inte avbrytas.
- Buden på en avbruten auktion sparas men ger ingen vinnare.

## Statuskoder
| Situation                                                                         | Kod |
|-----------------------------------------------------------------------------------|-----|
| Inte inloggad                                                                     | 401 |
| Inloggad men saknar behörighet (inte admin, inte säljaren, bud på egen auktion)   | 403 |
| Data bryter mot en regel (för lågt bud, avslutad auktion, ogiltig längd)          | 400 |
| Auktionen eller användaren finns inte                                             | 404 |
| E-post eller användarnamn finns redan                                             | 409 |

## Möjliga förbättringar
- Planerat startdatum, så att säljaren kan välja när auktionen ska starta.
