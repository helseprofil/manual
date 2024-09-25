---
layout: default
title: "khfunctions"
parent: "Produksjon"
nav_order: 2
---

[khfunctions](https://github.com/helseprofil/khfunctions) er et R-prosjekt som inneholder hoveddelen av koden som brukes for databehandling. 

For å bruke khfunctions åpner du produksjonsprosjektet og går til filen `khfunctions/khfunctions brukerkode.Rmd`. Denne inneholder eksempelkode for å lage filgrupper (stablede filer) og kuber (produksjonsklare datafiler). Det ligger også eksempler på hvordan du kan lagre fildumper på ulike steder i prosesseringen. 

For å få tilgang til funksjonene må første kodeblokk med `use_khfunctions()` kjøres. 

# Bruk

- De to hovedfunksjonene i prosjektet er `LagFilgruppe()` og `LagKUBE()`.
- Parametre må settes opp i ACCESS-filen `KHELSA.mdb`, og logg skrives til ACCESS-filen `KHlogg.mdb`

# Kontroll av siste kjøring

- Etter kjøring kan du se resultatene direkte i objektet RESULTAT, som inneholder full datafil, den filen som skal publiseres, og filen som brukes til kvalitetskontroll. 
- Du kan også se på loggfilene i ACCESS-databasen.