---
layout: default
title: "R pakke"
parent: "Orgdata"
nav_order: 2  
---

## Orgdata og R versjon

Fra og med R versjon 4.2 ble default encoding endret. Dette medførte problemer med å lese norske bokstaver i Access og datafilene, som gav mismatch i kolonnenavn og krasj. Dette er fikset fra og med orgdata versjon 1.4.7, da encodingsystem for access og csv-filer nå defineres separat. Dette har medført at orgdata ikke lenger er kompatibelt med tidligere versjoner av R. 

Har du behov for å bruke R-versjon tidligere enn 4.2 (f.eks. 4.1.3), må du derfor installere orgdata versjon 1.4.6. Dette gjøres ved følgende kommando i konsollen.

```r
pak::pkg_install(helseprofil/orgdata@v1.4.6)
```

## Error loading "lazy-load database .... is corrupt" {#inst-error}

Når man installerer **orgdata** i RStudio kan det opptå feil ved kompilering av dokumentasjonen for `.Rdb` filer. Prøv:
- Restarte R bl.a ved å kjøre `.rs.restartR()`
- Slett orgdata med `remove.packages("orgdata")`
- Restarte RStudio
- Installere **orgdata** på nytt

## Error ved oppgradering

Prøv å gjøre det akkurat som for [Error loading..](#inst-error) ovenfor.


## Error with `rlang`

Hvis du får denne feilmelding om `rlang` versjon

```r
> library(orgdata)
Error: package or namespace load failed for ‘orgdata’ in loadNamespace(i, c(lib.loc, .libPaths()), versionCheck = vI[[i]]):
 namespace ‘rlang’ 1.0.2 is being loaded, but >= 1.0.5 is required
```

Slett eller uninstall `rlang` med `remove.packages("rlang")`.
Installere på nytt med `install.packages("rlang")`.

Hvis det ikke løser problemmet, slett alle pakke mappen i den R versjon du bruker. Mappen for R pakker ligger i `C:\Program Files\R`. Deretter installere `rlang` på nytt.
