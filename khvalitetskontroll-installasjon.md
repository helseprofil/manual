---
layout: default
title: "Installasjon og feilsøking" 
parent: KHvalitetskontroll"
nav_order: 1  
---

## Installasjon

For å installere prosjektet, kjør:

```r
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_install(KHvalitetskontroll)
```
RStudio restarter når prosessen er ferdig, og prosjekt for KHvalitetskontroll åpnes automatisk. 

Prosjektet lagres her: 
`C:/Users/dittBrukerNavn/helseprofil/KHvalitetskontroll`.

## Oppstart

- Når prosjektet åpnes, vil du få spørsmål om du vil oppdatere til siste versjon. Velger du ja, vil siste versjon av alle filer lastes fra GitHub. Velger du nei, beholder du filene slik de var, slik at du kan ta kopi av endringer du ønsker å beholde.
- Funksjonene lastes alltid direkte fra GitHub, men du bør alltid ha siste versjon av brukerfilene.
- Alle filer som skal brukes ligger i mappen `USER`.

- **Det er anbefalt å restarte prosjektet (Ctrl+Shift+F10) før du begynner med ny fil**

## Feilsøking ved oppdaterings- og oppstartsproblemer

### Kan ikke oppdatere Rprofilen
Dersom du har en tidligere versjon installert kan det oppstå problemer ved oppdatering ettersom .Rprofilen er endret i nyere tid. Dette er et script som kjøres ved oppstart, og denne kan ikke oppdateres på samme måte som andre filer. Dette kan løses på en av flere måter:

1. I Terminal-vinduet, skriv: `git pull`, forsøk så å restarte (Ctrl + Shift + F10)
2. Forsøk å installere prosjektet på nytt som beskrevet over
3. Slett prosjektet og installer på nytt

### Merge conflicts
Dersom du får feilmelding om merge conflict f.eks. (lib2git::checkout_tree: 1 conflict prevents checkout), så skyldes det sannsynligvis at du har lagret en endring i en lokal fil som ikke er kompatibel med endringene som er gjort i hovedfilene. I Git-vinduet vil du kunne se hvilken fil dette gjelder. Dette kan løses på en av flere måter.

1. I terminal-vinduet, skriv: `git pull`, forsøk så å restarte (Ctrl + Shift + F10)
2. I terminal-vinduet, skriv: `git stash`, deretter `git pull`, forsøk så å restarte (Ctrl + Shift + F10)
3. Dersom filen er 'renv/settings.json' er løsningen å slette denne filen og restarte prosjektet. 
4. If all else fails, slett prosjektet og installer på nytt. 

### renv/activate.R
Får du feilmeldingen: "In file(filename, "r", encoding = encoding) :   cannot open file 'renv/activate.R", løses dette ved å kjøre `renv::activate()` i konsollen.

### Problemer med pakker eller pakkeversjoner
Får du advarsel om at prosjektet ikke er synkronisert med lockfilen, løses dette vanligvis ved å bruke `renv::restore()` i konsollen og følge innstruksene som dukker opp. 
