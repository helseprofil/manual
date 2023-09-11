---
layout: default
title: "Brukerveiledning del 2" 
parent: "FAQ KHvalitetskontroll"
nav_order: 3
---

Brukerfilen finner du i hovedmappen til prosjektet/USER/Kvalitetskontroll_del2.Rmd
Funksjonene ligger i [R/functions_step2.R](https://github.com/helseprofil/KHvalitetskontroll/blob/main/R/functions_step2.R)

# Generelle tips
- Kvalitetskontrollen kan gjennomføres stegvis nedover i dokumentet ved å trykke på "play" i hver kodechunk (evt ved å plassere pekeren inni kodechunken og trykke Ctrl + Shift + Enter). Det står i hver kodechunk for hvordan input til funksjonen eventuelt kan endres ved behov. 
- Kommentarer kan legges til i rapporten utenfor kodechunkene dersom det er ønskelig å ha disse med i rapporten. Bruk gjerne punktlister (* eller -). Det er også lagt opp til en kommentarliste øverst i filen. 

## Laste inn filer og omdøpe kolonnenavn
Dette er likt som i [del 1](https://helseprofil.github.io/khvalitetskontroll-del1.html), men det er viktig at det også fylles inn her for å kunne generere rapport. 

### Noen flere inputparametre er nødvendig:
- `PROFILEYEAR`: styrer hvilken mappe rapporten og fildumper lagres i
- `DUMPS`: Styrer hvilke fildumper som skal lagres. Som standard skal både dfnew_flag, dfold_flag og compareKUBE lages, men dette kan endres eller settes til NULL om du ikke vil lagre disse. 

## Formattering av data for videre prosesssering
- Funksjonen `FormatData()` bruker den nye og gamle filen til å generere `dfnew_flag`, `dfold_flag` og `compareKUBE`. 
- Argumentet `dumps` bestemmer hvilke fildumper som skal lagres. Dette er definert i objektet `DUMPS` over. I utgangspunktet vil ikke fildumpen skrives om den samme filen eksisterer (kjennetegnes av kubenavn og datotag). Dette kan overstyres ved å sette `Formatdata(overwrite = TRUE)`

### Forklaring av hva FormatData() gjør

#### 1. Flagging av nye og utgåtte rader
Den nye filen blir først flagget for å indikere om en rad er ny (newrow = 1). For fellesdimensjoner flagges rader som ikke eksisterer i den gamle filen, og for nye dimensjoner flagges alle rader som ikke = 0 (totaltall, som implisitt finnes i gammel fil). Den gamle filen blir tilsvarende flagget for om en rad er utgått (exprow = 1), altså at den ikke lenger er med i den nye filen. 

#### 2. Identifisering av uteliggere
- Både ny og gammel fil blir flagget for uteliggere, både for absolutte tall og for år-til-år endringer.
- Uteliggere defineres basert på `MEIS` > `RATE` > `SMR`, og innenfor geonivåene L, F, K (store kommuner), k (små kommuner) og B. 
- Først estimeres kolonnene `MIN`, `MAX`, vektede (etter innbyggertall) kvantiler: `wq25`, `wq50`, `wq75`, og grenseverdier for uteliggerdeteksjon `LOW` og `HIGH`. 
- Uteliggere defineres deretter som tallene som ligger utenfor grenseverdiene. Kolonnene OUTLIER (0-1) og HIGHLOW representerer om noe er en uteligger og om den er høy eller lav.
- Tallene som representerer år-til-år endringer har kolonnenavn som starter på `change_`

#### 3. Lage compareKUBE
- Felles dimensjoner og felles verdikolonner er grunnlaget for compareKUBE, nye og utgåtte rader filtreres bort.
- Dersom gammel fil inneholder kolonnene `TELLER`, `NEVNER`, `sumTELLER`, `sumNEVNER`, `RATE.n`, mens ny fil ikke gjør det, vil disse i den nye filen erstattes med tilsvarende `_uprikk`-kolonne, for å kunne sammenligne tall. Disse vil da prikkes basert på SPVFLAGG != 0. 
- Alle verdikolonner fra ny og gammel fil får suffix `_new` og `_old`
- For alle par av `_new` og `_old` verdikolonner lages det en  `_diff` (absolutt forskjell) og `_reldiff` kolonne. 

#### 4. Identifisere bare nye uteliggere
- Dersom uteligger er definert basert på samme variabel i ny og gammel fil, vil den flaggede nye filen også få kolonnene `PREV_OUTLIER` og`NEW_OUTLIER`, som er 0-1 variabler som hhv indikerer om noe var uteligger også i den gamle filen, og om noe er en ny uteligger i årets fil. Tilsvarende for `change_...` 

### dfnew_flag innhold, tolkning og bruk
- Alle rader til og med SPVFLAGG er identisk som ALLVIS-kuben. Kolonnene som ligger etter denne inneholder informasjon om:
    - hvorvidt noe er en ny rad (newrow = 1)
    - Uteliggere: Grenseverdier og indikatorkolonner for å vise om noe er en uteligger, og om noe har vært uteligger tidligere. Kan være nyttig å filtrere på `NEW_OUTLIER` for å få en liste over nye uteliggere, som er lettere enn å se på boksplott alene. Senere vil denne kolonnen brukes for å bare plotte de nye uteliggerne. 


### dfold_flag innhold, tolkning og bruk
- Mest av alt en hjelpefil for å lage dfnew_flag og compareKUBE. 

### compareKUBE innhold, tolkning og bruk
- Inneholder alle felles dimensjoner, ny/gammel kolonne samt absolutt/relativ diffkolonne for alle felles verdikolonner. 
- Alle kolonner til og med SPVFLAGG er med i begge filene. 
    - Dersom f.eks. TELLER_new og TELLER_old kommer etter SPVFLAGG, betyr det at TELLER ikke er med i den nye filen, og at det er TELLER_uprikk som er benyttet i sammenligningen. Tilhørende diff-kolonner vil også komme til slutt. 
- Brukes hovedsakelig til å sammenligne årets mot forrige fil, for å se at det ikke er kommet inn betydelige forskjeller i dataene. Bruk diff-kolonnene for å sortere på størst/minst diff. 


## Sammenligning av rader med forskjell
`- CompareDiffRows()` genererer en interaktiv tabell basert på `compareKUBE` som forteller, fordelt på geonivå og for hver verdikolonne:
    - Hvor mange rader er identiske
    - Hvor mange rader er prikket nå, men var ikke prikket sist
    - Hvor mange rader har tall nå, men var prikket sist
    - Hvor mange rader er ulike.
- For ulike rader, beregnes:
    - Gjennomsnittlig, minimum, maximum forskjell, både absolutt (ny - gammel) og relativ (ratio ny/gammel)
    
## Plotting av differ over tid
- `PlotTimediff()` genererer et plott per geonivå, hvor de absolutte og relative diffene plottes med AAR på x-aksen. Disse plottene kan brukes til å se om forskjellene mellom den nye og gamle filen endrer seg over tid, f.eks. om forskjellene er større for gamle tall. 
- Funksjonen bruker MEIS > RATE > SMR, og om ingen av disse er med plottes ingenting. 

## Lagre rapport
Se [del 1](https://helseprofil.github.io/khvalitetskontroll-del1.html)



