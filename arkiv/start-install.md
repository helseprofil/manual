---
layout: default
title: "Installasjon"
parent: "Startside"
nav_order: 1  
---

# Hvordan sette opp systemet for databehandling

Følg stegene under. Det er viktig at hvert steg fullføres før du går videre til neste!

### 1. Installere R, Rstudio, Rtools og sette opp Git

I Firmaportal, installer programmene **R** (minimum versjon 4.4.0), **Rstudio**, **Rtools** (versjon 4.4) og **Git**

### 2. Sette opp Git i RStudio

Åpne Rstudio og gå til Tools -> Global Options -> GIT/SVN. Sjekk at *Enable version control* er huket av og at git.exe-filen er angitt. Dette er viktig for å kunne synkronisere prosjekter og installere pakker som ligger på GitHub. 

### 2b. Autentisering i git

Dette er bare aktuelt om du har behov for å laste opp endringer til GitHub.
For å sette opp autentisering i GitHub, bruk følgende kode. Det kan være du må installere pakken `usethis` først.

```R
usethis::create_github_token()
```
Dette tar deg til GitHub i nettleseren, hvor du kan sette opp en token som kobler din påloggingsinformasjon til RStudio. Denne må du kopiere. Deretter kjører du følgende i RStudio.

```R
gitcreds::gitcreds_set()
```
Følg instruksjonene og lim inn koden fra GitHub. 

### 3. Sette encoding (valgfri, men veldig nyttig)

Fra og med R versjon 4.2 ble det innført en endring i encoding, som gjør at norske bokstaver ikke leses korrekt. Vi må derfor sette encoding manuelt. For at dette skal skje automatisk når du bruker R, kan dette med fordel legges direkte i `.rprofile` som er et script som kjøres ved oppstart. For å redigere  denne kan du skrive følgende i konsollen, og endre filen som åpnes. Det kan være du må installere pakken `usethis` først.

```R
usethis::edit_r_profile()
```

I dokumentet som åpnes legger du til følgende, og lagrer dokumentet: 
`Sys.setlocale("LC_ALL", "nb-NO.UTF-8")`

  
### 4. Installere pakkene

I konsollen, kjør følgende kode for å installere alle pakker og sette opp mappestruktur:

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
ProfileSystems()
```
Funksjonen gjør:

- Oppretter mappen `C:/Users/Navn/helseprofil`. Denne er viktig da den brukes til å lagre midlertidige filer lokalt på den PCen som gjennomfører databehandling. 
- Oppretter R-prosjektet **produksjon**, som inneholder brukerfiler for de ulike delene av produksjonsapparatet. 
- Installerer alle nødvendige pakker, inkludert våre lokale pakker *norgeo*, *orgdata*, *qualcontrol*

Etter installasjon kan du finne mappen *produksjon* i filbehandleren (eller via RStudio) og åpne filen *produksjon.Rproj*. Når du først har åpnet den vil du finne den i prosjektlisten oppe til høyre i RStudio. 

Dersom du ønsker å ha prosjektene et annet sted enn i helseprofilmappen kan du spesifisere argumentet `path`

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
ProfileSystems(path = "Din/favoritt/mappe")
```

# For utviklere

Skal du bidra til utvikling av databehandlingssystemet trenger du tilgang til alle relevante underprosjekter. Disse kan klones ved å bruke følgende funksjon. Dersom du setter getupdates = TRUE vil den også oppdatere prosjekter du allerede har installert. 

```R
source("https://raw.githubusercontent.com/helseprofil/misc/main/ProfileSystems.R")
DevelopSystems(path = "Din/favoritt/mappe", getupdates = FALSE)
```

Dette installerer følgende prosjekter:

- produksjon
- norgeo
- orgdata
- khfunctions
- orgcube (foreløpig navn på pakke som skal erstatte khfunctions)
- qualcontrol
- config
- GeoMaster
- misc
- manual
- snutter (R-snutter som brukes i databehandlingen)

De ulike prosjektene inneholder ulike deler av produksjonsapparatet, og synkroniseres med GitHub. 
