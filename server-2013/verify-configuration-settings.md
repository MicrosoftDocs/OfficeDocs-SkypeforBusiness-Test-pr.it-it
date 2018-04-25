---
title: Verificare le impostazioni di configurazione
TOCTitle: Verificare le impostazioni di configurazione
ms:assetid: 51c2d1d9-63f7-43ab-88ca-b8913da7cede
ms:mtpsurl: https://technet.microsoft.com/it-it/library/JJ204885(v=OCS.15)
ms:contentKeyID: 49300573
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare le impostazioni di configurazione

 

_**Ultima modifica dell'argomento:** 2012-09-06_

È possibile convalidare la replica delle informazioni di configurazione nel server perimetrale eseguendo il cmdlet **Get-CsManagementStoreReplicationStatus** di Lync Server 2013 nel computer interno in cui è contenuto l' archivio di gestione centrale o in qualsiasi computer aggiunto al dominio in cui è installato Lync Server 2013, Componenti di base (OcsCore.msi).

I risultati iniziali possono indicare lo stato "False" anziché "True" per la replica. In questo caso, eseguire il cmdlet **Invoke-CsManagementStoreReplication** e attendere il completamento della replica prima di eseguire di nuovo **Get-CsManagementStoreReplicationStatus**.

