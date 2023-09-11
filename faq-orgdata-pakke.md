---
layout: default
title: "R pakke"
parent: "FAQ orgdata"
nav_order: 2  
---

## Error loading "lazy-load database .... is corrupt"

Når man installerer **orgdata** i RStudio kan det opptå feil ved kompilering av dokumentasjonen for `.Rdb` filer. Prøv:
- Restarte R bl.a ved å kjøre `.rs.restartR()`
- Slett orgdata med `remove.packages("orgdata")`
- Restarte RStudio
- Installere **orgdata** på nytt

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
