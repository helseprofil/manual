---
layout: default
title: "Installasjon og feilsøking" 
parent: "FAQ KHfunctions"
nav_order: 1
---

# Installasjon

Første gang du installerer prosjektet, kjør denne kommandoen.

```r
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_install(khfunctions)
```

Det skal ikke være behov for å installere prosjektet på nytt, da funksjoner alltid vil lastes direkte fra GitHub.

# Større oppdateringer

Ved større oppdateringer vil det i noen tilfeller bli nødvendig å installere prosjektet på nytt. I såfall må prosessen over gjentas utenfor R-prosjektet. For github-kyndige kan man også løse dette ved å bruke kommandoen `git pull` i terminal-vinduet, og så restarte (Ctrl + Shift + F10)

### Problemer med å installere

Hvis du får feilmelding når du kjører `kh_install(khfunctions)` kan du gjøre **EN** av disse:

1. Slett mappen `khfunctions` fra `C:/Users/DinBrukerNavn/helseprofil`, og prøv på nytt.
2. Spesifisere `path` der du vil installere `khfunctions`, for å installere prosjektet et annet sted, som dette:

```r
kh_install(khfunctions, path = "C:/Users/You/FolderName")
```

# Pakkeversjoner

For at alle skal bruke samme versjoner av alle pakker, vedlikeholdes dette via renv-pakken. Denne genererer en renv.lock-fil, som spesifiserer hvilken versjon som skal brukes av alle pakker. Ved oppstart av prosjektet vil du kunne få en advarsel om at prosjektet ikke er synkronisert med denne filen. Dette løser du ved å bruke følgende kommandoer og følge innstruks. Det anbefales å restarte prosjektet etterpå. 

Sjekke status:
```r
renv::status()
```

Oppdatere pakker
```r
renv::restore()
```

Om dette feiler, kan du prøve å installere den aktuelle pakken manuelt via menyene eller ved følgende kode, og deretter restarte prosjektet. 
```r
install.packages("pakkenavn")
```
