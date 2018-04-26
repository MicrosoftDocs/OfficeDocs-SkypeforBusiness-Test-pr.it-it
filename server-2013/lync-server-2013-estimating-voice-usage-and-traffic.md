---
title: "Lync Server 2013: Stima dell'utilizzo e del traffico vocale"
TOCTitle: Stima dell'utilizzo e del traffico vocale
ms:assetid: 621b08fb-f894-4d91-ac38-e443401b098b
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398439(v=OCS.15)
ms:contentKeyID: 49300762
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Stima dell'utilizzo e del traffico vocale Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-08-07_

Microsoft Lync Server 2013, Strumento di pianificazione utilizza la metrica seguente per stimare il traffico utente in ogni sito e il numero di porte necessarie per supportare tale traffico.

  -   
    Per un livello di **traffico leggero** (una chiamata PSTN per utente all'ora) considerare 15 utenti per porta.

  -   
    Per un livello di **traffico medio** (2 chiamate PSTN per utente all'ora) considerare 10 utenti per porta.

  -   
    Per un livello di **traffico pesante** (3 chiamate PSTN o più per utente all'ora) considerare 5 utenti per porta.

Il numero di porte determina a sua volta il numero di Mediation Server e gateway che saranno necessari. I gateway PSTN (Public Switched Telephone Network) distribuiti nella maggior parte delle organizzazioni variano in dimensione da 2 a 960 porte. Sono disponibili anche gateway più grandi, ma vengono utilizzati principalmente dai provider di servizi di telefonia.

Un'organizzazione con 10.000 utenti e traffico medio, ad esempio, necessiterebbe di 1000 porte. Il numero di gateway richiesti sarebbe uguale al numero totale di porte necessarie determinato in base alla capacità totale dei gateway.

