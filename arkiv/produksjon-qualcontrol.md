---
layout: default
title: "qualcontrol"
parent: "Produksjon"
nav_order: 3
---

[qualcontrol](https://github.com/helseprofil/qualcontrol) er en R-pakke som inneholder funksjoner for å gjennomføre kvalitetskontrollen av publikasjonsklare datafiler.

Brukerfiler: - qualcontrol/1. Kvalitetskontrollrutiner - kontroll av enkeltfiler - qualcontrol/2. Friskvik og barometersjekk - kontroll av godkjente friskvikfiler

For å bruke khfunctions åpner du produksjonsprosjektet og går til filen `qualcontrol/1. Kvalitetskontrollrutiner.Rmd`. Denne inneholder en strømlinjeformet oversikt over kvalitetskontrollrutinene og følges nedover. Resultater vil lagres i `PRODUKSJON/VALIDERING/QualControl/**PRODUKSJONSÅR**/**KUBENAVN**`

# Forarbeid

-   For å få tilgang til funksjonene må første kodeblokk med `library(qualcontrol)` kjøres.
-   Du kan endre produksjonsåret med funksjonen `update_qcyear()`. Dette bestemmer hvilken mappe resultatfilene vil publiseres i.

# Kvalitetskontrollrutiner

De ulike stegene dokumenteres i KUBESTATUS-tabellen i KHELSA.mdb.

## 1. Grovsjekk

-   Last inn ny (og gammel/forrige publiserte) datafil med funksjonen `readfiles()`, og formatter filene med funksjonen `make_comparecube()`. Dette vil også produsere noen .csv-filer som lagres i mappen `FILDUMPER`. \## 1. Deskriptiv grovsjekk
-   Her sjekkes hva som finnes i filen, f.eks. hvilke kolonner, hvilke nivåer i dimensjonene
-   Tidsserier på landsnivå plottes for all dimensjoner for å fange opp eventuell feilklassifisering.

## 2. Batch vs Batch

-   Sammenligning mot forrige publiserte fil
-   Oppsummering av antallet identiske/ulike rader og hvor store forskjellene er
-   Antallet forskjellige rader og summen av disse, totalt og per årgang
-   Plott av forskjellene over tid, for å se om forskjellene er stabile eller endrer seg over tid

## 3. Prikking

-   Er det noen tall under grensen for personvernskjuling?
-   Sammenligning av antall skjulte tall, totalt og per årgang
-   Sammenligning av antall tidsserier med 0-maks antall skjulte tall

## 4. Sjekk aggregering

-   Sjekke at lavere geografisk nivå summerer seg opp til høyere, f.eks. at kommuner summerer seg til fylke.
-   Sjekke andelen ukjent bydel
-   Plotte tidsserier for bydelene, og vektede bydelstall mot kommunetallet.

## 5. Ekstremverdier

-   Genererer boksplott og tidsserieplott som markerer ekstremverdier, definert som verdier utenfor intervallet definert av vektet 25.percentil - 1.5 \* IQR og vektet 75.percentil + 1.5 IQR.
-   Disse vurderes for om de kan være riktige.

## 6. Ekstremverdier, år-til-år

-   Samme som over, men for relativ endring fra forrige årgang. Kan fange opp usannsynlig store endringer fra et år til et annet.

# 2. Friskvik og barometersjekk

Inneholder to funksjoner, en som sjekker alle friskvikfilene i nyeste godkjentmappe, og en som sjekker om like verdier får farget prikk i barometeret. Disse brukes i forbindelse med profilproduksjonen.

## Tolkning av output fra friskviksjekk

`CheckFriskvik()` genererer en csv-fil som lagres i mappen `PRODUKSJON/VALIDERING/FRISKVIK_vs_KUBE/profilår`. Denne inneholder følgende kolonner:

-   **Friskvik**: Navn på friskvikfilen
-   **Kube**: Kube med samme datotag (som friskvik er hentet fra). Denne er hentet fra DATERT-mappen
-   **File_in_NESSTAR**: Er det denne kuben som er lagt i NESSTAR-mappen (som publiseres i statistikkbanken).
-   **FRISKVIK_ETAB**: Hva står i ETAB-kolonnen i friskviktabellen
-   **KUBE_KJONN**: Hvilket strata er hentet ut
-   **KUBE_ALDER**: Hvilket strata er hentet ut
-   **KUBE_UTDANN**: Hvilket strata er hentet ut
-   **KUBE_INNVKAT**: Hvilket strata er hentet ut
-   **KUBE_LANDBAK**: Hvilket strata er hentet ut
-   **FRISKVIK_YEAR**: Hvilke år finnes i friskvikfilen
-   **Last_year**: Er siste år i Friskvikfilen lik siste året i kubefilen? Normalt skal nyeste årgang slices ut.
-   **Periode_bm**: Hentet fra FRISKVIK-tabellen i ACCESS, år i barometerfiguren
-   **Periode_nn**: Hentet fra FRISKVIK-tabellen i ACCESS, år i fotnotene under barometerfigur
-   **Identical_prikk**: Sjekker at prikking er lik i friskvikfilen og i kuben, for å sikre at ikke noen får tall i profilene som er prikket i statistikkbanken eller motsatt.
-   **Matching_kubecol**: Hvilken kolonne i kuben er det som matcher med tallene som vises i friskvik
-   **Different_kubecol**: Hvilke kolonner i kuben matcher IKKE med det som vises i friskvik
-   **Enhet**: Hentet fra FRISKVIK-tabellen i ACCESS, hvilken enhet står i barometeret.
-   **REFVERDI_VP**: Hentet fra SPEC-filen som ble generert ved kubekjøring, hvordan var filen standardisert.
-   **VALID**: Dersom enheten indikerer at filen er standardisert må den faktisk være standardisert, og det må være MEIS som vises i friskvik. Dersom dette er konsistent, er kombinasjonen valid, og dette indikeres her.

### Hva skjer i bakgrunnen

`CheckFriskvik()` tar utgangspunkt i nyeste godkjentmappe med friskvikfiler. For hver av filene i denne mappen leter den i DATERT-mappene for kommune- og norgeshelsa etter en kubefil med samme datotag. Dersom flere kubefiler med samme datotag eksisterer, finnes den korrekte filen ved å sjekke i FRISKVIK-tabellen i ACCESS etter korrekt kubenavn. Den korresponderende SPEC-filen som ble generert ved kubekjøring leses også inn.

Kubefilen filtreres basert på ETAB-kolonnen i friskvikfilen, i tillegg til alle felles kolonner med unntak av år. Den filtrerte kubefilen inneholder dermed det samme strataet som er slicet ut i friskvikfilen, men samtlige årganger.

Friskvikfilen og den filtrerte kubefilen brukes som input i de ulike funksjonene som gjennomfører hver enkelt test. Resultatet av alle testene resulterer i en linje i outputfilen.

### Filer som ikke lar seg sjekke

For noen friskvikfiler er det ikke mulig å identifisere en korresponderende kubefil. Dette gjelder friskvikfiler generert utenfor løypen, som f.eks. forventet levealder som er basert på flere separate kubefiler. Disse filene vil gå en tom rad i outputfilen.
