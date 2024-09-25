---
layout: default
title: "qualcontrol"
parent: "produksjon"
nav_order: 3
---

qualcontrol er en [R-pakke](https://github.com/helseprofil/qualcontrol) som inneholder funksjoner for å gjennomføre kvalitetskontrollen av publikasjonsklare datafiler.

For å bruke khfunctions åpner du produksjonsprosjektet og går til filen `qualcontrol/1. Kvalitetskontrollrutiner.Rmd`. Denne inneholder en strømlinjeformet oversikt over kvalitetskontrollrutinene og følges nedover. 
Resultater vil lagres i PRODUKSJON/VALIDERING/QualControl/**PRODUKSJONSÅR**/**KUBENAVN** 

For å få tilgang til funksjonene må første kodeblokk med `library(qualcontrol)` kjøres. 

# Forarbeid

- Du kan endre produksjonsåret med funksjonen `update_qcyear()`. Dette bestemmer hvilken mappe resultatfilene vil publiseres i. 
- Last inn ny (og gammel/forrige publiserte) datafil med funksjonen `readfiles()`, og formatter filene med funksjonen `make_comparecube()`. Dette vil også produsere noen .csv-filer som lagres i mappen `FILDUMPER`.

# Stegene i kvalitetskontrollen. 

De ulike stegene dokumenteres i KUBESTATUS-tabellen i KHELSA.mdb.

# 1. Deskriptiv grovsjekk

- Her sjekkes hva som finnes i filen, f.eks. hvilke kolonner, hvilke nivåer i dimensjonene
- Tidsserier på landsnivå plottes for all dimensjoner for å fange opp eventuell feilklassifisering.

# 2. Batch vs Batch

- Sammenligning mot forrige publiserte fil
- Oppsummering av antallet identiske/ulike rader og hvor store forskjellene er
- Antallet forskjellige rader og summen av disse, totalt og per årgang
- Plott av forskjellene over tid, for å se om forskjellene er stabile eller endrer seg over tid

# 3. Prikking

- Er det noen tall under grensen for personvernskjuling?
- Sammenligning av antall skjulte tall, totalt og per årgang
- Sammenligning av antall tidsserier med 0-maks antall skjulte tall

# 4. Sjekk aggregering

- Sjekke at lavere geografisk nivå summerer seg opp til høyere, f.eks. at kommuner summerer seg til fylke.
- Sjekke andelen ukjent bydel
- Plotte tidsserier for bydelene, og vektede bydelstall mot kommunetallet. 

# 5. Ekstremverdier 

- Genererer boksplott og tidsserieplott som markerer ekstremverdier, definert som verdier utenfor intervallet definert av vektet 25.percentil - 1.5 * IQR og vektet 75.percentil + 1.5 IQR. 
- Disse vurderes for om de kan være riktige. 

# 6. Ekstremverdier, år-til-år

- Samme som over, men for relativ endring fra forrige årgang. Kan fange opp usannsynlig store endringer fra et år til et annet. 

