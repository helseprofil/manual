---
layout: default
title: "HDIR-spesial"
has_children: true
nav_order: 7
---
  
Her finner du spesialløsninger som må benyttes for å kjøre systemet på HDIR-maskiner
i overgangsfasen.

# Installere prosjektene på ny PC

(Se eventuelt [Installasjon](https://helseprofil.github.io/manual/start-install.html)).

Du må først installere følgende programmer fra Firmaportal:
- **R (helst versjon 4.4, minimum 4.3)**
- **RStudio**
- **Git**. Denne må settes opp i RStudio (Tools -> Global Options -> Git/SVN)

Bruk deretter den nye løsningen for å installere pakker og prosjekter. 

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
ProfileSystems(path = NULL eller "din/favoritt/mappe")
``` 

Vil du klone alle relevante repo (Misc, config, GeoMaster osv) fra GitHub (for utvikling), kan du bruke:

```R
DevelopSystems(path = "din/favoritt/mappe")
```

# KHfunctions

Gå til mappen du har installert prosjektet i (default er C:/Brukere/navn/helseprofil). Åpne `.Rproj`-filen.
Ved oppstart er det mulig du må kjøre `renv::restore()` for å installere pakkene inni prosjektet. 

Siden alle filstier er nye på HDIR-siden, ligger det en versjon av prosjektet i en egen branch på GitHub. 

Når du åpner R-prosjektet `khfunctions` vil du få opp en feilmelding av typen **"KRITISK FEIL: path ikke funnet"**. Dette er fordi produksjonsbranchen er satt opp til FHI-filstier, og leter etter F-disken. For å bruke HDIR-versjonen av koden må du skrive følgende i konsollen:

```R
usebranch("HDIR")
```

Dette må du gjøre hver gang du starter prosjektet. Da leses alle funksjonene inn på nytt fra HDIR-branchen på GitHub. Deretter kan du bruke funksjonene `LagFilgruppe()` og `LagKube()` som normalt. 

# KHvalitetskontroll

Det ligger en versjon av prosjektet i en egen branch på GitHub. For å bruke denne må du skrive følgende i konsollen:

```R
.usebranch("HDIR")
```
(ja, det skal være . foran usebranch her)

For å lage rapporter må .Rmd-filene også fortelles at de skal bruke HDIR-variantene av kodene ettersom disse laster inn alle funksjoner fra scratch ved kjøring. Dette styres øverst i .Rmd-filene ved å ta vekk `#` foran linjen med `.usebranch("HDIR")`. 

# Orgdata

For å kjøre orgdata på HDIR-maskiner må du ha siste versjon (v1.4.9, oppdatert 21.05.2024). Installer denne ved:

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
ProfileSystems(all = F, orgdata = T)

# ELLER om du allerede har installert orgdata

orgdata::update_orgdata()
```

Når du laster inn orgdata med `library(orgdata)` skal du få opp en dialogboks som spør om du er på HDIR-maskin. Ved å trykke ja på denne, endres filstiene til `O:/...`, og du kan kjøre som vanlig.

For at databasen skal fungere må det eksistere en `chkfile.txt`, og inne i databasen må både link til denne og til backend-filen endres slik at de peker på riktig fil. 

For geo-databasen er det en tilsvarende `chkgeo.txt`-fil. 
