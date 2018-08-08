---
title: "Lync Server 2013: Ripristino del contenuto delle conferenze tramite backup"
TOCTitle: Ripristino del contenuto delle conferenze tramite il servizio di backup
ms:assetid: 3e0f18ec-7319-4c07-a59b-2938e7787bc9
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ688030(v=OCS.15)
ms:contentKeyID: 49887530
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Ripristino del contenuto delle conferenze tramite il servizio di backup in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-11-01_

Se le informazioni sulla conferenza memorizzate nell'archivio file di un pool Front End diventano non disponibili, è necessario ripristinarle in modo che gli utenti presenti nel pool possano mantenere i propri dati della conferenza. Se il pool Front End che ha perso i dati della conferenza è associato a un altro pool Front End, è possibile utilizzare il servizio di backup per ripristinarli.

È inoltre necessario eseguire questa attività se si verifica un errore dell'intero pool e si deve eseguire il failover degli utenti che vi appartengono in un pool di backup. Quando viene eseguito nuovamente il failover di questi utenti nel pool originale, è necessario utilizzare questa procedura anche per copiare il contenuto della conferenza nel pool originale.

Partire dal presupposto che Pool1 è associato a Pool2 e che i dati della conferenza di Pool1 siano stati persi. È possibile usare il cmdlet seguente per richiamare il servizio di backup e ripristinare il contenuto:

    Invoke-CsBackupServiceSync -PoolFqdn <Pool2 FQDN> -BackupModule ConfServices.DataConf

Il ripristino del contenuto della conferenza può richiedere del tempo, a seconda delle dimensioni. È possibile usare il cmdlet seguente per verificare lo stato del processo:

    Get-CsBackupServiceStatus -PoolFqdn <Pool2 FQDN> -BackupModule ConfServices.DataConf

Il processo è terminato quando questo cmdlet restituisce il valore di stato stabile per il modulo della conferenza dati.

