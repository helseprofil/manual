---
layout: default
title: "orgdata"
parent: "Produksjon"
nav_order: 1
---

Orgdata er en [R-pakke](https://github.com/helseprofil/orgdata) som brukes for å aggregere rådatafiler. 

For å bruke orgdata åpner du produksjonsprosjektet og går til filen `orgdata/orgdata brukerkode.Rmd`. Denne inneholder eksempelkode som kan tilpasses til filen som skal kjøres. 

Parametre må settes opp i ACCESS-filen `raw-database.accdb`

For å få tilgang til funksjonene må første kodeblokk med `library(orgdata)` kjøres. 