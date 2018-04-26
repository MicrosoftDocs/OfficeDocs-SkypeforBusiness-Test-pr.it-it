---
title: Migrazione di server di archiviazione e Monitoring Server
TOCTitle: Migrazione di server di archiviazione e Monitoring Server
ms:assetid: 8d879253-ad76-42b7-8386-e44b110239cf
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688124(v=OCS.15)
ms:contentKeyID: 49887648
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Migrazione di server di archiviazione e Monitoring Server

 

_**Ultima modifica dell'argomento:** 2012-10-02_

Se su distribuiscono Archiving Server e Monitoring Server in Office Communications Server 2007 R2, è possibile distribuire tali server nell'ambiente Lync Server 2013 dopo aver eseguito la migrazione dei pool Front End. Se le funzionalità di archiviazione e monitoraggio sono di importanza cruciale per l'organizzazione, tuttavia, è consigliabile aggiungerle al pool pilota prima di eseguire la migrazione in modo che le funzionalità siano disponibili durante il processo di migrazione.

Se si desiderano funzionalità di archiviazione e monitoraggio durante la fase di migrazione e coesistenza, tenere presente quanto segue:

  - I dati di archiviazione e di monitoraggio non vengono spostati nella distribuzione di Lync Server 2013. I dati di cui si esegue il backup prima della rimozione delle autorizzazioni dell'ambiente legacy rappresentano la cronologia delle attività in Office Communications Server 2007 R2.

  - La versione Office Communications Server 2007 R2 di Archiving Server e Monitoring Server può essere associata solo a un pool Front End di Office Communications Server 2007 R2. In Lync Server 2013, archiviazione e monitoraggio non sono più ruoli server bensì servizi integrati nel pool Front End di Lync Server 2013.

  - Durante il periodo di coesistenza della distribuzione legacy e di Lync Server 2013, la versione Office Communications Server 2007 R2 del server di archiviazione e del Monitoring Server raccoglie dati per gli utenti situati nei pool di Office Communications Server 2007 R2. La versione Lync Server 2013 del server di archiviazione e del Monitoring Server invece raccoglie dati per gli utenti situati nei pool di Lync Server 2013.
    

    > [!NOTE]
    > Durante la fase di migrazione in cui si continua a utilizzare il server perimetrale legacy con il nuovo pool pilota di Lync Server 2013, la versione Office Communications Server 2007 R2 del server di archiviazione continua a raccogliere dati per gli utenti situati nei pool di Office Communications Server 2007 R2 e la versione Lync Server 2013 del server di archiviazione raccoglie dati per gli utenti situati nei pool di Lync Server 2013.



  - Se si utilizza una soluzione di archiviazione e monitoraggio di terze parti insieme al server di archiviazione e al Monitoring Server, informarsi presso il fornitore su quando e come integrare la soluzione di terze parti con Lync Server 2013.

