# Zadatak - Olimpijske igre

- Napisati JavaScript / C# program za simulaciju košarkaškog turnira na Olimpijskim igrama.
Biće potrebno da simulirate grupnu fazu i eliminacionu fazu turnira.
- Zadatak je potrebno uraditi koristeći isključivo JavaScript / C#, bez upotrebe eksternih paketa.
- Zadatak se pokreće komandom: `npm start` / `dotnet run` i zatim u std output-u prikazuje simulaciju turnira.
- Ukoliko zadatak radiš u JavaScript-u koristi `node v20.17.0`, a ukoliko ga radiš u C#-u koristi `.NET 8`.

Opis zahteva dat je u daljem tekstu.

## Grupna faza
Grupe i timovi su dati u `groups.json` fajlu u sklopu git repozitorijuma zadatka. Date su informacije o imenu zemlje, ISO-3166 kodovi i FIBA rang pre početka Olimpijskih igara.

Potrebno je simulirati rezultat svih utakmica grupne faze i konačno timove u okviru grupe rangirati po propozicijama takmičenja.
Rezultate utakmica odrediti tako da verovatnoća pobede i poraza tima bude u korelaciji sa razlikom u njihovim pozicijama na FIBA rang listi.

### Pravila grupne faze su:
1. Grupna faza se sastoji od toga da svaki tim igra sa preostala tri tima iz svoje grupe. Timovi dobijaju:
   - 2 boda za pobedu,
   - 1 bod za poraz,
   - 0 bodova za poraz predajom.
2. Timovi u okviru grupe se rangiraju na osnovu broja bodova.
U slučaju da dva tima iz iste grupe imaju isti broj bodova, rezultat međusobnog susreta će biti korišćen kao kriterijum za rangiranje.
U slučaju da 3 tima iz iste grupe imaju isti broj bodova, kriterijum za rangiranje biće razlika u poenima u međusobnim utakmicama između ta 3 tima (takozvano formiranje kruga).
3. Na kraju grupne faze prvoplasirani, drugoplasirani i trećeplasirani timovi iz svih grupa dobijaju rang od 1 do 9:
   - Prvoplasirani timovi iz grupa A, B i C se medjusobno rangiraju po primarno po broju bodova, zatim koš razlici (u slučaju jednakog broja bodova) i zatim broja postignutih koševa (u slučaju jednakog broja bodova i koš razlike) kako bi im se dodelili rangovi 1, 2 i 3.
   - Drugoplasirani timovi iz grupa A, B i C se medjusobno rangiraju istom principu kako bi im se dodelili rangovi  4, 5 i 6.
   - Trećeplasirani timovi iz grupa A, B i C se medjusobno rangiraju po istom principu kako bi im se dodelili rangovi  7, 8 i 9.
4. Ekipe sa rangom od 1 do 8 prolaze u eliminacionu fazu, ekipa sa rangom 9 ne nastavlja takmičenje.

### U output-u prikazati ishode svih utakmica grupne faze po kolima, zatim rangiranja po grupama i kojih 8 ekipa je prošlo dalje.

Primer output-a (vaš prikaz može biti drugačije formatiran, to nije presudno):
```
Grupna faza - I kolo:
    Grupa A:
        Kanada - Grška (85:79)
        Australija - Španija (92:80)
    Grupa B:
        Nemačka - Japan (97:77)
        Francuska - Brazil (78:66)
    ...

Konačan plasman u grupama:
    Grupa A (Ime - pobede/porazi/bodovi/postignuti koševi/primljeni koševi/koš razlika)::
        1. Kanada      3 / 0 / 6 / 267 / 247 / +20
        2. Australija  2 / 1 / 4 / 246 / 250 / -4
        3. Grčka       2 / 1 / 4 / 233 / 241 / -8
        4. Španija     2 / 1 / 4 / 249 / 257 / -8
    ...
```

## Žreb
Timovi koji su se kvalifikovali u četvrtfinale biće podeljeni u četiri šešira:
   - Šešir D: Timovi sa rangom 1 i 2.
   - Šešir E: Timovi sa rangom 3 i 4.
   - Šešir F: Timovi sa rangom 5 i 6.
   - Šešir G: Timovi sa rangom 7 i 8.

Timovi iz šešira `D` se nasumično ukrštaju sa timovima iz šešira `G`, a timovi iz šešira `E` sa timovima iz šešira `F` i tako se formiraju parovi četvrtfinala. Veoma važna propozicija je da se timovi koji su igrali međusobno u grupnoj fazi, ne mogu sresti u četvrtfinalu.

U istom trenutku se formiraju i parovi polufinala, nasumičnim ukrštanjem novonastalih parova četvrtfinala, uz pravilo da se parovi nastali ukrštanjem šešira `D i E` ukrštaju sa parovima nastalim ukrštanjem šešira `F i G`.

### Nakon žreba prikazati timove po šeširima i konačni kostur eliminacione faze.

Primer output-a:
```
Šeširi:
    Šešir D
        Nemačka
        SAD
    Šešir E
        Srbija
        Kanada
    Šešir F
        Francuska
        Australija
    Šešir G
        Brazil
        Grčka

Eliminaciona faza:
    Francuska - Kanada
    Nemačka - Grčka

    SAD - Brazil
    Srbija - Australija

```

## Eliminaciona faza
Turnir se nastavlja standardnim formatom eliminacije, gde pobednici prolaze u polufinale, a gubitnici ispadaju. Pobednici polufinala idu u finale, dok gubitnici igraju za bronzanu medalju.

### Prikazati sve mečeve eliminacione faze po rundama (četvrtfinale, polufinale, utakmica za 3. mesto, finale). Nakon toga prikazati timove koji su osvojili medalje.

Primer output-a:
```
Četvrtfinale:
    Francuska - Kanada (82: 73)
    Nemačka - Grčka (76: 63)

    SAD - Brazil (122: 87)
    Srbija - Australija (95: 90)


Polufinale:
    Francuska - Nemačka (73: 69)
    SAD - Srbija (95: 91)


Utakmica za treće mesto:
    Nemačka - Srbija (83: 93)


Finale:
    Francuska - SAD (87: 98)


Medalje:
    1. SAD
    2. Francuska
    3. Srbija
```

## Bonus

Kod određivanja verovatnoće pobednika uzeti u obzir i formu ekipe.
Početna tačka za ovu kalkulaciju mogu biti podaci iz fajla `exibitions.json` u kome su dati rezultati 2 prijateljske utakmice za svaku ekipu.
Formu prera;unavati kako turnir odmiče, a možete kao faktor forme uključiti i jačinu protivnika i razliku koju je ekipa ostvarila.