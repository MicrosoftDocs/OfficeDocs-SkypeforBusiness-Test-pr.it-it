---
title: 'Lync Server 2013: Panoramica del server Director'
TOCTitle: Panoramica del server Director
ms:assetid: cf9919b3-e16b-47c5-be1d-2c4bc64f44ea
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398879(v=OCS.15)
ms:contentKeyID: 49302032
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica del server Director in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

Un Server Director è un server Lync Server 2013 che autentica le richieste degli utenti, ma non ospita account utente. È possibile distribuire facoltativamente un Server Director nei due scenari seguenti:

  - Se si abilita l'accesso degli utenti esterni mediante la distribuzione di server perimetrali, è inoltre necessario distribuire un Server Director. In questo scenario il Server Director autentica gli utenti esterni e trasferisce il relativo traffico ai server interni. Se si utilizza un Server Director per l'autenticazione degli utenti esterni, viene ridotto il sovraccarico per i server del pool Front End generato dall'autenticazione di questi utenti. Consente inoltre di isolare i pool Front End interni dal traffico dannoso, ad esempio da attacchi di tipo DoS (Denial-of-Service). Se la rete è inondata da traffico esterno non valido durante un attacco di questo tipo, il traffico termina nel Director.

  - Se si distribuiscono più pool Front End in un sito centrale e si aggiunge un Server Director a tale sito, è possibile semplificare le richieste di autenticazione e migliorare le prestazioni. In questo scenario tutte le richieste vengono trasmesse innanzitutto al Server Director, che quindi le instrada al pool Front End corretto.

