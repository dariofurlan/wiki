---
title: Clean Architecture
tags:
 - architecture
aliases:
 - Ports & Adapters
 - Hexagonal Architecture
---

## Descrizione
Architettura esagonale, conosciuta anche come Clean Architecture[^1] o Ports & Adapters[^2], sottolinea la separazione trail dominio applicativo e i dettagli implementativi. Tramite questo modello il sistema è piùfacile da testare, da effettuare manutenzione e flessibile ai cambiamenti.

[^1]: "The Clean Architecture" [source](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

[^2]: "DDD, Hexagonal, Onion, Clean, CQRS, ... How I put it all together" [source](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/)

## Blocchi Fondamentali

All’interno dell’architettura esagonale sono presenti tre blocchi di codice principali:
- Ciò che rende possibile eseguire una **interfaccia utente**, qualsiasi tipo essa sia: pagine web, applicazioni desktop, linea di comando.
- La **logica di business**, o nucleo applicativo, il quale verrà utilizzato dall’interfaccia utente al fine di compiere azioni.
- Il codice per la **infrastruttura** responsabile dell’interazione con strumenti esterni quali database, motori di ricerca o API di terze parti.