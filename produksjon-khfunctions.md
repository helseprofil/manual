---
layout: default
title: "khfunctions"
parent: "produksjon"
nav_order: 2
---

khfunctions er et [R-prosjekt](https://github.com/helseprofil/khfunctions) som inneholder hoveddelen av koden som brukes for databehandling. 

For å bruke khfunctions åpner du produksjonsprosjektet og går til filen `khfunctions/khfunctions brukerkode.Rmd`. Denne inneholder eksempelkode for å lage filgrupper (stablede filer) og kuber (produksjonsklare datafiler). Det ligger også eksempler på hvordan du kan lagre fildumper på ulike steder i prosesseringen. 

Parametre må settes opp i ACCESS-filen `KHELSA.mdb`, og logg skrives til ACCESS-filen `KHlogg.mdb`

For å få tilgang til funksjonene må første kodeblokk med `use_khfunctions()` kjøres. 

# Kontroll av siste kjøring

- Etter kjøring kan du se resultatene direkte i objektet RESULTAT, som inneholder full datafil, den filen som skal publiseres, og filen som brukes til kvalitetskontroll. 
- Du kan også se på loggfilene i ACCESS-databasen.