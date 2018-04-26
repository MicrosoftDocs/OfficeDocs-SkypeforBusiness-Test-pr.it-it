---
title: 'Lync Server 2013: Verificare la connettività tra server interni e server perimetrali'
TOCTitle: Verificare la connettività tra server interni e server perimetrali
ms:assetid: 219f706e-2b8a-46c5-b394-c384240eef50
ms:mtpsurl: https://technet.microsoft.com/it-it/library/Gg398292(v=OCS.15)
ms:contentKeyID: 49299914
ms.date: 08/24/2015
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Verificare la connettività tra server interni e server perimetrali in Lync Server 2013

 

_**Ultima modifica dell'argomento:** 2012-09-08_

In Lync Server 2013 è disponibile una procedura guidata di convalida a parte per verificare la connettività tra gli Edge Server e i server interni. In Lync Server 2013 la convalida della connettività viene eseguita automaticamente quando si installano gli Edge Server.

È possibile convalidare la replica delle informazioni di configurazione nel perimetro eseguendo il cmdlet **Get-CsManagementStoreReplicationStatus** di Windows PowerShell nel computer interno in cui è contenuto l' archivio di gestione centrale o in qualsiasi computer aggiunto al dominio in cui è installato Lync Server 2013, Componenti di base (OcsCore.msi). I risultati iniziali possono indicare lo stato "False" anziché "True" per la replica. In questo caso, eseguire il cmdlet **Invoke-CsManagementStoreReplication** e attendere il completamento della replica prima di eseguire di nuovo **Get-CsManagementStoreReplicationStatus**.

È possibile verificare la connettività degli utenti esterni separatamente, utilizzando tra l'altro l'analizzatore connettività remota di Office Communications Server per verificare la connettività degli utenti remoti. Per informazioni dettagliate, vedere [Verificare la connettività per gli utenti esterni in Lync Server 2013](lync-server-2013-verify-connectivity-for-external-users.md).

