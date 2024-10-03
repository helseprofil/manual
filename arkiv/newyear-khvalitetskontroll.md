---
layout: default
title: "Oppdatere KHvalitetskontroll" 
parent: "Ny årgang"
nav_order: 4  
---

Her følger en liste over ting som er viktig å oppdatere i kvalitetskontrollsystemet før ny årgang.

# Oppdatere GEO-koder og befolkningsvekter

Omkoding av GEO (for harmonisering av forrige fil ved sammenligning) og befolkningsvekter (for deteksjon av ekstremverdier) benytter filene `data/georecode.csv` og `data/popinfo.csv`. Disse må oppdateres ved overgang til ny profilårgang. 

For å oppdatere GEO-kodene, kjør følgende kode:

```r
.updateGeoReode(year = 2024)
```

For å oppdatere befolkningsvektene, kjør følgende kode. `popfile` skal være komplett filnavn på befolkningsfilen i NESSTAR-mappen. 

```r
updatePopInfo(popfile = "BEFOLK_GK_2024-01-04-12-34",
              year = 2024)
```

# Oppdatere `globals.R`

- Globals-filen henter inn listen over dimensjoner, denne bør sjekkes at er oppdatert. 
- Endre parametrene `PROFILEYEAR` og `.currentgeo`

# Pushe til github
Ved oppstart leser prosjektet alle innstillinger fra master-branch på github. De lokale filene brukes ikke. Derfor er det viktig at disse endringene pushes til GitHub. 

Dette kan du gjøre i terminalvinduet ved å skrive følgende:

- `git add -A`. Dette gjør alle endrede filer klare til opplasting
- `git commit -m "new profile year"`. Skrive en commit-melding for å beskrive hva som er gjort
- `git push`. Laste endringene opp til GitHub. 


