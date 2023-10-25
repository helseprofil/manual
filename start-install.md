---
layout: default
title: "Installasjon"
parent: "Startside"
nav_order: 1  
---

# Hvordan installerer ...

Installasjon brukes for å sette opp ny maskin eller kjører fersk installasjon.
Det er viktig at du må først installere **Git** fra Firmaportalen.

### KHfunctions
- Sjekk at du ikke er i et prosjekt. Ellers må du først stenge prosjektet ie. `Close Project`.
<p align="left"><img src="img/RStudio-project.png" width="330"/></p>

- Kjør:

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_install(khfunctions)

# Eller
kh_install(khfunctions, path = "C:/Min/Favoritt/Path")
```
- Standard path blir `C:/Users/DittBrukernavn/helseprofil` hvis argument `path` ikke er spesifisert.
- RStudio skal restarte når alle tillegg pakkene har blitt installert og så re-åpne innen *khfunctions* prosjekt.
For å synkronisere alle pakkeversjoner som brukes i *KHfunctions*, kjør:

```R
renv::restore()
```

- I tillegg til ny maskin så trenger du å kjøre komandoen på nytt hvis:
  1. Nye pakker eller oppdatert pakker versjoner har blitt brukt i `KHfunctions.R`. Du bør få beskjed om dette.
  2. Du har oppgradert R versjon

- Du behøver *IKKE* å kjøre komandoen på nytt hvis det bare er endring i kodene. 

- For mer detaljert veileding kan leses [her](https://github.com/helseprofil/khfunctions#khfunctions "khfunctions")

### orgdata
- Kjør:

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_install(orgdata)
```
- Du får automatisk beskjed i consolen ved pakke *loading* når det kommer ny
   versjon. For å oppdatere til ny versjon manuelt, kjør:

```R
orgdata::update_orgdata()
```
- For mer detaljert veiledning kan leses [her](https://helseprofil.github.io/orgdata "orgdata")

### Andre
Du kan også installere andre R pakker eller løsninger som brukes i arbeidet med KHelse via `kh_install()` funksjon
f.eks `KHvalitetskontroll`, `norgeo` og `lespdf`. Skulle det være et behøv for å installere vanlige R pakker fra CRAN også
i tillegg til de for KHelse samtidig så kan du bruke `kh_load()` funksjon til formålet. Funksjonen skal både `load`
pakker eller installere først hvis ikke allerede er gjort. Du kan lese [her](https://helseprofil.github.io/manual/start-load.html "kh_load")
om hvordan du kan bruke funksjonen effektivt.
