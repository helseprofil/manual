---
layout: default
title: "Installasjon"
parent: "Startside"
nav_order: 1  
---
# Hvordan sette opp systemet for databehandling

De tre hovedpakkene i produksjonsapparatet er `orgdata` (aggregering av originalfiler), `khfunctions` (lager filgrupper og kuber) og `KHvalitetskontroll`. 

## 1. Installere R, Rstudio og sette opp Git
For å installere pakkene må du først installere **R** (v4.3.0) og **RStudio**, som du  finner i Firmaportal. 
Du må også installere  **Git** (versjonskontroll) fra Firmaportal, og sette dette opp i RStudio (Global options). 

## 3. Sette encoding
Fra og med R versjon 4.2 ble det innført en endring i encoding, som gjør at norske bokstaver ikke leses korrekt. Vi må derfor sette encoding manuelt. For at dette skal skje automatisk når du bruker R, kan dette med fordel legges direkte i `.rprofile` som er et script som kjøres ved oppstart. For å redigere denne kan du skrive følgende i konsollen:

```R
usethis::edit_r_profile()
```

I dokumentet som åpnes legger du til følgende, og lagrer dokumentet: 
`Sys.setlocale("LC_ALL", "nb-NO.UTF-8")`

R-prosjektene som brukes i produksjonsapparatet har egne .rprofile-filer, der dette er håndtert.

## 2. Installere pakkene
Før installering, sjekk at du ikke er i et prosjekt. Ellers må du først stenge prosjektet ie. `Close Project`.
<p align="left"><img src="img/RStudio-project.png" width="330"/></p>

Kjør følgende kode for å installere alle pakker og sette opp mappestruktur:

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
ProfileSystems()
```

Dette vil opprette mappen `C:/Users/Navn/helseprofil`. Underprosjektene blir lagret i egne mapper i denne. 

Dersom du ønsker å ha prosjektene et annet sted kan du spesifisere argumentet `path`:

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
ProfileSystems(path = "Din/favoritt/mappe")
```

- Standard path blir `C:/Users/DittBrukernavn/helseprofil` hvis argument `path` ikke er spesifisert.

### Installere spesifikke deler av systemet
`ProfileSystems()` har argumenter som kan brukes for å bare installere spesifikke deler av systemet. Sett da `all = FALSE`, og endre de delene du vil installere/oppdatere til `TRUE`. 

```R
ProfileSystems(all = FALSE,
               packages = FALSE,
               norgeo = FALSE,
               orgdata = FALSE,
               khfunctions = FALSE,
               KHvalitetskontroll = FALSE)
```