---
layout: default
title: "HDIR-spesial"
has_children: true
nav_order: 7
---
  
Her finner du spesialløsninger som må benyttes for å kjøre systemet på HDIR-maskiner
i overgangsfasen.

# Installere prosjektene på ny PC

Bruk den nye løsningen. I påvente av at vi får tilgang til RTools er det bare mulig å installere pakker fra CRAN, khfunctions og KHvalitetskontroll. Dette kan du gjøre ved følgende kode (forutsatt at du har installert RStudio og Git). 

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
ProfileSystems(all = F,
               packages = T,
               norgeo = F,
               orgdata = F, 
               khfunctions = T,
               KHvalitetskontroll = T,
               path = NULL eller "din/favoritt/mappe")
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

Vi venter på RTools, ettersom prosjektet benytter norgeo. I mellomtiden vil ikke prosjektet fungere.

Det ligger en versjon av prosjektet i en egen branch på GitHub. For å bruke denne må du skrive følgende i konsollen:

```R
.usebranch("HDIR")
```
(ja, det skal være . foran usebranch her)

For å lage rapporter må .Rmd-filene også fortelles at de skal bruke HDIR-variantene av kodene ettersom disse laster inn alle funksjoner fra scratch ved kjøring. Dette styres øverst i .Rmd-filene ved å ta vekk `#` foran linjen med `.usebranch("HDIR")`. 

# Orgdata

Vi venter på tilgang til RTools for å kunne installere pakken.

# Norgeo

Vi venter på tilgang til RTools for å kunne installere pakken.
