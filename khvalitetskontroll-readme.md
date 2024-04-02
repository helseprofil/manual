---
layout: default
title: "Oversikt" 
parent: "KHvalitetskontroll"
nav_order: 5
---

Her finner du en oversikt over relevante filer i KHvalitetskontroll-prosjektet, og hva disse inneholder. De enkelte funksjonene er dokumentert direkte i filene de ligger i. 

# Brukerfiler

Brukerfilene ligger i mappen `USER`, og inkluderer:

- `Kvalitetskontroll_del1.Rmd`: Genererer rapport nr 1
- `Kvalitetskontroll_del2.Rmd`: Formatterer fildumper, lager plott, genererer rapport nr 2
- `Friskviksjekk.Rmd`: Gjennomfører sjekk av filene i en godkjentmappe
- `Interaktiv.Rmd`: Inneholder funksjoner som kan brukes til interaktiv kvalitetskontroll av enkeltfiler

# Kodefiler

All kode i prosjektet ligger i mappen `R`, fordelt på følgende scriptfiler. 

## setup.R
Her settes encoding for å håndtere norske bokstaver, før de andre scriptene leses inn. Dette kjøres ved oppstart av prosjektet, styrt av .Rprofile-filen. Alt som kjøres ved oppstart styres i denne filen. Laster til slutt inn `welcome.R` som inneholder en velkomstmelding ved oppstart av prosjektet. 

## updateproject.R
Lastes inn av `setup.R`.

Aktiverer en dialogboks hvor man får mulighet til å oppdatere prosjektet. I praksis innebærer dette å få siste versjoner av brukerfiler og nyeste verjon av `renv.lock` slik at man bruker de samme versjonene av pakker. I tillegg hentes alle andre script fra GitHub, men funksjonene i disse leses ved bruk fra GitHub så det er ikke kritisk at disse er oppdatert lokalt.

## load_packages_functions.R
Lastes inn av `setup.R` ved oppstart av prosjektet, og kjøres også i starten av de ulike brukerfilene for å tillate å generere HTML-rapporter. 

Denne filen laster inn alle pakker som brukes i prosjektet, og bruker pakken `conflicted` til å velge hvilken funksjon som skal brukes i de tilfellene flere funksjoner har samme navn. I praksis forsøkes det å konsekvent bruke `pakke::funksjon()` i prosjektet for å bruke riktig funksjon, men dette sparer uansett en del advarsler ved oppstart.

Dette skriptet laster også inn de andre scriptene som inneholder funksjoner brukt i prosjektet. 

## globals.R
Lastes inn av `load_packages_functions.R`.

Setter opp noen globale parametre som `.ALL_DIMENSIONS`, `PROFILEYEAR`, `DUMPS`, `.currentgeo`, `.georecode` og `.popinfo`. I tillegg settes det opp noen grunnleggende plotteparametre som styrer utseende på plottene i rapportene. 

## misc.R
Lastes inn av `load_packages_functions.R`.

Inneholder funksjoner som brukes flere steder i prosjektet. For eksempel `ReadFiles()`, `SaveReport()`, `.IdentifyColumns()`, `.doGeoRecode()`, `.ConnectKHelsa()`, `.ConnectGeokoder()`, `.usebranch()`. Her ligger også funksjoner for å oppdatere geotabell og populasjonsvekter. 

## functions_step1.R
Lastes inn av `load_packages_functions.R`.

Her ligger alle funksjoner og hjelpefunksjoner som brukes til å generere HTML-rapporten Kvalitetskontroll_del1.

## functions_step2.R
Lastes inn av `load_packages_functions.R`.

Her ligger alle funksjoner og hjelpefunksjoner som trengs for å generere HTML-rapporten Kvalitetskontroll_del2.

## functions_plots.R
Lastes inn av `load_packages_functions.R`.

Her ligger all kode som trengs for å lage boksplott, tidsserieplott og bydelsplott. Disse brukes i brukerfilen `Kvalitetskontroll_del2.Rmd`

## functions_friskvik.R
Lastes inn av `load_packages_functions.R`.

Her ligger alle funksjoner som brukes for å gjennomføre sjekk av filene i nyeste godkjentmappe, som sikrer at det er de riktige dataene som havner i profilene, og at disse er de samme som publiseres i statistikkbanken. 

## functions_interactive.R
Lastes inn av `load_packages_functions.R`.

Her ligger litt forskjellige funksjoner som kan brukes for å gjøre interaktiv kvalitetskontroll av enkeltfiler. To nyttige funksjoner som ligger her er `FindGeo()` og `FindGeoName()` som bruker norgeo til å finne hhv navn på en geografisk enhet fra geokoden og å finne geokoden fra navnet på den geografiske enheten. 

## superseeded_deprecated.R
Lastes ikke inn. 

Inneholder funksjoner som er utgått eller erstattet av nyere funksjoner. Funksjoner kan flyttes hit etterhvert som de blir overflødige. 