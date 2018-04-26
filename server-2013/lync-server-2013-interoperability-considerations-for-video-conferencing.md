---
title: Considerazioni sull'interoperabilità delle videoconferenze
TOCTitle: Considerazioni sull'interoperabilità delle videoconferenze
ms:assetid: 31ead3b5-ed95-42d4-96e2-7d9403d5c026
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204790(v=OCS.15)
ms:contentKeyID: 49300112
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Considerazioni sull'interoperabilità delle videoconferenze

 

_**Ultima modifica dell'argomento:** 2012-10-02_

In questa sezione viene descritta l'esperienza utente durante la fase di coesistenza della migrazione, quando si stabilisce un'interoperabilità tra i client legacy e un pool di Lync Server 2013 o i client Lync Server 2013 e un pool legacy.

## Pool di Lync Server 2013

Quando un client legacy viene usato in un pool di Lync Server 2013, gli utenti osserveranno il comportamento seguente:

  - Per le chiamate a due parti, la risoluzione video è identica a quella del pool legacy.

  - Per le conferenze multiparte, la risoluzione video e le funzionalità di videoconferenza sono identiche a quelle del pool legacy. La visualizzazione Raccolta e la risoluzione elevata non sono disponibili.

## Pool legacy

Quando un client Lync Server 2013 viene usato in un pool legacy, gli utenti osserveranno il comportamento seguente:

  - Per le chiamate a due parti, i client Lync Server 2013 possono usare le nuove funzionalità nel modo seguente:
    
      - H.264 è disponibile se entrambi i partecipanti usano i clienti Lync Server 2013.
    
      - Il client Lync Server 2013 usa il valore predefinito per TotalReceiveVideoBitRateKb, in quanto il server legacy non invia queste informazioni con il provisioning in banda.

  - Per le conferenze multiparte, la risoluzione video e le funzionalità di videoconferenza sono identiche a quelle del client legacy nel pool legacy.


> [!NOTE]
> Quando un server legacy ospita un client Lync Server 2013, è possibile configurare la larghezza di banda delle videoconferenze in modo che tutti gli utenti del pool ricevano solo video a risoluzione bassa, ma inviino video a risoluzione elevata. Un esempio è quando si imposta MaxVideoRateAllowed su CIF-250K nella configurazione dei contenuti multimediali e VideoBitRateKb è impostato su 2000 kbps nei criteri di conferenza. L'effetto in questa situazione è che la risoluzione elevata non è disponibile per gli utenti del pool.<BR>Poiché MaxVideoRateAllowed non è più usato per i client Lync Server 2013, non può impedire che tali client richiedano video a risoluzione elevata. Impostare invece VideoBitRateKb nei criteri di conferenza per tutti gli utenti del pool sullo stesso valore di MaxVideoRateAllowed, ovvero CIF viene impostato su 250 kbps, VGA viene impostato su 600 kbps o HD viene impostato su 1500 kbps.


