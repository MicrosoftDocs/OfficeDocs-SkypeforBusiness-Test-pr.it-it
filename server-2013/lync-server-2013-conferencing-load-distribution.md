---
title: Distribuzione del carico per le conferenze
TOCTitle: Distribuzione del carico per le conferenze
ms:assetid: 5901a076-1b6f-4720-8837-95fc7f3c37f3
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204922(v=OCS.15)
ms:contentKeyID: 49300624
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Distribuzione del carico per le conferenze

 

_**Ultima modifica dell'argomento:** 2012-10-22_

A differenza di altre soluzioni per conferenza dedicate, l'architettura di Lync Server è un modello di hardware condiviso. Questo significa che lo stesso hardware viene condiviso da molti componenti software, ognuno dei quali supporta tipi diversi di comunicazione in tempo reale. Ciascun tipo di comunicazione in tempo reale impone un carico specifico ai server. Ad esempio, un Front End Server può eseguire componenti di routing SIP (Session Initiation Protocol), applicazioni Web (come la ricerca nella Rubrica), il servizio Web Conferencing, il servizio A/V Conferencing, applicazioni VoIP aziendale (ad esempio, l'applicazione Operatore Conferenza e l'applicazione Response Group), e il Mediation Server. Un set di database nel Front End Server fornisce inoltre funzionalità di archiviazione ed elaborazione dei dati utente, contatto, presenza, conferenze e routing vocale. Con la condivisione dell'hardware i componenti, i servizi e i processi sono in competizione per le risorse di CPU e memoria, e quindi i carichi di lavoro non correlati alle conferenze influiscono in modo diretto sulla scalabilità dei server.

Rispetto ad altre soluzioni per conferenza basate su porte, l'architettura di conferenza di Lync Server è un modello senza prenotazione. Quando un utente pianifica una riunione, Lync Server crea un record nel database delle conferenze, in cui sono archiviati i dati relativi alle conferenze, ma non prenota in anticipo risorse hardware per la riunione pianificata. Lync Server dispone di una logica di bilanciamento del carico predefinita per allocare dinamicamente le risorse per le conferenze nei Front End Server in modo da distribuire equamente i carichi tra tutti i Front End Server del pool. Questo sistema esegue il provisioning e usa le risorse hardware in modo efficiente, ma rende difficile supportare le riunioni di dimensioni molto grandi (soprattutto se non è stata eseguita una pianificazione accurata). Ad esempio, quando un pool Lync Server 2013 ha a disposizione tutta o quasi la propria capacità, ogni Front End Server può ospitare circa 125 riunioni di medie dimensioni. Aggiungere un'altra riunione di piccole dimensioni non è un problema, ma lo sarebbe se la riunione prevedesse 1000 utenti, perché i Front End Server non riuscirebbero probabilmente a supportare una riunione così grande contemporaneamente alle altre 125.

