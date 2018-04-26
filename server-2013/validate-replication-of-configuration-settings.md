---
title: Convalidare la replica delle impostazioni di configurazione
TOCTitle: Convalidare la replica delle impostazioni di configurazione
ms:assetid: 81a3c21d-b28a-4287-adac-11791e8db56d
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ205042(v=OCS.15)
ms:contentKeyID: 49301150
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Convalidare la replica delle impostazioni di configurazione

 

_**Ultima modifica dell'argomento:** 2012-10-19_

È possibile convalidare la replica delle informazioni di configurazione nel server perimetrale eseguendo il cmdlet **Get-CsManagementStoreReplicationStatus** di Lync Server 2013 nel computer interno in cui è contenuto l'archivio di gestione centrale o in qualsiasi computer aggiunto al dominio in cui è installato Lync Server 2013, Componenti di base.

I risultati iniziali possono indicare lo stato "False" anziché "True" per la replica. In questo caso, eseguire il cmdlet **Invoke-CsManagementStoreReplication** e attendere il completamento della replica prima di eseguire di nuovo **Get-CsManagementStoreReplicationStatus**.

