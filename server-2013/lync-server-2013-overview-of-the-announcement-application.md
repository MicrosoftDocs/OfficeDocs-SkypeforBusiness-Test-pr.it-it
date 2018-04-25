---
title: "Lync Server 2013: Panoramica dell'applicazione Annuncio"
TOCTitle: Panoramica dell'applicazione Annuncio
ms:assetid: 2abee804-2599-48bb-90b2-15df0bae5e20
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204757(v=OCS.15)
ms:contentKeyID: 49300015
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Panoramica dell'applicazione Annuncio in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-13_

Quando si distribuisce l' applicazione Annuncio, è necessario configurare una tabella dei numeri non assegnati che determina l'azione da intraprendere quando un utente compone un numero non assegnato. La tabella dei numeri non assegnati contiene intervalli di numeri di telefono che sono validi per l'organizzazione e specifica quale applicazione Annuncio gestisce ogni intervallo. Quando un chiamante compone un numero di telefono valido per l'organizzazione ma non assegnato, tramite Lync Server il numero viene cercato nella tabella di routing dei numeri non assegnati, viene identificato l'intervallo che contiene il numero e viene eseguito il routing della chiamata all' applicazione Annuncio specificata per tale intervallo. L' applicazione Annuncio risponde alla chiamata e riproduce un messaggio audio (se configurato) e quindi disconnette la chiamata o la trasferisce a una destinazione predeterminata, ad esempio un operatore. È possibile usare i cmdlet di Lync Server Management Shell per configurare più messaggi audio o per il trasferimento alle destinazioni.

Il modo in cui configurare la tabella dei numeri non assegnati dipende da come si desidera usarla. Se si dispone di numeri specifici non più in uso e si desidera riprodurre messaggi personalizzati per ogni numero, è possibile immettere tali numeri specifici nella tabella dei numeri non assegnati. Se, ad esempio, è stato modificato il numero del Service Desk clienti, è possibile immettere il vecchio numero del servizio clienti e associarlo a un annuncio che fornisce il nuovo numero. Se si desidera riprodurre un messaggio generale a chiunque chiami un numero non assegnato, ad esempio per dipendenti che non lavorano più nell'organizzazione, è possibile immettere intervalli per tutti gli interni validi dell'organizzazione. La tabella dei numeri non assegnati viene richiamata ogni volta che il chiamante compone un numero attualmente non assegnato.

In Lync Server 2013 l' applicazione Annuncio viene installata automaticamente con l' applicazione Response Group. Le applicazioni Announcement e Response Group sono componenti standard di una distribuzione di VoIP aziendale e quando si distribuisce VoIP aziendale, entrambe le applicazioni vengono distribuite automaticamente.

