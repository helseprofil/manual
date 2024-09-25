---
layout: default
title: "Friskviksjekk" 
parent: "KHvalitetskontroll (arkiv)"
nav_order: 4
---

Brukerfilen finner du i hovedmappen til prosjektet/USER/Friskviksjekk.Rmd
Funksjonene ligger i [R/functions_friskvik.R](https://github.com/helseprofil/KHvalitetskontroll/blob/main/R/functions_friskvik.R)

# Hensikt med sjekken
Når vi har laget en godkjentmappe er det en del ting som bør sjekkes for å sikre at riktige parametre er hentet ut og at tallene stemmer overens med det som publiseres i statistikkbanken.

# Hvordan gjennomføre sjekken
Komplett sjekk gjennomføres for nyeste godkjentmappe for folkehelse- (FHP) eller oppvekstprofiler (OVP), for bydel (B), kommune (K) og Fylke (F). Sjekken gjennomføres ved funksjonen `CheckFriskvik()`. Argumentene som må defineres er profile ("FHP"/"OVP"), geolevel ("B"/"K"/"F") og profilår. For å sjekke siste godkjentmappe for folkehelseprofilene for kommune, ville man brukt følgende kode:

```R
CheckFriskvik(profile = "FHP",
              geolevel = "K",
              profileyear = 2024)
```

# Tolkning av output
`CheckFriskvik()` genererer en csv-fil som lagres i mappen `PRODUKSJON/VALIDERING/FRISKVIK_vs_KUBE/profilår`. Denne inneholder følgende kolonner:

- **Friskvik**: Navn på friskvikfilen
- **Kube**: Kube med samme datotag (som friskvik er hentet fra). Denne er hentet fra DATERT-mappen
- **File_in_NESSTAR**: Er det denne kuben som er lagt i NESSTAR-mappen (som publiseres i statistikkbanken). 
- **FRISKVIK_ETAB**: Hva står i ETAB-kolonnen i friskviktabellen
- **KUBE_KJONN**: Hvilket strata er hentet ut
- **KUBE_ALDER**: Hvilket strata er hentet ut
- **KUBE_UTDANN**: Hvilket strata er hentet ut
- **KUBE_INNVKAT**: Hvilket strata er hentet ut
- **KUBE_LANDBAK**: Hvilket strata er hentet ut
- **FRISKVIK_YEAR**: Hvilke år finnes i friskvikfilen
- **Last_year**: Er siste år i Friskvikfilen lik siste året i kubefilen? Normalt skal nyeste årgang slices ut. 
- **Periode_bm**: Hentet fra FRISKVIK-tabellen i ACCESS, år i barometerfiguren
- **Periode_nn**: Hentet fra FRISKVIK-tabellen i ACCESS, år i fotnotene under barometerfigur
- **Identical_prikk**:  Sjekker at prikking er lik i friskvikfilen og i kuben, for å sikre at ikke noen får tall i profilene som er prikket i statistikkbanken eller motsatt. 
- **Matching_kubecol**: Hvilken kolonne i kuben er det som matcher med tallene som vises i friskvik
- **Different_kubecol**: Hvilke kolonner i kuben matcher IKKE med det som vises i friskvik
- **Enhet**: Hentet fra FRISKVIK-tabellen i ACCESS, hvilken enhet står i barometeret.
- **REFVERDI_VP**: Hentet fra SPEC-filen som ble generert ved kubekjøring, hvordan var filen standardisert.
- **VALID**: Dersom enheten indikerer at filen er standardisert må den faktisk være standardisert, og det må være MEIS som vises i friskvik. Dersom dette er konsistent, er kombinasjonen valid, og dette indikeres her. 

# Hva skjer i bakgrunnen

`CheckFriskvik()` tar utgangspunkt i nyeste godkjentmappe med friskvikfiler. For hver av filene i denne mappen leter den i DATERT-mappene for kommune- og norgeshelsa etter en kubefil med samme datotag. Dersom flere kubefiler med samme datotag eksisterer, finnes den korrekte filen ved å sjekke i FRISKVIK-tabellen i ACCESS etter korrekt kubenavn. Den korresponderende SPEC-filen som ble generert ved kubekjøring leses også inn. 

Kubefilen filtreres basert på ETAB-kolonnen i friskvikfilen, i tillegg til alle felles kolonner med unntak av år. Den filtrerte kubefilen inneholder dermed det samme strataet som er slicet ut i friskvikfilen, men samtlige årganger. 

Friskvikfilen og den filtrerte kubefilen brukes som input i de ulike funksjonene som gjennomfører hver enkelt test. Resultatet av alle testene resulterer i en linje i outputfilen.


# Filer som ikke lar seg sjekke
For noen friskvikfiler er det ikke mulig å identifisere en korresponderende kubefil. Dette gjelder friskvikfiler generert utenfor løypen, som f.eks. forventet levealder som er basert på flere separate kubefiler. Disse filene vil gå en tom rad i outputfilen. 