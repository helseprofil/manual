---
layout: default
title: "KHfunctions" 
parent: "Tips and Tricks"
nav_order: 1  
---

### Spore opp funksjoner som brukes til debugging

For å se hvilke funksjoner som brukes eller aktiveres når man kjører
`LagFilgruppe` eller `LagKUBE` kan gjøres ved å definere `show_functions` objekt
til `TRUE` etter at man har `source` *KHfunctions.R* filen. Dersom du vil se funksjonen 
inkludert argumentene, kan du definere `show_arguments` til `TRUE`. Dersom begge er satt til
TRUE, vil `show_functions` brukes til debugging. 

```r
rm(list = ls())
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_source(repo = "khfunctions", branch = "master", file = "KHfunctions.R", encoding = "latin1")

show_functions <- TRUE
# Eller
show_arguments <- TRUE
```

Denne muligheten kan være nyttig for å se hvilke funksjoner som kan lage
problemer i kjøringen. Funksjonen som kjøres skal vises i *console* som:

```r
Execute: LagKUBE()
```

### Lagre loggfil som tekstdokument

*console* har en begrensning på hvor mange linjer som vises, av minnehensyn. Derfor vil ikke hele prosessen kunne vises for store funksjoner som lagKUBE, som overskrider denne grensen. For å komme rundt dette, kan du printe all output til et tekstdokument som lagres eksternt, ved hjelp av funksjonen `sink()`

Dette er spesielt nyttig i kombinasjon med debuggingalternativene over, da du kan få ut en komplett logg over alle funksjoner som blir kjørt.

```r
# Definer hvor du vil lagre loggen med sink()
sink(file = "filsti/.../.../filnavn.txt") 

# Kjør koden, f.eks. lagKUBE, hvor du også ønsker å få ut alle funksjonene med argumenter.
show_arguments <- TRUE
lagKUBE("NAVN")

# Lukk koblingen til den eksterne filen etter at du er ferdig
sink(file = NULL)
```
