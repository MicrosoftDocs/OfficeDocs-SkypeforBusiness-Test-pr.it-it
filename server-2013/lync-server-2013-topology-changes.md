---
title: 'Lync Server 2013: Modifiche della topologia'
TOCTitle: Modifiche della topologia
ms:assetid: 9e40ef93-9ab0-498c-9bbf-f94584353e53
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688153(v=OCS.15)
ms:contentKeyID: 49887676
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Modifiche della topologia in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-10-02_

I requisiti e le considerazioni sulla topologia di Lync Server 2013 si differiscono da quelli delle versioni precedenti, come descritto in questa sezione.

## Nuova architettura dei pool Front End

In Lync Server 2013, l'architettura di Enterprise Editionpool Front End è stata modifica per passare a un architettura di sistemi distribuiti.

Con questa nuova architettura, il database di back-end non è più l'archivio dati in tempo reale in un pool. Le informazioni su uno specifico utente vengono mantenute nei tre server Front End nel pool. Per ogni utente, un server Front End agisce come master per le informazioni dell'utente e due altri server Front End servono come repliche. Se un server Front End diventa inattiva, un altro server Front End che veniva usato per la replica viene automaticamente alzato al livello master.

Ciò avviene in background e gli amministratori non hanno bisogno di sapere quali server Front End sono master e per quali utenti. Questa distribuzione dell'archiviazione dei dati migliora le prestazioni e la scalabilità nel pool ed elimina il singolo punto di errore di un singolo server back-end.

Il server back-end funge da archivio di backup per i dati di utenti e conferenze e rappresenta anche l'archivio principale per altri database come il database di Response .

Questi miglioramenti implicano anche modifiche alla modalità di pianificazione e manutenzione dei pool. È consigliabile che tutti i Enterprise Editionpool Front End includano almeno tre server Front End, per fornire il numero completo di repliche per cui è progettata l'architettura del pool Front End. Inoltre, è necessario eseguire alcune procedure per l'aggiunta di server a un pool Front End, rimuovere server da esso, o aggiornare i server. Per ulteriori informazioni, vedere [Topologie e componenti per Front End Server, messaggistica istantanea e presenza in Lync Server 2013](lync-server-2013-topologies-and-components-for-front-end-servers-instant-messaging-and-presence.md).

## Modifiche alla topologia dei ruoli server

Alcuni ruoli server eseguiti precedentemente in server distinti sono ora consolidati nel ruolo Front End Server, il che consente di risparmiare sui costi dell'hardware

  - In Lync Server 2013, A/V Conferencing Server è sempre collocato con Front End Server.

  - I front-end per monitoraggio e archiviazione sono sempre collocati con Front End Server. Il monitoraggio e l'archiviazione di ogni server richiedono ancora un database back-end separato che può trovarsi nello stesso server del database back-end del pool Front End oppure ospitato in server back-end distinti.

  - server Chat persistente è ora un ruolo server. In Microsoft Lync Server 2010, Group Chat Server è un'applicazione attendibile di terze parti per Microsoft Lync Server 2010. In Lync Server 2013, le funzionalità di server Chat persistente sono implementate mediante tre nuovi ruoli server:
    
      - **PersistentChatService :** servizi principali di server Chat persistente implementati come ruolo front-end
    
      - **PersistentChatStore :** ruolo server back-end
    
      - **PersistentChatComplianceStore :** ruolo server back-end per conformità con Chat persistente Compliance

