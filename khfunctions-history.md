---
layout: default
title: "Om prosjektet" 
parent: "FAQ KHfunctions"
nav_order: 3
---

KHfunctions er Hovedhjernen til dataprosessering for folkehelseprofilene. Koden er hovedsakelig utviklet og skrevet av [Kåre Bævre](https://www.fhi.no/om/organisasjon/helse-og-ulikhet/kare-bavre/). Prosjektet ble videre utviklet av [Yusman Bin Kamaleri](https://www.fhi.no/om/organisasjon/helse-og-ulikhet/yusman-bin-kamaleri/) frem til høsten 2022. 

I april 2023, i forbindelse med overgang til nytt publikasjonssystem, ble det gjennomført en større omstrukturering hvor all kode som tidligere var samlet i en stor fil `khfunctions.R` ble splittet opp i mange mindre filer, som ligger i mappen `R`. Filene er organisert etter hvor i prosjektet de ulike funksjonene brukes, og mange funksjoner ble også fjernet da de ikke lenger var i bruk. Dette ble gjort for å gjøre jobben med vedlikehold og videreutvikling lettere. 

En kopi av prosjektet slik det var før omstruktureringen finnes i branchen som heter "masterpreallvis". Man kan laste ned og bruke denne versjonen av prosjektet ved å kjøre følgende kode:

```r 
rm(list = ls())
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_source(repo = "khfunctions", branch = "masterpreallvis", file = "KHfunctions.R", encoding = "latin1")
```

### Dokumentasjon

[Dokumentasjon av LagFilgruppe](https://helseprofil.github.io/khfunctions/) (Skrevet av Yusman Bin Kamaleri)
