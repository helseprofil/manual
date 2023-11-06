---
layout: default
title: "Brukerguide" 
parent: "FAQ KHfunctions"
nav_order: 2
---

# Oppstart
Hver gang prosjektet startes, vil setupfilen lastes fra GitHub. Denne laster ned alle funksjoner fra GitHub, slik at de er tilgjengelige for deg i environment (listen ser du i RStudio). 

For å sikre at du har siste versjon av funksjonene er det anbefalt å restarte (Ctrl + Shift + F10) prosjektet, og ikke la det stå åpent over lengre perioder ettersom du da vil fortsette å bruke innlastet versjon frem til neste gang du restarter. 

# Sepaafil
Filen *sepaafil.R* som ligger lagret lokalt kan være utdatert, og bør ikke brukes. En oppdatert versjon per 12.05.2023 ligger på github, og vil lastes ned enten ved å installere prosjektet på nytt eller ved å bruke *git pull* i Terminal-vinduet. Det skal stå øverst i filen at den er oppdatert 12.05.2023

<div id="toc">
  <h2>Innhold</h2>
  <ul>
    <li><a href="#fg">LagFilgruppe()</a></li>
    <li><a href="#kube">LagKUBE</a></li>
  </ul>
</div>

# LagFilgruppe {#fg}

- Selve funksjonen er uendret per mai 2023, og hovedfunksjonen som brukes er:

```r
LagFilgruppe("FILGRUPPENAVN", versjonert = TRUE)
```

- Etter overgang til R >= 4.2 er standard encoding endret. Filgrupper som er kjørt gjennom orgdata (f.o.m. versjon 1.4.7) vil ha UTF-8-encoding, og kan leses direkte i LagFilgruppe. Filer som ikke har gått gjennom orgdata må sannsynligvis leses med spesifikk encoding, spesielt om de inneholder ÆØÅ. I tabell INNLESING kan dette styres i kolonnen INNLESARG. 
    - Dersom brukfread=FALSE leses filen inn med read.csv(), og da kan man sette encoding="latin1". 
    - Dersom brukfread ikke er satt til FALSE leses filen med fread(), og da må man sette encoding="Latin-1"
- Manheader kan brukes dersom norske bokstaver bare finnes i kolonnenavnene, men ikke dersom de også forekommer i radene (f.eks "DØD AV..."). Da må encoding-argumentet settes for at filgruppen skal bli riktig. 

# LagKUBE {#kube}

Denne delen av produksjonsløypen er oppdatert per 12. mai 2023. Hovedfunksjonen som skal brukes er:

```r
LagKubeDatertCsv("KUBENAVN")
```
- Denne lagrer en ALLVIS-kube i `KUBER/....HELSA/DATERT`, en Kvalitetskontrollkube i `KUBER/....HELSA/QC` og access-specs ved kubekjøring i `KUBER/....HELSA/SPECS`. 
- I tillegg lagres det et objekt i RStudio som heter `RESULTAT` hvor du kan åpne de ulike elementene direkte i RStudio ved å skrive `RESULTAT$ALLVIS` og `RESULTAT$QC`.


# Fildumper
For å lage fildumper må du først lage en liste over hvilke dumppunkter du ønsker, og hvilket format ("CSV", "STATA") disse skal være i. Deretter må du angi dette i filgruppe- eller kubekjøringen, som under: 

```r
dumps <- list() # Dette gir ingen dumper
dumps <- list(STATAPRIKKpre = "CSV", STATAPRIKKpost = "STATA", RSYNT_POSTPROSESSpost = c("CSV", "STATA"))
LagKubeDatertCsv("KUBENAVN", dumps = dumps)
LagFilgruppe("FILGRUPPENAVN", versjonert = TRUE, dumps = dumps)
```
## Tilgjengelige dumppunkter i LagFilgruppe:

- RSYNT_PRE_FGLAGRINGpre
- RSYNT_PRE_FGLAGRINGpost
- RESHAPEpre
- RESHAPEpost
- RSYNT2pre
- RSYNT2post
- KODEBOKpre
- KODEBOKpost
- RSYNT1pre
- RSYNT1post

## Tilgjengelige dumppunkter i LagKUBE:
- raaKUBE0
- maKUBE0
- anoKUBE1
- anoKUBE2
- anoKUBE3
- anoKUBE4
- KUBE_SLUTTREDIGERpre
- KUBE_SLUTTREDIGERpost
- STATAPRIKKpre
- STATAPRIKKpost # Rett før postprosess, kan brukes som postprosess-pre.
- RSYNT_POSTPROSESSpost

# TEST-branch. 

Ved testing av ny funksjonalitet, må følgende kode kjøres for å bruke aktuell testversjon av funksjonene:

```r
rm(list = ls())
source("https://raw.githubusercontent.com/helseprofil/misc/main/utils.R")
kh_source(repo = "khfunctions", branch = "NAVN PÅ TESTBRANCH", file = "R/KHsetup.R", encoding = "latin1")
```
