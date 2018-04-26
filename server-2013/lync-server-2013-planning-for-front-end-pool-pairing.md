---
title: "Lync Server 2013: Pianificazione dell'abbinamento dei pool Front End"
TOCTitle: Pianificazione dell'abbinamento dei pool Front End
ms:assetid: cca5773d-57ff-45ce-a7b4-f82ae697c477
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205293(v=OCS.15)
ms:contentKeyID: 49302002
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Pianificazione dell'abbinamento dei pool Front End in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-28_

Per sfruttare al meglio le funzionalità di ripristino di emergenza disponibili in Lync Server 2013, distribuire coppie di pool Front End su due siti in zone geografiche diverse. Ogni sito include un pool Front End accoppiato a un pool Front End corrispondente nell'altro sito. Entrambi i siti sono attivi e il servizio di backup di Lync Server garantisce la replica dei dati in tempo reale per mantenere i pool sincronizzati. Il servizio di backup è una nuova funzionalità di Lync Server 2013 progettata per supportare la soluzione di ripristino di emergenza. Viene installato in un pool Front End quando il pool viene accoppiato con un altro pool Front End.

Se si verifica un errore nel pool di un sito, è possibile spostare tramite failover gli utenti di tale pool nel pool dell'altro sito, che quindi fornisce servizi a tutti gli utenti di entrambi i pool. Ai fini della pianificazione della capacità, ogni pool deve essere progettato in modo da poter gestire i carichi di lavoro di tutti gli utenti di entrambi i pool qualora si verifichi una situazione di emergenza.

## Contenuto della sezione

  - [Opzioni e procedure consigliate per l'abbinamento dei pool per Lync Server 2013](lync-server-2013-supported-pool-pairing-options-and-best-practices.md)

  - [Eseguire il backup delle relazioni di registrazione in Lync Server 2013](lync-server-2013-backup-registrar-relationships.md)

  - [Tempo di ripristino per il failover e il failback dei pool in Lync Server 2013](lync-server-2013-recovery-time-for-pool-failover-and-pool-failback.md)

  - [Failover dell'archivio di gestione centrale in Lync Server 2013](lync-server-2013-central-management-store-failover.md)

  - [Sicurezza dei dati per l'abbinamento dei pool Front End in Lync Server 2013](lync-server-2013-front-end-pool-pairing-data-security.md)

