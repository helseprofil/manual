---
layout: default
title: "HDIR-spesial"
has_children: true
nav_order: 7
---
  
Her finner du spesialløsninger som må benyttes for å kjøre systemet på HDIR-maskiner
i overgangsfasen.

# KHfunctions

Siden alle filstier er nye på HDIR-siden, ligger det en versjon av prosjektet i en egen branch på GitHub. 

Når du åpner R-prosjektet `khfunctions` vil du få opp en feilmelding av typen "KRITISK FEIL: path ikke funnet". Dette er fordi produksjonsbranchen er satt opp til FHI, og leter etter F-disken. For å bruke HDIR-versjonen av koden må du skrive følgende i konsollen:

```R
usebranch("HDIR")
```

Dette må du gjøre hver gang du starter prosjektet. Da leses alle funksjonene inn på nytt fra HDIR-branchen på GitHub. 

# KHvalitetskontroll

Vi venter på RTools, ettersom prosjektet benytter norgeo. 

Det ligger en versjon av prosjektet i en egen branch på GitHub. For å bruke denne må du skrive følgende i konsollen:

```R
.usebranch("HDIR")
```
(ja, det skal være . foran usebranch her)

# Orgdata

Vi venter på tilgang til RTools for å kunne installere pakken.

# Norgeo

Vi venter på tilgang til RTools for å kunne installere pakken.
