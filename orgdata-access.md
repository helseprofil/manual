---
layout: default
title: "Access-database"
parent: "Orgdata"
nav_order: 1  
---

## Advarsel "Kan ikke legge til post(er) ..." i Access

Du får advarselen når du skal legge `LESID` og `FILGRUPPE` etter at du har lagt
inn `FILNAVN`. Trykk **OK** og flytt cursor ned eller opp. Deretter bør du kunne
legge `LESID` og `FILGRUPPE`.

## Kan ikke lese filen flere ganger i Access

For å kunne lese en fil flere ganger f.eks annen fane i en Excel fil, kan gjøres
ved å velge `Rediger` knappen. Valg `FILID` av filen, men IKKE skrive filstien på
nytt siden den allerede finnes i databasen ie. original filer.

## Hvordan finner jeg FILID av en tidligere rawfil

Trykk knappen **Orgfiler**. En ny fane som heter *Originalfiler* åpnes hvor du kan
søke filen du er interessert i. Deretter ser du *FILID* til filen.

## Feilmelding om "dublettverdier i en indeks, primærnøkkel eller relasjon".

Dette skjer ofte når man skal legge inn ny rawfil som allerede finnes i
databasen. Trykk knappen **Orgfiler** og bruk *FILID* til den filen som allerede
finnes i databasen istedenfor å legge den på nytt.

## Kan ikke se doble anførselstegn `""` i Access når kodebok for TYPE er RE

Når en kolonne skal omkodes ved bruk av TYPE lik `RE` til `""` blir symbolen
likevel forsvant eller usynlige når cursor blir flyttet. Løsningen er å skrive
enten `delete` eller `slett` i *TIL* for å gjøre det tydelig. Selvsagt funker det
med `""` også, hvis du vil gjøre det vanskelig for deg selv og andre å se hva
som egentlig definert i kodeboken &#128512;

## Kolonnenavn med ÆØÅ - bruk regulært uttrykk i MANHEADER ved behov 

*Oppdatering:* Fra versjon 1.2.1 kan man bruke *regulært uttrykk* dvs.
`^$\[.*\]` osv. i MANHEADER også f.eks `^utdan=UTDANNING` for å gi nytt navn for spesielle kolonner f.eks et langt og med `æøå` kolonnenavn `utdanning særlig før migrasjonsår` til et kort kolonnenavn `UTDANNING`.

**Problem ca 01.09.22:**
I går prøvde Hanna og jeg å lese inn UFORE-filene i orgdata. Det fungerte ikke på min PC (og heller ikke hos Yusman). Problemet var knyttet til ÆØÅ, som ble lest forskjellig fra Access og fra filene, slik at kolonnenavnene ikke matchet.  Det ble lest inn feil både i filene og fra Access specs, men feil på to forskjellige måter. Dette medførte også utfordringer med å se på spesifikke kolonner, da R ikke klarte å lese riktige kolonnenavn. 

Etter mye frem og tilbake ser det ut til at dette er knyttet til encoding-innstillinger som er endret i R versjon 4.2 (gått over til UTF-8). 

LØSNING 1: Jeg endret til R versjon 4.1.3, og da fungerte alt som det skulle. 

NESTEN LØSNING 2: I R versjon 4.2.1 forsøkte jeg å endre encoding-innstillingene til å bruke det samme som i tidligere R-versjoner. Da får jeg til å lese riktige kolonnenavn i filene, men kolonnenavnene fra Access specs leses fortsatt inn feil. Dette løser altså halve problemet. Korrekt innlesing av access specs må endres i selve orgdata, så det må Yusman være med å se på når det dukker opp en ledig stund. 

KONKLUSJON:
-	Foreløpig fortsett å bruke R versjon 4.1.3
-	Jeg vet ikke hvordan en oppdatering til R 4.2.x vil påvirke KHfunctions, det må testes
-	I fremtiden bør vi nok alle oppdatere til siste versjon av R, men da må vi først få orden på encodingen slik at det ikke dukker opp mer problemer. 

MANHEADER:
Dette feltet i Access-specen gjør at kolonnehoder i innfilen erstattes med noe vi skriver. 
De "vanskelige" kolonnehodene angis med nummer, og bør gis navn uten ÆØÅ.


