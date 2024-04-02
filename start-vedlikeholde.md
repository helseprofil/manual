---
layout: default
title: "Vedlikehold/Utvikling"
parent: "Startside"
nav_order: 2
---

For å vedlikeholde produksjonsapparatet uten at det blir rot bør man i hovedsak følge trinnene under. Dette sikrer at produksjonsbranchen (main/master) forblir stabil mellom oppdateringer. 

# 1. Opprette issue på GitHub

Dersom du savner noe, eller finner ut at noe ikke fungerer som det skal, kan dette legges inn som en "issue" i det aktuelle repoet på GitHub. Her er det fint om problemet eller ønsket beskrives så detaljert som mulig, slik at det er tydelig hva som må gjøres. Alle kan melde inn ønsker på denne måten. 

# 2. Lag ny branch for å løse en issue

Den som skal oppdatere koden oppretter en ny branch fra main/master eller dev, og gjør nødvendige endringer/utvikling i denne. I *khfunctions* og *khvalitetskontroll* kan man bruke funksjonen `usebranch(NAVN)` for å laste inn en spesifikk versjon fra github for testing. 

# 3. Pull request 

Når oppdateringen er komplett og ferdig testet, kan denne merges inn i dev eller main/master. Fortrinnsvis kan små oppdateringer merges til dev, før flere små endringer kan gå inn i produksjonsbranchen. 

For å merge en branch må det opprettes en pull request på GitHub, der man forteller hvilken branch som skal merges med dev eller main/master. Når denne er godkjent vil de nye endringene merges. Da kan man gjerne også slette den ferdige feature-branchen. 
