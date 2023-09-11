---
layout: default
title: "Bruk"
parent: "Startside"
nav_order: 2  
---

# Hvordan bruker ...

### KHfunctions
- Sjekk at du er i prosjekt for *khfunctions*.
- Bruk [SePaaFil.R](https://helseprofil.github.io/orgdata/articles/sepaafil.html) som veileding til hvordan man kan få tilgang til alle funksjonene i KHelse ved å source `KHfunctions.R` fra GitHub.
- Hvis du ikke vil bruke `SePaaFil.R` er det viktig at du kjører komandoen nedenfor først for å kunne ha tilgang til alle funksjonene i *KHfunctions*

```R
rm(list = ls())
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_source(repo = "khfunctions", branch = "master", file = "KHfunctions.R", encoding = "latin1")
```

### orgdata

- Du må gjøre *orgdata* pakke tilgjenglig ved å kjøre `library(orgdata)`
- Eksampler til bruk av de funksjonene for orgdata finnes i [SePaaFil.R](https://helseprofil.github.io/orgdata/articles/sepaafil.html "sepaafil")
