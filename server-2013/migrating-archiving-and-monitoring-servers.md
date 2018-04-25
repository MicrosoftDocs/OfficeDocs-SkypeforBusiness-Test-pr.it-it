---
title: Migrazione di server di archiviazione e Monitoring Server
TOCTitle: Migrazione di server di archiviazione e Monitoring Server
ms:assetid: 77831579-df45-4697-b8c5-207b74a07a40
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205015(v=OCS.15)
ms:contentKeyID: 49301032
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione di server di archiviazione e Monitoring Server

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Se sono stati distribuiti il server di archiviazione e il Monitoring Server nell'ambiente Lync Server 2010, sarà possibile distribuire questi server nell'ambiente Lync Server 2013 dopo la migrazione dei pool Front End. Se le funzionalità di archiviazione e monitoraggio sono fondamentali nell'organizzazione, è consigliabile tuttavia aggiungerle al pool pilota di Lync Server 2013 prima della migrazione, in modo che queste funzionalità siano disponibili durante il processo di migrazione.

Se si desidera usufruire delle funzionalità di archiviazione e monitoraggio durante la fase di migrazione, tenere conto delle considerazioni seguenti:

  - I dati di archiviazione e di monitoraggio non vengono spostati nella distribuzione di Lync Server 2013. I dati di cui è stato eseguito il backup prima della rimozione delle autorizzazioni per l'ambiente legacy costituiranno la cronologia delle attività nell'ambiente Lync Server 2010.

  - La versione Lync Server 2010 di Archiving Server e Monitoring Server può essere associata solo a un pool Front End di Lync Server 2010. In Lync Server 2013, archiviazione e monitoraggio non sono più ruoli server bensì servizi integrati nel pool Front End di Lync Server 2013.

  - Durante il periodo di coesistenza della distribuzione legacy e di Lync Server 2013, la versione Lync Server 2010 del server di archiviazione e del Monitoring Server raccoglie dati per gli utenti situati nei pool di Lync Server 2010. Archiviazione e monitoraggio in Lync Server 2013 raccolgono dati per gli utenti situati nei pool di Lync Server 2013 pools.
    

    > [!NOTE]
    > Durante la fase di migrazione in cui si continua a utilizzare il perimetro legacy con il nuovo pool pilota di Lync Server 2013, la versione Lync Server 2010 del server di archiviazione continua a raccogliere dati per gli utenti situati nei pool di Lync Server 2010, e l' archiviazione in Lync Server 2013 raccoglie dati per gli utenti situati nei pool di Lync Server 2013 pools.



  - Se si utilizza una soluzione di archiviazione e monitoraggio di terze parti insieme al server di archiviazione e al Monitoring Server in Lync Server 2013, informarsi presso il fornitore su quando e come integrare la soluzione di terze parti con Lync Server 2013.

