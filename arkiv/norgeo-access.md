---
layout: default
title: "Geo-databasen" 
parent: "Norgeo og Geo-databasen"
nav_order: 2
---

GEO-databasen oppdateres ved hjelp av norgeo-funksjoner. Brukerveiledning ligger [her](https://helseprofil.github.io/orgdata/articles/geo-recode.html)

For å oppdatere tabellene for hvert geonivå i geo-databasen brukes funksjonen `geo_recode()`. Denne benytter `track_change()` fra norgeo, med fix = TRUE for å håndtere geosplitting. For å lage koblingstabellen som kobler koder fra ulike geonivå sammen (f.eks. grunnkrets -> kommune -> fylke -> bydel) brukes funksjonen `geo_map()`. 