---
layout: default
title: "Oversikt" 
parent: "KHfunctions"
nav_order: 5
---

Her finner du en oversikt over relevante filer i KHfunctions-prosjektet, og hva disse inneholder. De enkelte funksjonene er (delvis) dokumentert direkte i filene de ligger i. 

# Kodefiler

All kode i prosjektet ligger i mappen `R`, fordelt på følgende scriptfiler. 

## KHsetup.R
Lastes inn i `.Rprofile`.

Setter encoding for å håndtere norske bokstaver, oppdaterer lockfilen dersom man er i master-branch, laster inn alle pakker og bruker pakken `conflicted` til å velge hvilken funksjon som skal brukes i de tilfellene flere funksjoner har samme navn. I praksis forsøkes det å konsekvent bruke `pakke::funksjon()` for å bruke riktig funksjon, men dette sparer uansett en del advarsler ved oppstart. Laster deretter inn alle de andre filene som inneholder interne funksjoner. 

## KHmisc.R
Lastes inn av `KHsetup.R`.

Inneholder funksjoner som brukes både i `LagFilgruppe()` og `LagKUBE()`.

## KHpaths.R
Lastes inn av `KHsetup.R`.

Setter grunnsti til produksjonsmappen og til `KHELSA.mdb` og `KHlogg.mdb`. Inneholder også funksjoner for testing og lokal kjøring, men disse brukes lite. 

## KHglobs.R
Lastes inn av `KHsetup.R`.

Setter alle globale parametre og lager objektet `KHglobs` som brukes i de fleste funksjoner i prosjektet. 

## KHfilgruppefunctions.R
Lastes inn av `KHsetup.R`.

Inneholder funksjoner som brukes i `LagFilgruppe()`. 

## KHfilgruppe.R
Lastes inn av `KHsetup.R`.

Inneholder hovedfunksjonen `LagFilgruppe()`.

## KHkubefunctions.R
Lastes inn av `KHsetup.R`.

Inneholder funksjoner som brukes i `LagKUBE()`.

## KHkube.R
Lastes inn av `KHsetup.R`.

Inneholder hovedfunksjonen `LagKUBE()`.

## KHother.R
Lastes inn av `KHsetup.R`

Inneholder funksjoner som ikke brukes i hovedfunksjonene, bl.a. for sammenligning av kubefiler. Trolig overflødige, og kan muligens overføres til `KHgraveyard.R`. 

## KHgraveyard.R
Lastes ikke inn. 

Inneholder utgåtte funksjoner som ikke brukes lenger. Andre funksjoner som erstattes eller utgår kan flyttes hit i stedet for å slettes. 